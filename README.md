# Whiteboard App with Python and Tkinter

A white board tool written in Python with Tkinter.

## Building the Drawing Feature

``` python
def start_drawing(event):
    global is_drawing, prev_x, prev_y
    is_drawing = True
    prev_x, prev_y = event.x, event.y
```
