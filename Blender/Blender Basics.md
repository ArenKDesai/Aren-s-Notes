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
- Select next vertex or line - ctrl+'+'
- hide vertices - h
	- unhide - alt+h
- Create breakaway face - e
- Change influence on sculpting brush - shift+s
- select more - shift
- create parent/child - ctrl+p (select child first)
- fullscreen - ctrl+space
- zoom to object - numpad '.'
- zoom menu - '~'
- apply scale - ctrl+a

## Meshes

### Vertices and Edges
Entering edit mode on a mesh allows for vertex and edge selection. 
Proportional editing edits vertices and edges around the selected vertices as well. Scrolling up and down increases or decreases the circle of influence. 

X-Ray allows selection of vertices through a mesh instead of vertices facing the camera. 

Snapping allows meshes to align to something. Defaults to axis. 

## Modifiers

Note: order matters. 
### Subdivision "Subsurf" Modifier
Allows for the averaging of faces to generate more smooth surfaces. Increasing the Render value in Catmull-Clark increases the number of faces generated after a render, but doesn't generate those renders during an edit. 

### Solidifier
Changes the volume, or thickness of a mesh. May need to toggle viewing edges in edit mode. 
Increasing the "Crease Inner" smoothes the crease between the mesh and the face. 

### Shrinkwrap
Snaps all vertices from one mesh to another. Useful for layers. 

### Geometry Nodes

## Modes

### Edit Mode
Allows for minute control of edges and vertices on meshes. 

### Object Mode
Allows for the creation, deletion, and selection of full meshes. 

### Sculpt Mode
Brushes can modify meshes in various ways, such as enlarging details. 

### Isolate Mode
Can be accessed with forward slash. Isolates one mesh. 