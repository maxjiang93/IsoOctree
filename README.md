# IsoOctree
Unconstrained Isosurface Extraction on Arbitrary Octrees (Unix Port for Misha Kazhdan's original Windows implementation)

## About the code
This is a port for Misha Kazhdan's original [IsoOctree](http://www.cs.jhu.edu/~misha/Code/IsoOctree/) code from Windows. Some Windows based C++ standard functions are swapped out, and a CMake file is provided. 

## Compiling the code
Standard CMake compile will work
```bash
mkdir build; cd build
cmake ..
make
```

## Examples
```bash
./IsoOctree --in ../example/bunny.ply --out ../example/bunny_out.ply --maxDepth 6
```

## Code specification from original project
### Code Description
The code provides an implementation of the isosurface extraction in the context of mesh-simplification. Given an input mesh, the Euclidean Distance Transform of the mesh is computed and an octree is adapted to the data, sampling the transform more finely near the surface of the mesh. (Additional parameters allow the user to restrict octree refinement to high-curvature regions.) Finally, the zero-crossing isosurface is computed and written to the specified output file. (By default, the output is a polygonal representation, though a triangulation can be obtained as well by enabling the flag that computes the minimal area triangulation.)
**Note**: The construction of the EDT assumes that the input mesh is watertight with properly oriented triangles. In the case that these conditions are not satisfied (and sometimes even if they are) spurious disconnected surface patches may be generated.

### Executable Arguments
--**in** <*input mesh*>  
&nbsp; &nbsp; &nbsp; &nbsp; This string is the name of the file containing the mesh used to bulid the Euclidean Distance Transform. The mesh is assumed to be in the PLY format.  
--**out** <*output mesh* > 
&nbsp; &nbsp; &nbsp; This string is the name of the file to which the extracted isosurface will be written. The mesh will be written in the PLY format.  
--**maxDepth** <*octree depth*>  
&nbsp; &nbsp; &nbsp; &nbsp; This integer is the maximum depth of the octree used to sample the Euclidean Distance Transform of the input mesh.  
[--**curvature** <*cut-off value*>]  
&nbsp; &nbsp; &nbsp; &nbsp; This floating point value represents the cut-off used for determining if the octree is to be refined.  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; (In practice, a cut-off value of about 0.99 does a good job of generating an adaptively sampled Euclidean Distance Transform that results in a simplified model with coarser triangles in flatter regions and finer triangles in regions of high-detail.)  
[--**conforming**]  
&nbsp; &nbsp; &nbsp; &nbsp; If this argument is specified, the octree sampling the Euclidean Distance Transform will be forced to satisfy the condtion that the depth-disparity between face-adjacent leaf nodes is never greater than one.  
[--**fullCaseTable**]  
&nbsp; &nbsp; &nbsp; &nbsp; If this argument is specified, the ambiguous Marching-Cubes cases are dis-ambiguated by assigning a value to the center of a face equal to the average of the corners.  
[--**triangleMesh**]  
&nbsp; &nbsp; &nbsp; &nbsp; If this argument is specified, the minimal area triangulation is used to triangulate the polygons making up the isosurface.   
[--**dual**]  
&nbsp; &nbsp; &nbsp; &nbsp; If this argument is specified the primal/dual method of [Schaeffer and Warren 04](https://www.cs.rice.edu/~jwarren/papers/dmc.pdf) is used to compute the isosurface, sampling the Euclidean Distance Transform at the centers of octree leaf-nodes rather than the corners.  
