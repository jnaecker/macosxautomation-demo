# AppleScript Demo

## Intro

Everything on the Mac is an object.

## Opening and Closing

```
tell application "Finder" to open the startup disk
```

```
tell application "Finder" to close every window
```


## Properties and Values

All objects have properties that can be read or manipulated, eg size, position, name.

Use the verb `get` to retrieve properties of objects:   

```
tell application "Finder" to get the name of the front Finder window
```

Note that some properties (including the name of a Finder window) are read-only.

### The `index` property

All windows of an application exist in stacks. No two windows can occupy thte same layer in the stack, so index is a good way to refer to specific windows.

Can refer to indexes in several English-like descriptive ways:
```
tell application "Finder" to get the name of Finder window 1
```
or 
```
tell application "Finder" to get the name of the first Finder window
```
or even
```
tell application "Finder" to get the name of the 1st Finder window
```

Can also refer to windows by relative position:
```
tell application "Finder" to get the index of the front Finder window
```

Other adjectives include `back`, `last`, and `middle`.

Can even access window properties relative to others using `before` and `after`:
```
tell application "Finder" to get the index of the Finder window before the last Finder window
```

### Setting a property's value

Set a value with the verb `set`:

```
tell application "Finder" to set the index of the back Finder window to 1
```

Note this changes the index value of other windows too!

### The `target` property

The `target` property refers to the folder or disk displayed by the referenced Finder window.

```
tell application "Finder" to get the target of the front window
```

The target property can be set, which will change the contents of the Finder window:

```
tell application "Finder" to set the target of the front Finder window to the startup disk
```

If you want to refer to a particular folder, use a chain of `of`:

```
tell application "Finder" to set the target of the front Finder window to the folder "Learning" of the folder "Dropbox" of home
```

### Other Finder window properties

- `toolbar visible`: boolean
- `statusbar visible`: boolean
- `sidebar width`: integer
- `current view`: list view, column view, flow view, icon view

Note you can set one property to have the same value as another property:

```
tell application "Finder" to set the sidebar width of the first Finder window to the sidebar width of the second Finder window
```

### The `position` property

The `position` property refers to the location of the top left corner relative to the top left corner of the screen.  

#### Finder vertical offset exception

Note than finder is unique in that its position actually refers to just below the title bar and toolbar, which have a combined height 45 pixels.

### The `bounds` property

The property `bounds` refers to the top left and bottom right corners of the window.  So `{top left horizontal, top left vertical, bottom right horizontal, bottom right vertical}`

Alternatively, think of the first to arguments as position and the second two as position plus width and length.

Can get your desktop dimensions like so:

```
tell application "Finder" to get the bounds of the window of the desktop
```

### Other verbs:

- `get`
- `set`
- `open`: cause a window to display
- `close`: close a window
- `selelct`: cause a window to come to the front

## Tell Blocks

Instead of writing many tell statements, put them in a tell block:

```
tell application "Finder"
    ...
end tell
```

Tell blocks can also be nested to futher economize on typing references:

```
tell application "Finder"
    close every window
    open home
    tell the front Finder window
        ...
    end tell
    open folder "Dropbox" of home
    tell the front Finder window
        ...
    end tell
end tell
```

## Running Scripts

If you want to run a script from a keyboard shortcut:

- Open automator and make a new service. Drag in "Applescript" and paste in your script. Save it with a descriptive name.
- Open System Preferences > Keyboard > Shortcuts.  Scroll down until you see your new service. Give it your preferred shortcut.
- Open System Preferences > Security and Privacy > Accessibility.  Make sure "Automator" is allowed access.

Note: if your keyboard shortcut conflicts with one for the app that is currently active, your script will not run.


## References

- [Mac OS X Automation Training](http://macosxautomation.com/training/applescript/index.html)
- [Assigning shortcut](https://apple.stackexchange.com/questions/175215/how-do-i-assign-a-keyboard-shortcut-to-an-applescript-i-wrote)