# Whiteboard App with Python and Tkinter

A white board tool written in Python with Tkinter.

## Building the Drawing Feature

``` python
def start_drawing(event):
    global is_drawing, prev_x, prev_y
    is_drawing = True
    prev_x, prev_y = event.x, event.y
```

This code define a function named `start_drawing` that is meant to handle the beginning of a drawing action in a graphical user interface (GUI) application.

Break down of what this function does:

1. `def start_drawing(event)`: This line defines a function named `start_drawing` that takes an event as its parameter. In GUI programming, events are actions or occurences (like mouse clicks, key presses and so on) that trigger specific function when they happen.

2. `global is_drawing, prev_x, prev_y`: This line declares that the variables `is_drawing`, `prev_x` and `prev_y` are global variables. In Python, global variables are accessible from anywhere in the code and can be modified within functions. This line ensures that these variables are accessible within the function.

3. `is_drawing = True`: This line sets the `is_drawing` variable to `True`. This variable is typically used to indicate whether a drawing action is in progress. By setting it to `True`, the function signals that a drawing action has started.

4. `prev_x, prev_y = event.x, event.y`: This line captures the current coordinates of the mouse cursor when the `start_drawing` function is called. It assigns the `x` and `y` coordinates of the mouse cursor at that moment to the `prev_x` and `prev_y` variables. These variables are used to track the starting point of the drawing action.

So when this function us called (usually in response to a mouse click event), it sets the `is_drawing` flag to `True` to indicate the a drawing action is in progress and records the initial position of the mouse cursor using the `prev_x` and `prev_y` variables. These variables are then used in the subsequent drawing actions to connect the starting point with the current cursor position to create a drawing on the canvas.

Next up, the function to actually draw on the whiteboard, like this:
``` python
def draw(event):
    global is_drawing, prev_x, prev_y
    if is_drawing:
        current_x, current_y = event.x, event.y
        canvas.create_line(prev_x, prev_y, current_x, current_y, fill=drawing_color, width=line_width, capstyle=tk.ROUND, smooth=True)
        prev_x, prev_y = current_x, current_y
```

A drawing is essentially a combination of points filled with colors, functioning as a vector. To work as a vector, it needs to have a starting and ending point. So after creating a function to start drawing, it'll need a function to stop drawing, like this:
``` python
def stop_drawing(event):
    global is_drawing
    is_drawing = False
```

### Building the Color Changing Feature

Now that after having primary drawing functionality, the next step is to implement the color-changing function. This is a simple function that calls the `askcolor` module, which is already part of Tkinter, like this:
``` python
def change_pen_color():
    global drawing_color
    color = askcolor()[1]
    if color:
        drawing_color = color
```

For the last functionality, create a function to adjust the line width, allowing you to choose the thinkness of your lines. Here's how to implement it:
``` python
def change_line_width(value):
    global line_width
    line_width = int(value)
```

Now we've completed the functions. Next we'll use Tkinter to create the window for your app and buttons for choosing colors, clearing the whiteboard, and selecting your line width.

## Building the GUI

GUI stands for Graphical User Interface, representing the windows you interact with on your computer, smartphone tablets, and so on.

When coding a desktop app using Python and Tkinter, we define the size, position, buttons, and any other elements we want for our program. In this case, we need to create the following assets:
- A title for app.
- A white blank canvas for drawing.
- A frame to hold the controls of our app in the same line.
- A color button.
- A clear canvas button to erase all our work and start drawing again.
- A slider to select your line width.

### Creating the window

``` python
root = tk.Tk()
root.title("Whiteboard App")

canvas = tk.Canvas(root, bg="white")
canvas.pack(fill="both", expand=True)

is_drawing = False
drawing_color = "black"
line_width = 2

root.geometry("800x600")
```

Let's break down what each part does:
1. `root = tk.Tk()`: This line creates the main application window. It initializes a Tkinter application and assigns it to the variable `root`. This window serves as the container for all the graphical elements of the whiteboard application.

2. `root.title("Whiteboard App")`: This sets the title of the application window to "Whiteboard App." The title appears in the title bar of the window and provides a name for the application.
