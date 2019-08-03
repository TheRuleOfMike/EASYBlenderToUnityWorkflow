# EASYBlenderToUnityWorkflow
Contents of this file:
1. From the description on dlendswap.
2. Full file list.
3. Example easic eorkflow.
4. Detail eask editing workflow.




1. FROM THE DESCRIPTION ON BLENDSWAP:

WARNING: The files are only compatible with Blender 2.8. Baking is (currently) possible only using Cycles. To view the intended effect use Eevee.

ABOUT:

I found myself in the need of simplifying the process of creating assets for the Unity Standard shader.

I've created a specific node-setup that emulates the shader and allows for easy baking by simply connecting a specific node group output and baking the diffuse color. The node group can also work as a preview for the Unity export - the functionality is nicely emulated (including detail maps).

Just create your model as you would normally do just use the node group for the materials on the high-poly mesh (duplicate the StartMaterial). View the "ExampleMaterial" on the "ExampleObjectsWithAtlas" for an easy introduction. Use the BakeMaterial on the low-poly mesh (the attached bake texture is 2048x2048).

Two blend files are attached:
UnityRoughnessSetupBlenderStartFile.blend
UnitySmoothnessSetupBlenderStartFile.blend

Thanks to the node group you can bake Albedo, Metallic, Roughness/Smoothness, Emission, Alpha Transparency, a Detail Mask and a Detail Mask with the Alpha channel of the Detail Albedo baked in to the mask. And obviously you can bake the Normal Map and Ambient Occlusion as usual.

What you CAN'T bake and preview is the Height Map due to the lack of this functionality in Cycles and Blender 2.8 overall. This function allegedly will come soon, and if it will I will implement this in a future version of the files.

I attach a variety of example baked textures - both for the ExampleMaterial and for the Unity export - and an fbx file to experiment with in Unity.

A file explaining the workflow in a little more detail is also attached.

I work with those files myself when developing for the Unity Standard shader. The Metallic workflow is however universal so if you are working with different engines like Unreal or Godot, this file can also be quite useful for you.

The Blend files come with two HDRI environments. Both files are CC0 and originate on the wonderful hdriheaven.com (I know I didn't need to attribute, but that's just an awesome site).

Contact me if you have any questions.
Follow me on:
Twitter: @TheRuleOfMike
Instagram: theruleofmike
Artstation: theruleofmike
DeviantArt: theruleofmike

More useful stuff and quite a lot of art coming soon.

Yours truly,
Michał Klekowicki


2. FULL FILE LIST

Main folder:

UnityRoughnessSetupBlenderStartFile.blend – the Blend file for the Roughness setup of the Unity Standard shader. The colorspace is set to sRGB instead of Filmic to emulate typical Unity visuals. There is a default ExampleObjectWithAtlas mesh and which you can clearly see what’s going on.

UnitySmoothnessSetupBlenderStartFile.blend – the Blend file for the Smoothness setup of the Unity Standard shader. The colorspace is set to sRGB instead of filmic to emulate typical Unity visuals. There is a default ExampleObjectWithAtlas mesh and which you can clearly see what’s going on.

UnityExampleModel.fbx – fbs export of the example model

Example_Maps_Collection:

ExampleMaterial_Albedo.png

ExampleMaterial_DetailAlbedo.png

ExampleMaterial_DetailAlbedoAlt.png

ExampleMaterial_DetailMask.jpg

ExampleMaterial_DetailMask.png

ExampleMaterial_DetailNormal.png

ExampleMaterial_DetailNormalAlt.png

ExampleMaterial_Emission.jpg

ExampleMaterial_Metallic(R)Roughness(G)AO(B).png – the composite map with Metallic, Roughness, and Occlusion packed in to color each channel - use GIMP or other similar software to split the channels to view/edit the maps individually.

ExampleMaterial_Metallic(R)Smoothness(G)AO(B).png -  the composite map with Metallic, Smoothness, and Occlusion packed in to color each channel - use GIMP or other similar software to split the channels to view/edit the maps individually.

ExampleMaterial_NormalMap(sRGB_ColorSpace).png

Exported_To_Unity:

(The files were downscaled to 1024x1024 – except for the detail mask - to save space in the zip file)

ExampleMaterial_Albedo.jpg

ExampleMaterial_AO.jpg

ExampleMaterial_DetailAlbedoAlt.jpg

ExampleMaterial_DetailMask.png

ExampleMaterial_DetailNormalAlt.jpg

ExampleMaterial_Emission.jpg

ExampleMaterial_Metallic.jpg

ExampleMaterial_NormalMap(sRGB_ColorSpace).png

ExampleMaterial_Roughness.jpg

ExampleMaterial_Smoothness.jpg


3. EXAMPLE BASIC WORKFLOW:

1. Create your high-poly mesh as you normally do.

2. When you assign materials to the separate elements or parts of the mesh, be sure to use duplicates of the StartMaterial. If you wan’t to create more complex single materials, be sure to ALWAYS use the node group as shader nodes when you are mixing.

3. When baking, attach the desired node group output to the Material Output. Be sure to this in every material of the high poly mesh. If somewhere you used the mix shader node to create a more complex material, attach the desired group outputs to the mix node inputs. Be sure to do this to every instance of the group.

4. Use the BakeMaterial for the low poly mesh. Set up a cage etc.

5. Bake the desired map using Cycles. Choose Diffuse and un-select Direct and Indirect lighting. Be sure to bake only color (in the files this is set up as a default state, so if you are using them unchanged just bake “as is”). You can bake Albedo, Metallic, and Roughness using the “Basic 3” option (Albedo will be baked on the Diffuse Color, Metallic on Glossy Color, and Roughness on Emission).

6. Bake the Normal Map and Occlusion Map using Cycles. Choose Normal or Ambient Occlusion in the baker.

7. Voila. Rinse and repeat.


4. DETAIL MASK EDITING WORKFLOW:

Thanks to the node group you can also easily paint detail maps (as you would normally paint a texture – just choose the Detail Map slot while painting) BUT you can also modify it with the alpha of the detail mask (as Unity doesn’t support Detail Albedo alpha out-of-the-box, this can be VERY useful).

1. Attach Detail Mask to the group.

2. Attach the Detail Albedo with an Alpha channel.

3. Set up tiling and scaling s you wish using the mapping nodes.

4. Attach the BakeDetailMask(DetailAlbedoAlphaApplied) to the Material Output.

5. Bake using the Diffuse (un-select Direct and Indirect lighting. Be sure to bake only color – in the files this is set up as a default state, so if you are using them unchanged just bake “as is”).
