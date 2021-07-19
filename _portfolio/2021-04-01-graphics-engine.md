---
collection: portfolio
title: "Render Engine"
excerpt: "An application making use of DirectX11 graphics library<br/><img src='/images/graphics-thumbnail_500x300.PNG'>"
video_title: "Mirror Demo"
video_url: "https://www.youtube.com/embed/HVUtgnfE7-c"

---
DirectX is a low-level graphics API. This application provides a graphics API abstraction on top of Windows DirectX11 graphics API.

This software is incomplete, but is intended to be a render engine that provides an easier to use graphics API to interact with DirectX and the GPU, providing an abstraction which hides the repetitive minutiae of graphics programming.

## The Experience

This project was the result of 20+ hours per week of work in a 10 week rendering/graphics programming course at DePaul University. As it was for a graphics introduction class, we only discussed the most basic techniques and as such there is much room for improvement, including to it's architecture. This project required me to be both the architect and the artist, which was a new, beneficial, and challenging experience. In addition to the project, this course taught me about the complexity and stages of the graphics rendering pipeline, focusing on 5 of the DirectX rendering stages: Input-Assembler, Vertex-Shader, Raterizer, Pixel-Shader, and the Output-Merger stage. All-in-all, through this course, I have established a foundation in graphics progamming, and realized how intricate the graphics rendering process is, meritting sophisticated and well-designed graphics support.

### Result
- I learned an incredible amount through this course, but, despite that, I am far from happy with the end result that is my final project. The final project was simply to make a scene which demos all of the elements covered through the course, making use of our new graphics API. I created a simple scene inspired by Gotham city, but it is riddled with artifacts of my struggles with the art aspect of this project (i.e. procuring viable models).
<br/><br/><img src='/images/graphics-thumbnail.PNG'>

## The Architecture

### Resource Management
- To manage the many resources used for graphics programming (Textures, Shaders, Models), I make use of the Singleton design pattern to provide encapsulated, global access to these resources. This design helps to streamline the process of creating Graphic Objects, which are not cleanly managed by a resource-managing object in this iteration.

### Graphic Object
- The other core component behind the graphics API abstraction is the Graphic Object. This essentially packages 1) a mode, 2) its associated shader, and 3) how to properly send the relevant data to that shader. By encapsulating these components into a single object, the rendering process becomes much more streamlined.

## Features

### Effects
- I have created numerous shaders, both textured and colored, which can apply simple lighting and fog effects. Throughout the course we learned of a few basic techniques which can be applied to add effects to a scene. These include light effects through the use of the Phong Illumination model implemented in the pixel shader. As well as the concepts of blending and stenciling, through the use of very simple use-cases of rendering fog, transparency, and reflection/mirroring effects.

### Models
- I created numerous premade models including: unit cube, unit pyramid, unit sphere, flatplane, skybox, as well as a terrain model which can be supplied a heightmap texture. In addition, the render engine supports importing models that contain more than one mesh using the engine's mesh seperator, each of which can have their own material/color/texture. 

{% if page.video_title and page.video_url %}
	{% include {{ page.video_include }} url=page.video_url title=page.video_title %}
{% endif %}