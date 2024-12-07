#Unity #Graphics #CSharp

Classes defined with the Unity C# library need to extend a certain behavior class. For example, monospace:

```C#
public class Clock : UnityEngine.MonoBehaviour {
	// init here
}
```

## Classes
### Behaviors
- [MonoBehavior](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html): Offers life cycle functions, basic component of a GameObject. 

### Actions
- [Transform](https://docs.unity3d.com/ScriptReference/Transform.html): Objects have a Transform child object, which can be modified to modify the object. 

### Fields
- SerializeField: Used to make an object public, such as a Transform object. 

## Shaders
You can either use the shader creator to define a shader, or you can make your own shader with the