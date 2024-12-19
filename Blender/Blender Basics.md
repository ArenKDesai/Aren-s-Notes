#Graphics #Blender

## Controls
- Add an object - shift+a
- Move selected object - g. Left click to confirm, right click to cancel. 
	- Holding down middle mouse button allows to select a specific axis
- Render image - F12
- Look through camera - numpad 0 (or clicking icon w/o numpad)
	- properties -> "Camera to View" to move camera with middle mouse hold
- Properties view - n
- Orbit camera - middle mouse hold + move mouse
- Scale object - s
	- hit x,y,z to scale on axis
- Rotate object - r
	- x,y,z to rotate on axis
- Add subdivision surface modifier - ctrl+1
- Change between modes on a mesh - tab
- Select a whole line (extended edge) - alt+click

## Meshes

### Vertices and Edges
Entering edit mode on a mesh allows for vertex and edge selection. 
Proportional editing edits vertices and edges around the selected vertices as well. Scrolling up and down increases or decreases the circle of influence. 

## Modifiers

### Subdivision "Subsurf" Modifier
Allows for the averaging of faces to generate more smooth surfaces. Increasing the Render value in Catmull-Clark increases the number of faces generated after a render, but doesn't generate those renders during an edit. 