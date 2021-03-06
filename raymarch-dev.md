Raymarching Distance Fields Development Description
============================================

Contents
--------
*	The raymarching algorithm
*	Orthographic scene
*	Transformations and perspective
*	Shading
*	Displaying the results
*	Resources

The raymarching algorithm
-------------------------
The raymarching algorithm being used is inspired by the work of Inigo Quilez in the demoscene.
The algorithm can be formulated as such:

###Problem:###
For each pixel in the result image, we wish to cast a ray into the world and find the closest surface intersection.

###Solution:###
Instead of analytically solving the ray intersection problem, we look for an approximation.
First, we define our scene using distance functions that, for any given point in the world, return the
closest distance from the point to a surface.

For example, the (signed) distance function for a sphere centered at the origin would be:
```c
float sdSphere(vec3 p, float radius) {
	return length(p) - radius;
}
```
The distance function for the composed scene will then be the minimum of all the individual distance functions.

To solve for intersection, we march along the ray in variable steps. That is: for any point along the ray, we find the smallest distance to any surface in the scene and step forward this distance. Repeat until the distance is below a given epsilon. This way we can speed up the raymarching, and prevent missing surfaces

Displaying the results
---------------------
Using OpenGL we create a quadrilateral and a texture to be rendered onto that quad.
This allows us to render at a resolution lower than the window and simply scale the quad in the vertex shader.
The raymarching algorithm will be implemented in the fragment shader.

Perspective
-----------
An advantage of ray-casting-based rendering approaches is that changing from an orthographic view to a
perspective view does not change the behaviour of the rays.

A perspective view can be modeled by positioning the eye somewhere in the world, and defining the orientation
of the image plane and the distance from the eye to the plane.

We define the orientation of the image plane using a right-vector and an up-vector. The crossproduct of these
gives us the forward-vector. If we wanted an orthographic view, all the rays would be cast parallell to this direction.

Image plane position = s = eye + focalLength * (right x up) + u * right + v * up
Ray direction = d = normalize(s - eye) = focalLength * (right x up) + u * right + v * up

Dependencies
------------
*	[GLFW](http://www.glfw.org/docs/3.0/quick.html)
*	[OpenGL Mathematics (GLM)](http://glm.g-truc.net/)

References
----------
###OpenGL###
*	[Rendering to texture](http://www.opengl-tutorial.org/intermediate-tutorials/tutorial-14-render-to-texture/)
*	[glDrawPixels](http://www.opengl.org/sdk/docs/man2/xhtml/glDrawPixels.xml)

###Raymarching###
*	[Presentation by iq](http://www.iquilezles.org/www/material/nvscene2008/rwwtt.pdf)
*	[Distance functions](http://www.iquilezles.org/www/articles/distfunctions/distfunctions.htm)
*	[Camera](http://sizecoding.blogspot.no/2008/12/code-for-moving-camera-in-glsl.html)
*	http://www.rpenalva.com/blog/?p=254
*	http://www.iquilezles.org/prods/index.htm
*	http://web.cs.wpi.edu/~emmanuel/courses/cs563/write_ups/zackw/realistic_raytracing.html
*	http://www.codermind.com/articles/Raytracer-in-C++-Part-I-First-rays.html
*	http://pouet.net/topic.php?which=6675&page=2
*	http://pouet.net/topic.php?which=6675&page=9
*	http://pouet.net/topic.php?which=7931&page=8
*	[Toolbox](http://pouet.net/topic.php?which=7931&page=1&x=29&y=6)
*	[Normal calculation](http://pouet.net/topic.php?which=6803)

###Lighting###
*	http://www.arcsynthesis.org/gltut/Illumination/Tutorial%2011.html
*	http://www.arcsynthesis.org/gltut/Illumination/Tutorial%2009.html
*	http://pouet.net/topic.php?which=7535
*	http://www.danknowlton.com/blog.php?id=480

Resources
---------
*	[Summary of using raytracing to solve the rendering equation](http://web.cs.wpi.edu/~emmanuel/courses/cs563/write_ups/zackw/realistic_raytracing.html)
*	[Stackoverflow](http://stackoverflow.com/questions/779550/are-there-any-rendering-alternatives-to-rasterisation-or-ray-tracing)
*	[Fragmentarium](http://syntopia.github.io/Fragmentarium/)
*	[Various examples created using Fragmentarium](http://blog.hvidtfeldts.net/)
*	[Raymarching beginner's thread](http://pouet.net/topic.php?which=7920&page=52)
*	[Basic raymarching tutorial](http://pouet.net/topic.php?which=8177&page=2)
*	[GPU gems](http://http.developer.nvidia.com/GPUGems3/gpugems3_ch34.html)
*	[Simple pathtracing](http://www.iquilezles.org/www/articles/simplepathtracing/simplepathtracing.htm)
*	[hvidtfeldt: Distance estimators](http://blog.hvidtfeldts.net/index.php/2011/08/distance-estimated-3d-fractals-iii-folding-space/)
*	[Kaleidoscopic (escape time) IFS](http://www.fractalforums.com/ifs-iterated-function-systems/kaleidoscopic-(escape-time-ifs)/)

Raytracing
----------
*	[Codermind](http://www.codermind.com/articles/Raytracer-in-C++-Introduction-What-is-ray-tracing.html)
*	[Minilight](http://www.hxa.name/minilight/)
*	[Smallpt](http://www.kevinbeason.com/smallpt/)
*	[Smallpt presentation](https://docs.google.com/file/d/0B8g97JkuSSBwUENiWTJXeGtTOHFmSm51UC01YWtCZw/edit)
