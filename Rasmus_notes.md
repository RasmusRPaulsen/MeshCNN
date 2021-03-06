# Rasmus' notes on MeshCNN

## Mesh structure

Defined in models/layers/mesh.py

More details in models/layers/mesh_prepare.py  (from_scratch function)

- Mesh.vs : mesh vertices. 3 numbers (x, y, z) per vertex. Just a list. The position in the list is their ID

- Mesh.edges : mesh edges. For each edge there are two numbers, which are the ids of the two vertices.

- Mesh.gemm_edges : Each entry is the indices of the 4 one-ring neighbours of an edge.

- Mesh.sides :

- Mesh.v_mask : Boolean vector with the same number of elements as numbers of vertices. Marks if a vertex is active. Deleting a vertex is equal to setting the entry to False.

- Mesh.ve : Indexed by vertex id. For every vertex id has a list of edges (indices) that uses that vertex. 

- Mesh.edge_areas : The sum of areas of the two surrounding faces

## Selected functions

models/layers/mesh_prepare.py:

- fill_from_file: reads a OBJ file and generates vertices and faces. A face is defined by three values that are the ids of the vertices.  

- build_gemm: build mesh connectivity based on edges. Most of the logic happens here.