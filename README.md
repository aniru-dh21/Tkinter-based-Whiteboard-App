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

4. `prev_x, prev_y = event.x, event.y`:
