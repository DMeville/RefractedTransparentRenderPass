1) Create a new layer "AfterTransparent"
2) (on Forward Renderer Data object) Set OpaqueLayerMaks and TransparentLayermask to IGNORE this new "AfterTransparent" layer (we don't want to render this layer in the normal pass, only our custom pass we're about to set up!)
3) Add "GrabScreenFeature" to your renderer render features (on Forward Renderer Data object)
4) Name this "AfterTransparent", and ensure in the Settings the texture name is set to "_GrabPassTransparent". Change the layermask to ONLY the new "AfterTransparent" layer we created in step 1

Render feature is now set up properly, and any objects set to be in the "AfterTransparent" render layer will use this custom pass, and have access to a custom "_GrabPassTransparent" texture in their material.  We can see this by creating a new shader that samples this texture.

Next: Create a new shader (or use the included "GlassRefraction" shader, made in ASE so you can open to see nodes), assign it to a new material and object, and place it so you can see other transparent object/particles THROUGH this object. They will show up! Huzzah! Now you can see particles through glass and stuff. Welcome to the future.


- Sample the global texture _GrabPassTransparent in shader with screen uvs 
- The object with this grabpass shader on it, must render to it's own layer ("AfterTransparent")
- The forwardRenderer settings OpaqueLayerMask and TransparentLayermask must ignore this layer, otherwise we get a feedback loop in the Grabpass (and it breaks)
- The layermask on the render feature must be set to ONLY this layer "AfterTransparent.

For correct particle sorting.
- Create an extra layer "Particles".  
- Enable this on Opaque and Transparent layer masks on the Forrward Renderer Filtering
- Enable this on the render feature layer mask. (this allows the particles to correctly sort ONTOP of the custom refraction pass too, at the cost of rendering the particles twice)

Youtube video explaining and showing how to set this up: https://youtu.be/tyyn6NhH-MQ
