layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# GUI Programming in Python

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  

---
# Graphical User interface

* Python does not have GUI programming features bulilt into the language itself.


* `tkinter` package allows programmers to create simple GUI programs.
   * `tkinter` is short for "Tk interface"
   * `tkinter` was written by Steen Lumholt and Guido van Rossum.
   * `tkinter` is a set of wrappers that implement the Tk widgets as Python classes


* `Tk` is a platform independent GUI framework developed for `Tcl`.
   * `Tk` was written in C by John Ousterhout while at Berkeley (1991).
   * `Tk` was developed as an extension for the `Tcl` scripting language


.center[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d3/Tcl-Tk_universal_scripting.svg/800px-Tcl-Tk_universal_scripting.svg.png" width=150/>]

---
# Graphical User Interfaces

* **User Interface**: the part of the computer with which the user interacts


* **Command line interface**: displays a prompt and the user types a command that is then executed


* **Graphical User Interface (GUI)**: allows users to interact with a program through graphical elements on the screen


* GUI programs are .red[event-driven] because they must repond to the actions of the user.
   * The user determines the order in which things happen
   * The user causes `events` to take place and the program responds to the events


---
# Graphical User Interfaces

* Graphical user interface (GUI) was derived from **Sketchpad** (1963, .purple[Ivan E. Sutherland]) -> ".red[talking graphically with a computer!]"

.center[<img src="https://upload.wikimedia.org/wikipedia/en/7/7b/Sketchpad-Apple.jpg">]

* Engelbart's prototype of a **computer mouse**, as designed by Bill English from .purple[Douglas Engelbart]'s sketches (1963)  

.center[<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/SRI_Computer_Mouse.jpg" width=190/>
<img src="https://upload.wikimedia.org/wikipedia/commons/e/ed/Mouse-patents-englebart-rid.png" height=100/>]

---
# Graphical User Interfaces

.row[
.col-6[

<img src="https://user-images.githubusercontent.com/39995503/100191200-13fb3580-2f33-11eb-858d-73a6d35d5d65.png" width=400/>
]
.col-6[

* `tkinter` package: allows you to create simple GUI programs
   * fast, and usually comes with Python
   * IDLE was implemented with `tkinter` package


* `Widget`: graphical element that the user can interact with or view
   * Presented by a GUI program

]
]
 


---
# A Simple GUI Program

.row[
.col-8.font-14[
```python3
import tkinter as tk

class Application(tk.Frame):
    def __init__(self, master=None):
        super().__init__(master)
        self.master = master
        self.pack()
        self.create_widgets()

    def create_widgets(self):
        self.hi_there = tk.Button(self)
        self.hi_there["text"] = "Hello World\n(click me)"
        self.hi_there["command"] = self.say_hi
        self.hi_there.pack(side="top")

        self.quit = tk.Button(self, text="QUIT", fg="red",
                              command=self.master.destroy)
        self.quit.pack(side="bottom")

    def say_hi(self):
        print("hi there, everyone!")

root = tk.Tk()
app = Application(master=root)
app.mainloop()
```
]
.col-4[
.left[<img src="https://user-images.githubusercontent.com/39995503/100352391-4179d900-3030-11eb-92a0-228d052d9560.png" width=250/>]

```python3 
hi there, everyone!
>>>
``` 
]
]
---
# Tk Concepts

* **widgets**
   * Widgets are all the things that you see on screen   
   * Each widget is a Python object, an instance of a class


* **geometry management**
   * A geometry manager's job is to figure out exactly where those widgets are going to be put
   * taking control of the .red[master widget] and deciding how all the .red[slave widgets] will be displayed within it
   * A master is a widget, typically a toplevel application window or a frame, which contains other widgets, called slaves


* **event handling**
   * Tk runs an .red[event loop] that receives events from the operating system
   * using a widget-specific command .red[callback]
   * binding a function to an event

---
# Creating Widgets

* Each separate widget is a Python object. 


* When instantiating a widget, you must pass its .red[parent] as a parameter to the widget class. 
   * The only exception is the .red[root] window, which is the `toplevel` window that will contain everything else. 
   * `toplevel` window automatically created when you instantiate `Tk`. It does not have a parent.
   * All widgets have several .red[configuration options] that control .purple[how the widget is displayed] or .pink[how it behaves].

.font-15[
```python3
from tkinter import *
from tkinter import ttk

root = Tk()
content = ttk.Frame(root)
button = ttk.Button(content, text="Hello", command=buttonpressed)
button['text'] = 'goodbye'
button['textvariable'] = strLabel
```
]

---
# Frame

* A frame is a widget that displays as a simple .red[rectangle].
* Frames help to .red[organize] user interface.
* Frames often act as .red[master widgets] for a geometry manager like `grid`, which manages the slave widgets contained within the frame.

.font-15[
```python3
frame = ttk.Frame(parent)
frame['padding'] = 5             # 5 pixels on all sides
#frame['padding'] = (5,10)       # 5 on left and right, 10 on top and bottom
#frame['padding'] = (5,7,10,12)  # left: 5, top: 7, right: 10, bottom: 12
frame['borderwidth'] = 2
frame['relief'] = 'sunken'
```
]

.center[<img src="https://tkdocs.com/images/w_frame_all.png" height=170/>]

---
# Label

* A label is a widget that displays text or images.
* typically users will just view it but not otherwise interact with it.

.font-15[
```python3
label = ttk.Label(parent, text='Your Name:')
resultsContents = StringVar()
label['textvariable'] = resultsContents
resultsContents.set('New value to display')  # get/set
label['background'] = red
```
]
.font-15[
```python3
image = PhotoImage(file='myimage.gif')
label['image'] = image
label['compound'] = top # image above text (text/image/center/top/left/bottom/right)
```
]

.center[<img src="https://tkdocs.com/images/w_label_all.png" height=150/>]

---
# Cnnecting Widgets to Variables

* Widgets can be linked to application variables by using some configuration options: 
   * `variable`, `textvariable`, `onvalue`, `offvalue`, and `value`. 


* Not possible to connect a regular Python variable to a widget 
* `get()`/`set()` for reading and changing the value

```
s = StringVar()   # string; default to ""
i = IntVar()      # integer; default to 0
d = DoubleVar()   # float; default to 0.0
b = BooleanVar()  # boolean; 0 for False, 1 for True
```

---
# Button

* A button, unlike a frame or label, is to interact with a user.
* display text or images, and accept additional options to change their behavior.

.font-15[
```python3
button = ttk.Button(parent, text='Okay', command=submitForm)
button['default'] = active # active/normal, Default buttons are invoked if users hit the Return or Enter key
```
]

* The command option connects the button's action and your application. 
   * When a user presses the button, the script provided by the option is evaluated by the interpreter.

.font-15[
```python3
action = ttk.Button(root, text="Action", default="active", command=myaction)
root.bind('<Return>', lambda e: action.invoke())
```
]

.center[<img src="https://tkdocs.com/images/w_button_all.png" height=150/>]

---
# Button

* Buttons and many other widgets start off in a .red[normal] state. 
   * A button will respond to mouse movements, can be pressed, and will invoke its command callback. 


* Buttons can also be put into a .red[disabled] state, 
   * where the button is greyed out, does not respond to mouse movements, and cannot be pressed.


.font-15[
```python3
b.state(['disabled'])          # set the disabled flag
b.state(['!disabled'])         # clear the disabled flag
b.instate(['disabled'])        # true if disabled, else false
b.instate(['!disabled'])       # true if not disabled, else false
b.instate(['!disabled'], cmd)  # execute 'cmd' if not disabled
```
]

* .red[state flags] available to themed widgets is: 
   * `active`, `disabled`, `focus`, `pressed`, `selected`, `background`, `readonly`, `alternate`, and `invalid`.

---
# Checkbutton

* A checkbutton widget is like a regular button that also holds a binary value (i.e., a toggle).
* Checkbutton widgets are used to allow users to .red[turn an option on or off].

.font-15[
```python3
measureSystem = StringVar()
check = ttk.Checkbutton(parent, text='Use Metric', command=metricChanged, variable=measureSystem,
	    onvalue='metric', offvalue='imperial')
```
]

* The `variable` option links a variable to current value of the widget.
* The variable is updated whenever the widget is toggled. 
* By default, checkbuttons use a value of `1` when the widget is .red[checked], and `0` when .red[not checked]. 
   * These can be changed using the `onvalue` and `offvalue` options.

.center[<img src="https://tkdocs.com/images/w_checkbutton_all.png" height=150/>]
---
# Radiobutton

* A radiobutton widget lets you choose between one of several .red[mutually exclusive] choices. 


* Radiobuttons are always .red[used together in a set], where multiple radiobutton widgets are tied to a single choice or preference. 
   * They are appropriate to use when the number of options is relatively small, e.g., 3-5.


.font-15[
```python3
language = StringVar()
english = ttk.Radiobutton(parent, text='English', variable=language, value='english')
french = ttk.Radiobutton(parent, text='French', variable=language, value='french')
german = ttk.Radiobutton(parent, text='German', variable=language, value='german')
```
]

.center[<img src="https://tkdocs.com/images/w_radiobutton_all.png" height=150/>]

---
# Radiobutton

* Radiobuttons share most of the same configuration options as checkbuttons. 


* One exception is that the `onvalue` and `offvalue` options are replaced with a single `value` option. 
   * Each radiobutton in the set will have the .red[same linked variable], but a .purple[different value]. 
   * When the variable holds the matching value, that radiobutton will visually indicate it is selected. 
   * If it doesn't match, the radiobutton will be unselected.


.center[<img src="https://tkdocs.com/images/w_radiobutton_all.png" height=150/>]


---
# Entry

* An entry widget presents users with a .red[single line text field] where they can type in a string value.

.font-15[
```python3
username = StringVar()
name = ttk.Entry(parent, textvariable=username)

print('current value is %s' % name.get())
name.delete(0,'end')          # delete between two indices, 0-based. 'end':last index
name.insert(0,'your name')    # insert new text at a given index
```
]

* Entries can be used for passwords:

```python3
passwd = ttk.Entry(parent, textvariable=password, show="*")
```

.center[<img src="https://tkdocs.com/images/w_entry_all.png" height=150/>]

---
# Entry - input validation

*  To restrict what a user can type into the entry, you use .red[validation]. 

.font-15[
```python3
import re
def check_num(newval):
    return re.match('^[0-9]*$', newval) is not None and len(newval) <= 5

check_num_wrapper = (root.register(check_num), '%P')

num = StringVar()
e = ttk.Entry(root, textvariable=num, validate='key', validatecommand=check_num_wrapper)
e.grid(column=0, row=0, sticky='we')
```
]

* `validate` option: specifies when the callback function will be called for validation. 
   * The .red['key'] value -> validation occurs whenever any .red[keystroke] changes the widget’s contents.


* The `register` method (which can be called on any widget, not just root) creates a .red[Tcl procedure] which will call our Python function. 
   * The percent substitutions (e.g., `%P`) we've chosen will be passed to it as parameters. (`%P`: The value of the entry)
   * https://www.tcl.tk/man/tcl8.4/TkCmd/entry.htm#M25

---
# Combobox

* A combobox widget combines an `entry` with a list of choices. 
   * This lets users either choose from a set of values you've provided (e.g., typical settings), 
   * but also put in their own value (e.g., for less common cases) using `entry`.

.font-15[
```python3
countryvar = StringVar()
country = ttk.Combobox(parent, textvariable=countryvar)
country['values'] = ('USA', 'Canada', 'Australia')
country.state(["readonly"]) # restrict users to making choices only from the list of predefined values
```
]

* A combobox will generate a `<<ComboboxSelected>>` virtual event that you can bind to whenever its value changes. 

.font-15[
```python3
country.bind('<<ComboboxSelected>>', function)
selIndex = country.current() # return a 0-based index of the selected value
```
]

---
# Geometry Manager

* Geometry managers are used to specify the relative positioning of widgets within their container - their mutual master.
   * The size of any master widget is determined by the size of the “slave widgets” inside. 


* Available Geometry Managers:
   * `grid`: mix of power, flexibility, and ease of use
   * `pack`: quite powerful, but harder to use and understand
   * `places`: gives you complete control of positioning each element
   

---
# The Packer: `pack` method

* The packer is used to control where slave widgets appear inside the master into which they are packed.
   * `pack` makes a widget .red[visible] when the main window is displayed
   * widgets do not appear until they have had their geometry specified with a geometry manager.
   * `pack` should be called for .red[each widget] in a window


* `pack` receives an argument to specify positioning
   * Positioning depends on the order in which widgets were added to the window
   * Valid arguments: `side='top'`, `side='bottom'`, `side='left'`, `side='right'`

---
# pack - Example

.font-14[
```python3
import tkinter as tk

class Application(tk.Frame):
    def __init__(self, master=None):
        super().__init__(master)
        self.master = master
        self.pack()
        self.create_widgets()

    def create_widgets(self):
        self.hi_there = tk.Button(self)
        self.hi_there["text"] = "Hello World\n(click me)"
        self.hi_there["command"] = self.say_hi
        self.hi_there.pack(side="top")

        self.quit = tk.Button(self, text="QUIT", fg="red",
                              command=self.master.destroy)
        self.quit.pack(side="bottom")

    def say_hi(self):
        print("hi there, everyone!")

root = tk.Tk()
app = Application(master=root)
app.mainloop()
```
]

---
# `grid` Geometry Manager

* `grid` lets you layout widgets in .red[columns] and .red[rows]

* width of each column and height of each row will vary depending on the width/height of widegets contained within the colum/row

.row[
.col-6[
<img src="https://tkdocs.com/images/calcsketch.png" height=170/>
]
.col-6[
<img src="https://tkdocs.com/images/calcgrid.png" height=170/>
]
]

---
# grid - Example

.row[
.col-9.font-10[
```python3
from tkinter import *
from tkinter import ttk

def calculate(*args):
    try:
        value = float(feet.get())
        meters.set(int(0.3048 * value * 10000.0 + 0.5)/10000.0)
    except ValueError:
        pass

root = Tk()
root.title("Feet to Meters")

mainframe = ttk.Frame(root, padding="3 3 12 12")
mainframe.grid(column=0, row=0, sticky=(N, W, E, S))
root.columnconfigure(0, weight=1)
root.rowconfigure(0, weight=1)

feet = StringVar()
feet_entry = ttk.Entry(mainframe, width=7, textvariable=feet)
feet_entry.grid(column=2, row=1, sticky=(W, E))

meters = StringVar()
ttk.Label(mainframe, textvariable=meters).grid(column=2, row=2, sticky=(W, E))

ttk.Button(mainframe, text="Calculate", command=calculate).grid(column=3, row=3, sticky=W)

ttk.Label(mainframe, text="feet").grid(column=3, row=1, sticky=W)
ttk.Label(mainframe, text="is equivalent to").grid(column=1, row=2, sticky=E)
ttk.Label(mainframe, text="meters").grid(column=3, row=2, sticky=W)

for child in mainframe.winfo_children(): 
    child.grid_configure(padx=5, pady=5)

feet_entry.focus()
root.bind("<Return>", calculate)

root.mainloop()
```
]
.col-3[
<img src="https://tkdocs.com/images/calcgrid.png" height=100/>

<img src="https://tkdocs.com/images/f2m_all.png" height=150/>
]
]

---
# Step-by-Step Walkthrough

* setting up the main application window 

.font-15[
```python3
root = Tk()
root.title("Feet to Meters")
```
]

* creating a content frame

.font-15[
```python3
mainframe = ttk.Frame(root, padding="3 3 12 12")
mainframe.grid(column=0, row=0, sticky=(N, W, E, S))
root.columnconfigure(0, weight=1)
root.rowconfigure(0, weight=1)	
```
]

* creating the cntry widget

.font-15[
```python3
feet = StringVar()
feet_entry = ttk.Entry(mainframe, width=7, textvariable=feet)
feet_entry.grid(column=2, row=1, sticky=(W, E))
```
]


---
# Step-by-Step Walkthrough

* creating the remaining widgets  

.font-15[
```python3
meters = StringVar()
ttk.Label(mainframe, textvariable=meters).grid(column=2, row=2, sticky=(W, E))

ttk.Button(mainframe, text="Calculate", command=calculate).grid(column=3, row=3, sticky=W)

ttk.Label(mainframe, text="feet").grid(column=3, row=1, sticky=W)
ttk.Label(mainframe, text="is equivalent to").grid(column=1, row=2, sticky=E)
ttk.Label(mainframe, text="meters").grid(column=3, row=2, sticky=W)
```
]

* adding some polish

.font-15[
```python3
for child in mainframe.winfo_children(): 
    child.grid_configure(padx=5, pady=5)
feet_entry.focus()
root.bind("<Return>", calculate)
```
]

* start the event loop

.font-15[
```python3
root.mainloop()
```
]

---
# `tkinter` Widgets

* The `tkinter.ttk` module provides access to the .red[Tk themed widget set], introduced in Tk 8.5.


* Using the `Ttk` widgets gives the application an improved look and feel.


* `Ttk` comes with 18 widgets (all of them are subclasses of `Widget`), 
   * twelve of which already existed in `tkinter`: 
      * `Button`, `Checkbutton`, `Entry`, `Frame`, `Label`, `LabelFrame`, `Menubutton`, `PanedWindow`, `Radiobutton`, `Scale`, `Scrollbar`, and `Spinbox`. 
   * The other six are new: 
      * `Combobox`, `Notebook`, `Progressbar`, `Separator`, `Sizegrip` and `Treeview`. 


```python3
from tkinter import *
from tkinter.ttk import *
```

* This `import` code causes several `tkinter.ttk` widgets to automatically replace the `Tk` widgets.

---
# `tkinter` Widgets

.row[
.col-6[

* Listbox
<img src="https://tkdocs.com/images/w_listbox_all.png" width=300/>

* Scrollbar
<img src="https://tkdocs.com/images/w_scrollbar_all.png" width=300/>

* Text
<img src="https://tkdocs.com/images/w_text_all.png" width=300/>

]
.col-6[

* Scale
<img src="https://tkdocs.com/images/w_scale_all.png" width=300/>

* Spinbox
<img src="https://tkdocs.com/images/w_spinbox_all.png" width=300/>

* Progressbar
<img src="https://tkdocs.com/images/w_progressbar_all.png" width=300/>
]
]

* Menu, Treeview, Canvas, etc.

---
# Event Handling

* Event Loop

.center[<img src="https://tkdocs.com/images/eventloop.png" width=500/>]

---
# Binding an Event Handler

.font-14[
```python3
widget.bind(event, eventHandler)  # eventHandler: called "event handler" or "callback function"
```
]

.font-12[
```python3
import tkinter as tk
import sys

class Application(tk.Frame):
    def __init__(self, master=None):
        super().__init__(master)
        self.master = master
        self.pack()
        self.create_widgets()

    def create_widgets(self):
        self.hi_there = tk.Button(self)
        self.hi_there["text"] = "Hello World\n(click or double click me)"
        self.hi_there.bind('<Button-1>', self.say_hi)
        self.hi_there.bind('<Double-1>', self.say_bye)
        self.hi_there.pack(side="top")
        
    def say_hi(self, event):
        print("hi there, everyone!")
   
    def say_bye(self, event):
        print("good bye, everyone!")
        sys.exit()

root = tk.Tk()
app = Application(master=root)
app.mainloop()
```
]

---
# Event Types and Event Field

```python3
self.hi_there.bind('<Button-1>', self.say_hi)
...
def say_hi(self, event):
   print("hi there, everyone!", event.x, event.y)
```

https://www.python-course.eu/tkinter_events_binds.php

```
Tk      Tkinter Event Field             Tk      Tkinter Event Field 
--      -------------------             --      -------------------
%f      focus                           %A      char
%h      height                          %E      send_event
%k      keycode                         %K      keysym
%s      state                           %N      keysym_num
%t      time                            %T      type
%w      width                           %W      widget
%x      x                               %X      x_root
%y      y                               %Y      y_root
```

---
# Acknowledgement

* https://tkdocs.com/tutorial/index.html (most examples are from this site)
* https://docs.python.org/3/library/tk.html
* https://coderslegacy.com/python/python-gui/
* https://www.python-course.eu/python_tkinter.php