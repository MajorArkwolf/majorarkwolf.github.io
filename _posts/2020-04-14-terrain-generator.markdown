---
layout: post
title:  "Terrain Generator"
date:   2020-04-14 12:00:00 +0800
categories: University
image: /assets/img/terraingenerator.png
slideShow: 
- /assets/img/terrain/1.png
- /assets/img/terrain/2.png
- /assets/img/terrain/3.png
- /assets/img/terrain/4.png
- /assets/img/terrain/5.png
- /assets/img/terrain/8.png
- /assets/img/terrain/10.png
- /assets/img/terrain/11.png
- /assets/img/terrain/14.png
- /assets/img/terrain/15.png
- /assets/img/terrain/16.png
- /assets/img/terrain/17.png
- /assets/img/terrain/18.png
- /assets/img/terrain/19.png
- /assets/img/terrain/20.png
- /assets/img/terrain/21.png
- /assets/img/terrain/22.png
- /assets/img/terrain/23.png
---
## ICT397 University Project

Everything shown was produced by myself and with some assistance from 3rd party libraries such as GLM (Mathematics library).

I was tasked to produce a terrain generator for our ICT-397 Assignment. Due to issues in our past with fixed-pipeline OpenGL and being the only one in the group having experience with Modern OpenGL, it only made sense that I took on the task to produce something for our game engine. The renderer was also provided by myself in this demo and for the assignment. Above is a slider showing the progress, I will be referring to the images in that order on the problems I encountered and how I overcame them.

To begin with, I needed to generate a tile system that could produce a large enough mesh dynamically. It took a little longer, then I had initially thought since my first approach was to have a single square and then copy and paste X and Y amount of times until I had a mesh. While this method worked, it meant I had extra vertices because every overlapping square contained up to 2 – 4 vertices. There was one other issue, which was that when updating those vertices, I had to make sure to update all the vertices in that given region. At this point, I should have given up, but instead, I tried to make a function that would join vertices that shared cartesian coordinates. While I had a working solution by the end of this, I was disappointed in the performance and opted to generate single verticies instead and then a script that would join them. The final result can be seen in image 2. At this point, I also had toggleable wireframe implemented to allow me to debug any strange vertex problems.

Next, it was time to implement a Perlin noise loader and an alternative method called fracture terrain generation. The lecturer provided fracture generator; however, it was a C implementation and was extremely unsafe due to passing around raw pointers. I opted not to use this method since my implementation was using chunks, and the fracture method means that all chunks would need to be computed before the fracture method could run otherwise, each chunk would not attach. Instead, I developed a parameterized Terrain Factory that on startup could either generate a Perlin noise map or load one in to save on computational time. Image 3 and 4 show the Perlin noise map, and image 5 shows the fracture method. While the fracture method produces excellent terrain, it would not work in our implementation.

Next was chunk loading, and I wanted a way that could load chunks based on the camera location to not only reduce how much GPU rendering needed to be done, but also reduce the required initial load time as each chunk doesn’t take a significant amount of time to produce however 100 chunks does. As seen in image 6, only the chunks around the camera are drawn. The rest are not added to the draw queue.

Next was texture mapping based on altitude. I wanted to offload as much work from the CPU as possible, so this meant it needed to be done in the shaders. So my idea was simple and effective, take each height from the vertex shader, pass it into the fragment shader, then based on the Y coordinate, use the appropriate texture. You can see my first attempt in image 7 and 8. Since I was using if statements to determine the texture maps, it produce some horrible banding. So it was back to the drawing board. I instead opted for a percentage scale based on the height. This allowed for a smooth transition between texture heights. I ended up with two implementations, as seen in image 9 and 10. I opted for 9’s shader over 10’s as 10 produced too smooth of a transition. Finally, something that is not shown in the images. I coded a value for sand so that it would hard start around about the level of the water. This made our terrain feel a little more filled in then just grass, dirt, and snow.

Next was implementing water. I wanted a simple but effective method and opted for a set height level similar to how a water table might work in real life. So I generated the same mesh used in the terrain chunk and place it at a given height. I ran into some minor issues with shader conflicts. I discovered that shader variables share the global namespace, meaning I had to ensure that each shaders variables did not conflict with one another, as seen in image 11.

Now I needed some basic lighting as textures without any form of light produce this unpleasing aesthetic, and I didn’t want that in my final product. So I took the basic Phong lighting algorithm and implemented it into my terrain shader, as can be seen in image 12 and 13. This took several revisions and some extra work to get it to the point that I thought showed some sense of realism; however, I am thrilled with the final product image seen in image 17.

Next, it was time to add a skybox, the world felt a little dark and empty, so it was time to implement something to fill the void. Nothing to special here, load a cubemap in, switch the depth buffer so that it would draw the inside and not the outside. Give the shader the camera coordinates so it would always be relative to the camera and draw it last, so the poor Z’ed buffer didn’t have to fight it and boom, a vast open-world as seen in image 18.
