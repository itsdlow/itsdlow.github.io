---
collection: portfolio
title: "Game Engine"
excerpt: "A custom game engine implementation<br/><img src='/images/game-engine-thumbnail.png'>"
---



---

### Contents

- [Run-time Resources](#run-time-resources)
- [Animation](#animation)
- [Rendering](#rendering)
- [Multiple Camera Support](#multiple-camera-support)
- [Shaders](#shaders)
- [Camera Frustum Culling](#camera-frustum-culling)
- [Scene Support](#scene-support)



#### Run-time Resources

​	In order to standardize resource loading within the engine, all resources pertaining to models, textures and fonts must go through a conversion tool. The conversion tool takes in the various types of resources and serializes their data using [Google protocol buffers](https://developers.google.com/protocol-buffers/). The Google protocol buffer's are then used during engine runtime for the deserialization of resources, into the engines run-time formats.



​	This custom converter tool provides a command-line interface to enable conversion of models, fonts and textures. For models, the tool accepts gLTF models (.gltf or .glb). For textures it accepts image files of TGA or PNG. And for fonts it accepts a XML and image file describing the font. 



#### Animation

​	Animation is an important feature of any game engine system. However it requires very costly operations. Fortunately, the type of work required for animating models is perfect for the multi-core architecture of GPUs. 	

​	In order to enable animation of 3D models, the concept of vertex skinning is introduced, where vertices of a mesh are influenced by the bones of a skeleton. For each keyframe of an animation, each bone is able to be interpolated (LERP)/spherically interpolated (SLERP) independently from one another.  This calculation must be performed on a per bone-basis for each frame. Offloading this to the GPU provides major gains in terms of freeing up time for the CPU.

##### GPU Responsibilities

- LERP/SLERP between keyframes per bone per clip
- LERP/SLERP blending between two different clips
- Local space bone matrix calculation
- Bone weight blending per vertex
- Local space to world space transformation



#### Rendering

- ##### 2D Rendering

  - The engine supports the ability to render 2D sprites, which entails the ability to print UI graphics and dynamic/static text.

- ##### 3D Rendering

  - The engine also supports the ability to render 3D meshes.



#### Multiple Camera Support

The ability to switch between different cameras is supported. Along with multi-cam support are two different types of cameras: Perspective and Orthogonal. 

In addition to supporting multiple cameras, the engine also provides an interface to have multiple active cameras render to a screen, enabling features such as a HUD or rear-view camera display.



#### Shaders

- ##### Vertex & Fragment Shaders

  - The game engine includes multiple types of shaders, already built-in. Each shader can easily be toggled between filled and wireframes modes. The included shaders that support lighting use Phong-based shading.

- ##### Compute Shaders

  - The engine supports the ability to load and use compute shaders. The compute shader interface is wrapped into a easier to use interface for both dispatching and reading/writing buffers.



#### Camera Frustum Culling

The engine also supports camera frustum culling based on the active camera(s). While the GPU has its own early abort within the rendering pipeline, we can optimize this even further by avoiding the request to draw of the mesh. Support for camera culling is available if toggled on. Using a frustum collision check with the mesh's bounding sphere, we can decide if the mesh would be visible in the frame. If the bounding sphere is visible in the frame, we must request the draw. If the sphere isn't within the frustum, we don't try to draw the model. Note: For this feature to work, all transformations must be uniform scaling.



#### Scene Support

The engine supports the ability to create and switch between different scenes. Scenes contain their own instance data, allowing for more optimized and separated game logic. Resource managers, such as those that manage Textures, Models, and Shaders, are shared between all scenes in order to reduce redundancy and lower memory footprint.

