David Tu
david.tu2@csu.fullerton.edu

A program which draws a teapot with two light sources, based on Professor Shafae's hello_glsl program.
The light sources are white and the program uses the vertex and fragment shaders to position the verticies and color their resulting fragments, respectively. 
The color of the fragments are based on the following formula: C = W((cos(theta) + 1)/2)^P where cos(theta) is the dot product btween the eye vector, eyedirn, and the reflection vector, R. 

This is done for every color component:
	For red, W = P = 1.
	For green, W = 1 and P = 2. 
	For blue, W = 1 and P = 20. 
	
Please also note that R = 2N(N*L) - L, where N = the normal vector, normal and L = the light direction vector, direction. The derivation of the vectors will be explained below.

To use the formula to calculate the color per fragment, the following steps where taken in the fragment shader, bronze.frag.glsl:
1. First, calculate the direction towards the eye by subtracting the eye position, (0, 0, 0), with the transformed vertex, mypos, and then normalizing the result. This will give the vector that points towards the eye, eyedirn.
2. Second, using the same method as in the first step, calculate the direction towards the light source using the position of the light source, position, and the position of the transformed vertex, mypos, and then normalize the result. This will give you a vector that points towards the light source, direction.
3. Next, calculate the normal vector that is the normal to the fragment. This can be done by normalizing the transformed normal, _normal. This will give you the vector, normal, that is perpendicular to the plane where the fragment sits.
4. Once all the required vectors are obtained (eyedirn, direction and normal), we can finally compute the final color by evoking the function, ComputeGoldLight, passing our vectors and the given variable, light_color, as the function parameters.
5. Within the function, ComputeGoldLight, the calculation of the color is made, based on the mentioned formula from the top of this document. We should have all of the required parameters to compute the final color, which is then added to the final color, gl_FragColor.
