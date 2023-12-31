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

3. `canvas = tk.Canvas(root, bg="white")`: This line creates a drawing canvas within the main application window. The canvas is a white rectangular area where users can draw. It is initialized with a white background color. The canvas is assigned to the variable `canvas`.

4. `canvas.pack(fill="both", expand=True)`: This configures the canvas to fill both the horizontal and vertical space of the application window. It allows the canvas to expand and occupy the entire window.

5. `is_drawing = False`: This initializes a variable `is_drawing` to `False`. It's typically used to track whether the user is currently drawing or not. When the user starts drawing, this variable is set to `True` to indicate an ongoing drawing action.

6. `drawing_color = "black"`: This initializes a variable `drawing_color` to "block". It specifies the color that will be used for drawing on the canvas. You can change this color as needed to draw with different colors with the functions we will add.

7. `line_width = 2`: This initializes a variable `line_width` to 2. It specifies the width of the lines or strokes used for drawing. You can adjust this value to change the thickness of the lines.

8. `root.geometry("800x600")`: This sets the initial size of the application window to 800 pixels in width and 600 pixels in height. It defines the dimensions of the window when it is first displayed but you can resize your window and with it, your canvas space.

### Building Navbar and Controls

Next thing is to do is create a frame to hold the buttons or controls in the same line. This is the most comfortable way to have buttons, and it's kind of a navbar.
``` python
controls_frame = tk.Frame(root)
controls_frame.pack(side="top", fill="x")
```

Then, create two buttons and give them default fixed positions in screen, like this:
``` python
color_button = tk.Button(controls_frame, text="Change Color", command=change_pen_color)
clear_button = tk.Button(controls_frame, text="Clear Canvas", command=lambda: canvas.delete("all"))

color_button.pack(side="left", padx=5, pady=5)
clear_button.pack(side="left", padx=5, pady=5)
```

The application already have the two main buttons for app, one to change colors and one to clear the canvas. The last control we need to create is slider for the line width function. This is the following code:
``` python
line_width_label = tk.Label(controls_frame, text="Line Width:")
line_width_label.pack(side="left", padx=5, pady=5)

line_width_slider = tk.Scale(controls_frame, from_=1, to=10, orient="horizontal", command=lambda val: change_line_width(val))
line_width_slider.set(line_width)
line_width_slider.pack(side="left", padx=5, pady=5)
```

1. `line_width_label = tk.Label(controls_frame, text="Line Width:`: This line creates a label widget with the text "Line Width." The label is intended to display text to describe the purpose of the following slider (which controls the line width). It is placed within the `controls_frame` widget.

2. `line_width_label.pack(side="left", padx=5, pady=5)`: This line configures the label's placement within the `controls_frame`.

3. `side="left"`: This sets the label to be placed on the left side of the `controls_frame`. It ensures that the label is aligned to the left.

4. `padx=5`: It adds horizontal padding of 5 pixels around the label, creating some spacing.
   
5. `pady=5`: It adds vertical padding of 5 pixels around the label, creating spacing.

6. `line_width_slider = tk.Scale(controls_frame, from_=1, to=10, orient="horizontal", command=lambda val: change_line_width(val))`: This line creates a horizontal slider widget (Scale widget) that allows the userto select a line width. The slider ranges from a minimum value of 1 (`from_=1`) to a maximum value of 10 (`to=10`). The `command` option is set to call the `change_line_width` function with the selected value whenever the slider position changes.

7. `line_width_slider.set(line_width)`: This sets the initial position of the slider to the value stored in the `line_width` variable, which is initialized earlier in the code. This ensures that the slider starts at the default line width.

8. `line_width_slider.pack(side="left", padx=5, pady=5)`: This line configures the slider's placement within the `controls_frame`. It is placed on the left side, and padding is added to create spacing around the slider.

### Connnecting features with GUI

But if we press the buttons or move the slider for line width, it won't work because you still need to bind or "link" the functions coded at the beginning.

For that:
``` python
canvas.bind("<Button-1>", start_drawing)
canvas.bind("<B1-Motion>", draw)
canvas.bind("<ButtonRelease-1>", stop_drawing)

root.mainloop()
```

1. `canvas.bind("<Button-1>", start_drawing)`: When the left mouse button is clicked on the canvas, it triggers the `start_drawing` function.

2. `canvas.bind("<B1-Motion>", draw)`: While the left mouse button is held down and the mouse is moved on the canvas, it triggers the draw function.

3. `canvas.bind("<ButtonRelease-1>", stop_drawing)`: When the left mouse button is released (button released event), it triggers the `stop_drawing` function.

4. And finally, `root.mainloop()` starts the main loop of the application, allowing it to respond to user interactions and events.
