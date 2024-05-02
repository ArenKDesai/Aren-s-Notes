#Linking #Loading #CS354 #Relocation #UWMadison

## Symbol Table
Size is minimum size
Alignment - relative offset if initialized (not COM), otherwise in .bss

## Relocation
[[Memory Hierarchy]]
Needs relocation
- global variables
- external global variables
- anything "extern"
- global functions (uninitialized)
Doesn't
- static global function
- anything static (can be relative)