# Geometry Processing Foundations

## Why This Matters For Graphics Geometry Research

Geometry processing is the foundation for research on meshes, LOD, meshlets,
BVHs, displacement, scanning, deformation, neural geometry, and massive
real-time scenes. The goal of this note is not to explain every algorithm in
detail. It is a study map: for each topic, it lists what to learn, which
lectures or resources to read, and why the topic matters for rendering-focused
geometry research.

## Core Ideas

### Surface Representations

Learn how geometry can be represented as triangle meshes, polygon meshes,
subdivision surfaces, implicit surfaces, point clouds, and parametric surfaces.
For graphics research, always ask what representation an algorithm assumes and
what representation the renderer eventually consumes.

Recommended resources:

- Stanford CS468 2010: [Introduction](https://graphics.stanford.edu/courses/cs468-10-fall/LectureSlides/01_Introduction.pdf) and [Basics](https://graphics.stanford.edu/courses/cs468-10-fall/LectureSlides/02_Basics.pdf).
- Polygon Mesh Processing: Chapter 1, Surface Representations.
- Polygon Mesh Processing book slides: [Surface Representations & Mesh Data Structures](https://www.pmp-book.org/download/slides/Representations.pdf).

What to watch for in papers:

- Is the method designed for triangle meshes, point clouds, implicit fields, or
  subdivision surfaces?
- Where does conversion happen, and what error does conversion introduce?
- Does the representation support sharp features, boundaries, attributes, and
  streaming?

### Mesh Connectivity And Data Structures

Learn the vocabulary of vertices, edges, faces, boundaries, manifoldness,
orientability, valence, one-rings, and genus. Then learn why half-edge or
directed-edge data structures are useful for local mesh edits.

Recommended resources:

- Stanford CS468 2010: [Basics](https://graphics.stanford.edu/courses/cs468-10-fall/LectureSlides/02_Basics.pdf) and [Mesh Data Structures](https://graphics.stanford.edu/courses/cs468-10-fall/LectureSlides/02_Mesh_Data_Structures.pdf).
- Polygon Mesh Processing: Chapter 2, Mesh Data Structures.

What to watch for in papers:

- Does the algorithm require manifold input?
- Does it need fast adjacency traversal or only indexed triangle buffers?
- Are nonmanifold edges, boundaries, disconnected components, or inconsistent
  winding handled explicitly?

### Reconstruction And Point Clouds

Learn registration, surface reconstruction, normal estimation, point-cloud
cleanup, and how scanned data becomes renderable mesh data.

Recommended resources:

- Stanford CS468 2010: [Registration and Reconstruction I](https://graphics.stanford.edu/courses/cs468-10-fall/LectureSlides/03_Surface_Reconstruction.pdf) and [Registration and Reconstruction II](https://graphics.stanford.edu/courses/cs468-10-fall/LectureSlides/04_Surface_Reconstruction.pdf).
- Polygon Mesh Processing: Chapter 8, Model Repair, as the cleanup companion.
- For later research: Poisson surface reconstruction and marching-cubes-style
  extraction papers.

What to watch for in papers:

- Does the input have oriented normals, depth maps, raw points, or partial
  scans?
- Is the output a watertight mesh, point-based representation, implicit field,
  or textured asset?
- How does noise affect later simplification, remeshing, or BVH construction?

### Discrete Differential Geometry

Learn normals, curvature, tangent spaces, Laplacians, geodesics, differential
operators, and the relationship between smooth surface theory and discrete
mesh operators.

Recommended resources:

- Stanford CS468 2010: Differential Geometry.
- Stanford CS468 2012: Differential Geometry and Discrete Exterior Calculus on
  Meshes.
- Stanford CS468 2013: Differential Geometry for Computer Science, especially
  discrete surfaces, computing curvature, finite elements/Laplacians, and
  discrete exterior calculus.
- CMU DDG: Discrete Differential Geometry: An Applied Introduction.
- Polygon Mesh Processing: Chapter 3, Differential Geometry.

What to watch for in papers:

- Which discrete operator is used: uniform Laplacian, cotangent Laplacian,
  finite elements, DEC, or another construction?
- Does the method depend on triangle quality?
- Are boundaries and nonmanifold meshes treated carefully?

### Smoothing, Fairing, And Filtering

Learn Laplacian smoothing, diffusion flow, fairing, normal filtering, feature
preservation, and the common shrinkage/detail-loss tradeoff.

Recommended resources:

- Stanford CS468 2010: Smoothing.
- Stanford CS468 2012: Smoothing and Linear Solvers.
- Polygon Mesh Processing: Chapter 4, Smoothing.
- Polygon Mesh Processing: Appendix A, Numerics, if the method uses sparse
  linear systems.

What to watch for in papers:

- Is smoothing applied to vertex positions, normals, curvature, attributes, or
  an error field?
- Does it preserve sharp features and boundaries?
- Does it change geometry seen by ray tracing, or only shading normals?

### Simplification And LOD

Learn edge collapse, vertex clustering, incremental decimation, progressive
meshes, quadric error metrics, approximation error, and out-of-core
simplification.

Recommended resources:

- Stanford CS468 2010: [Simplification](https://graphics.stanford.edu/courses/cs468-10-fall/LectureSlides/08_Simplification.pdf) and Progressive Meshes.
- Stanford CS468 2012: Simplification and Progressive Meshes.
- Polygon Mesh Processing: Chapter 7, Simplification & Approximation.
- For rendering research later: papers on view-dependent LOD, meshlets,
  cluster hierarchies, and ray-tracing-aware LOD.

What to watch for in papers:

- What error metric drives simplification: geometric distance, normal error,
  silhouette error, screen-space error, or ray-hit error?
- Are UVs, normals, material boundaries, displacement, and skinning preserved?
- Is the LOD hierarchy suitable for streaming, culling, GPU traversal, or BVH
  updates?

### Subdivision

Learn subdivision schemes, especially the difference between approximating and
interpolating schemes, plus how coarse control meshes become smooth renderable
surfaces.

Recommended resources:

- Stanford CS468 2010: [Subdivision](https://graphics.stanford.edu/courses/cs468-10-fall/LectureSlides/10_Subdivision.pdf).
- Stanford CS468 2012: Subdivision.
- Polygon Mesh Processing: use the surface representation and remeshing
  chapters as background; supplement with dedicated Catmull-Clark and Loop
  subdivision references.

What to watch for in papers:

- Is subdivision used as a modeling representation, a rendering-time
  tessellation strategy, or an analysis tool?
- How are creases, boundaries, UVs, and displacement handled?
- Is tessellation adaptive to screen-space error, curvature, displacement, or
  ray-tracing needs?

### Parameterization

Learn UV parameterization, seams, distortion, conformal maps, area-preserving
maps, barycentric mapping, and distortion analysis.

Recommended resources:

- Stanford CS468 2010: Parameterization I and II.
- Stanford CS468 2012: Parameterization I and II.
- Polygon Mesh Processing: Chapter 5, Parameterization.
- Stanford CS468 2013: Conformal Geometry, if you want a deeper differential
  geometry route.

What to watch for in papers:

- What distortion is minimized: angle, area, stretch, boundary distortion, or
  application-specific signal error?
- How are seams chosen, and are seams compatible with materials, normal maps,
  displacement, and lightmaps?
- Does the parameterization survive simplification or remeshing?

### Remeshing

Learn isotropic remeshing, anisotropic remeshing, adaptive sampling, edge
split/collapse/flip operations, Delaunay/Voronoi ideas, and quad-dominant
remeshing.

Recommended resources:

- Stanford CS468 2010: Remeshing I and II.
- Stanford CS468 2012: Remeshing I and II.
- Polygon Mesh Processing: Chapter 6, Remeshing.
- Read after mesh data structures, differential geometry, and parameterization.

What to watch for in papers:

- Is the remeshing goal uniform triangle quality, curvature adaptation, feature
  preservation, simulation stability, or rendering efficiency?
- Are attributes transferred robustly?
- Does remeshing improve or hurt BVH quality, rasterization, displacement, and
  meshlet generation?

### Deformation

Learn mesh editing, handle-based deformation, Laplacian coordinates,
differential coordinates, surface deformation, space deformation, skinning, and
detail preservation.

Recommended resources:

- Stanford CS468 2010: [Deformation I](https://graphics.stanford.edu/courses/cs468-10-fall/LectureSlides/18_Deformation_1.pdf) and Deformation II.
- Stanford CS468 2012: [Deformation I](https://graphics.stanford.edu/courses/cs468-12-spring/LectureSlides/15_Deformation.pdf) and Deformation II.
- Stanford CS468 2013: Surface Deformation: Theory and Surface Deformation:
  Practice.
- Polygon Mesh Processing: Chapter 9, Deformation.
- Skinning.org for animation-oriented deformation and skinning.

What to watch for in papers:

- What is preserved: local detail, edge lengths, volume, curvature, rigidity,
  or user constraints?
- Is the method interactive, offline, linear, nonlinear, local, or global?
- How does deformation update bounds, LOD choices, and acceleration structures?

### Spectral Methods And Shape Analysis

Learn Laplacian eigenvectors, spectral bases, shape descriptors, and how
geometry can be analyzed through operators instead of only through triangles.

Recommended resources:

- Stanford CS468 2010: Spectral Methods I and II.
- Stanford CS468 2013: Isometry Invariance and Spectral Techniques.
- Stanford CS468 2014: Data-Driven Shape Analysis, if you later want matching,
  retrieval, segmentation, and descriptors.
- Polygon Mesh Processing: Chapter 3 and Chapter 4 as prerequisite material.

What to watch for in papers:

- Is the spectral basis used for smoothing, compression, matching, retrieval,
  deformation, or learning?
- How sensitive is it to remeshing, topology changes, noise, and boundaries?
- Does the method scale to production-sized geometry?

## Mental Model

Use this note as a routing table:

- If a paper edits mesh topology, review mesh data structures, remeshing, and
  simplification.
- If a paper uses curvature, gradients, geodesics, or Laplacians, review
  discrete differential geometry.
- If a paper builds LODs, clusters, or virtualized geometry, review
  simplification, remeshing, and parameterization.
- If a paper handles animated geometry, review deformation, skinning, and BVH
  update implications.
- If a paper starts from scans, review reconstruction, point clouds, model
  repair, and simplification.

The study loop should be:

1. Read the recommended lecture/resource for the topic.
2. Write down the assumptions the algorithm makes about input geometry.
3. Connect those assumptions to rendering: memory, shading, intersections,
   culling, LOD, streaming, and acceleration structures.
4. Track which assumptions fail on real production assets.

## Links

- [Stanford CS468 2010: Geometry Processing Algorithms](https://graphics.stanford.edu/courses/cs468-10-fall/)
- [Stanford CS468 2012: Geometry Processing Algorithms](https://graphics.stanford.edu/courses/cs468-12-spring/)
- [Stanford CS468 2013: Differential Geometry for Computer Science](https://graphics.stanford.edu/courses/cs468-13-spring/)
- [Discrete Differential Geometry: An Applied Introduction](https://www.cs.cmu.edu/~kmcrane/Projects/DDG/)
- [Polygon Mesh Processing](https://www.pmp-book.org/)
- [Skinning: Real-time Shape Deformation](https://skinning.org/)
