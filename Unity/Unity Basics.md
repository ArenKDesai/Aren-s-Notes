#Unity #Graphics 

From Jasper Flick's Unity Tutorial series. 

Objects in Unity can have many fields, but some, such as basic cylinders, contain three default fields:
1. Mesh filters, which contain a reference to built-in mesh defining the object. 
2. Mesh renderers, which ensure the mesh gets rendered, and determines what material the object gets rendered as. 
3. Capsule collider, for 3D physics. Unity doesn't have a primitive cylinder collider, so it uses a capsule collider for a cylinder. However, for more advanced physics, mesh colliders may be better. 

You can drag objects into a hierarchy that combines them into one group object, where rotating or shifting the object will translate all of them. Order in the hierarchy doesn't matter. 

