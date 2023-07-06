# Rcube-master
Rubik's Cube solver for very large cubes.

Solves any cube of any size from 1 to 65536. The code can be easily modified to handle even larger cubes. However the primary limitation is the amount of memory on a system and the length of time it takes to solve. Solve time grows ~N^2 which means it takes 4-5 times longer to solve a cube that is 2x larger in each dimension.

A 1024 layered cube can be solved in about 1.5 seconds. A 16384 layered cube can be solved in about 20 minutes.

# Solve Method
Solves the centers then corners then edges.
# Centers
The centers are solved in 15 stages where each stage moves all the pieces of a certain color from one face to the desired face. For example: a stage moves all green pieces on the white face to the green face. Repeat this for all colors and faces.

The solver uses the commutator described here which can commute center pieces from one quadrant of a face to a quandrant on another face. A very important property of this commutator is that can be modified to move many pieces in single row at the same time. For very large cubes this means it can move hundreds if not thousands of pieces in a single operation. The average number of moves k = (2 * P + 5) / P where P is the number of pieces that can be moved per operation. K quickly approaches 2 as the cube size increases.

# Corners
The corners are solved using a basic brute force method of moving the corner into place and then rotating until the faces were oriented correctly.

# Edges
The edges are solved by moving every pair of edges to the front face, then swapping desired pieces from the left edge to the right edge. A number of functions where needed to fix or prevent parity issues.

# Face Rotation Optomization
Face rotations are essentially free. Instead of moving all the pieces on a given face (N^2 pieces) to perform a rotation, the solver simply changes the coordinate system that is uses to read/write to the face. This saves an enormous amount of data swapping.

# Total Move Estimation
The total number of moves can be estimated using a simple formula. Assuming the cube is sufficiently randomized, we can expect the first face to be 1/6 solved and therefore 5/6 of the pieces will have to be moved. The second face will be 1/5 solved and require 4/5 of the pieces to be moved. The third face 3/4, Fourth face 2/3, Fifth face 1/2 and the last face will be completely solved. The average number of moves (k) to move single piece can be estimated experimentally as ~2.1. The value of k decreases as the size of the cube increases. The value can never be less than 2 since the commutator requires each piece to be moved at least 2 times.

# Features
->Scrambles the Rubik's Cube to create a random starting configuration.

->Solves the Rubik's Cube using an efficient solving algorithm.

->Provides step-by-step visualization of the solving process.

->Allows manual rotation of cube layers to interact with the cube.
