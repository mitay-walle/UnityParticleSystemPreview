# Unity ParticleSystem Prefab Preview
Forked from: https://github.com/akof1314/UnityParticleSystemPreview
changes:
- converted to UPM package
- Auto play saved between select different prefabs 
## reason
After using Unity to complete the particle effect prefab, save it to the unified effect directory of the project. When you need to use it, select the corresponding particle effect prefab. When there are more and more special effects prefabs, it will become more and more difficult to tell which one is really needed, and Unity does not provide the function of previewing resources like AnimationClip, which can only be dragged into the scene one by one. Going to preview playback is very time-consuming and laborious.

## Target
Implements the ability to preview particles directly in the inspector like model motion animations.

![](http://img.blog.csdn.net/20161031204154560)

## solve
The final effect of the particle effect preview is similar to the model action animation preview. First, replace the FBX model with particle objects, and then realize that it can be played in the preview window.

![](http://img.blog.csdn.net/20161031204228633)

First realize the three-dimensional space in the preview window, use the editor class PreviewRenderUtility, which creates a hidden camera, set the cullingMask to only the specific Layer layer to be rendered, render it into the target texture, and then draw the texture into the preview window. Next, create the objects to be rendered. Lattice flat floor, directional arrows, and particle effect objects.

![](http://img.blog.csdn.net/20161031204254884)

Finally, the preview playback of particles is realized. There are two ways to simulate playback of particles in edit mode. One is to directly call the Simulate method. The playback effect may be different from the actual playback effect. The other is to call the locked particle, and then call the Play method, the effect will be the same as the actual playback effect, because Unity will perform real calculations on the locked particle object internally. The second method is used here. The method of locking particles is not open, so the ParticleSystemEditorUtils.lockedParticleSystem method has to be reflected.

![](http://img.blog.csdn.net/20161031204322640)

For the particle effect root node with Mesh, the original Mesh preview window cannot be displayed, so add a button to the toolbar to switch.

![](http://img.blog.csdn.net/20161031204347181)

![](http://img.blog.csdn.net/20161031204357266)

The button PS (Show particle system preview) can switch between the original preview window and the particle effect preview window.

## Conclusion
The Unity editor provides flexible extension methods, but many of them are undocumented. It is necessary to study how it is used to facilitate porting and extension. The simulation playback method of particle effects, if you want the particles to be playable without selecting the particle object, then the only way is to lock the particles.

## source code
AssetStore address: https://www.assetstore.unity3d.com/cn/#!/content/73346
