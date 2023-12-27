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
