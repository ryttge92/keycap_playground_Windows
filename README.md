# keycap_playground for Windows
The Keycap Playground is a parametric OpenSCAD keycap generator made for generating keycaps of all shapes and sizes (and profiles)

This has been forked from the original Linux implementation and rewritten to work on Windows.

## Prerequisites

### Openscad

https://openscad.org/downloads.html#snapshots

You need the nightly, last stable is from 2021.01 and it's slow as molasses. 

### Multi-material keycaps

1. In OpenSCAD: Preferences -> Features, enable `lazy-union` (and `manifold` if it's listed; it's the default backend in newer snapshots).
2. In `keycap_playground.scad` set `WHAT_TO_RENDER = "multi-material"` (or `"multi-material row"` to render everything in `ROW`).
3. Render (F6) and export as `.3mf`. The file contains two objects: the keycap+stem and the legends (colors set by `MULTI_MATERIAL_BODY_COLOR` / `MULTI_MATERIAL_LEGEND_COLOR`).
4. In OrcaSlicer, answer "yes" when asked to load it as a single object with multiple parts, then assign a filament to each part.

### Python

https://www.python.org/downloads/windows/

#### Colorama

A python library, installed through pip

https://pypi.org/project/colorama/

`pip install colorama` 

## How to use

Open CMD in the script directory

`\keycap_playground\scripts`

To view all options run

`python gem_full.py`

To generate all keycaps defined in gem_full.py along with the .stl files for legends run

`python gem_full.py --legends --out generated`

This will place all .stl files in the directory

`\keycap_playground\scripts\generated`

## How it works

Basic rundown for the two main files relevant to the end user. 

### gem_full.py

Contains the definitions for all the keycaps to be generated.  
Use this file to define and generate a set of keycaps of your own. For a better understanding of how everything works i'd recommend you to start with playing around in keycap_playground.scad 

Heres an example line  
`gem_double_legends(name="quote", legends=["'", "", '\\u0022']),`

`gem_double_legends`  
Keycap class, changes within the class will be made to all keycaps within that class.  

`name="quote"`  
Name of the keycap

`legends=["'", "", '\\u0022'])`  
Defines the keycap legends, some legends like in this case " needs to be written with their unicode instead. 

https://www.babelstone.co.uk/Unicode/whatisit.html
Can be used to find what unicode is needed 


### keycap_playground.scad

The OpenSCAD library that does all the heavy lifting, can be run by itself to open "the playground"

A video by the original creator on how it works can be found here.

https://www.youtube.com/watch?v=WDlRZMvisA4&t=1s

## Known issues

#### Colorscad does not work.  
Not needed anymore, see *Multi-material keycaps* above.
https://github.com/jschobben/colorscad

It's a linux native application that should run fine with CYGWIN, might get around to fixing it. 


#### Backslash does not work

Backslash needs to be escaped with a backslash, CMD interprets \\\ as a UNC path which breaks the command line argument.  
Simple workaround is to use `keycap_playground.scad` to manually generate these. 