# Awesome Graphics Geometry

A curated, research-focused list of resources for geometry in computer graphics,
from geometry processing foundations to BVHs, LOD, meshlets, and massive
real-time geometry.

This repository complements `awesome-restir`, which focuses
on light transport sampling and sample reuse. Here, the focus is scene geometry:
how shapes are represented, processed, simplified, accelerated, streamed, and
rendered efficiently.

## Start Here

Computer graphics geometry sits between mathematical shape representation and
practical rendering systems. For research in modern rendering, it is useful to
understand both sides:

- geometry processing: meshes, surfaces, parameterization, simplification,
  deformation, and reconstruction;
- geometry for rendering: ray intersections, acceleration structures, LOD,
  meshlets, clusters, streaming, and GPU-friendly scene representation.

This list is intentionally biased toward resources that help with research in
real-time rendering, ray tracing, and massive geometry systems.

## Learning Roadmap

1. Learn polygon meshes, surfaces, and basic geometry processing language.
2. Study simplification, parameterization, subdivision, and deformation.
3. Learn ray-geometry intersection and acceleration structures.
4. Study BVH construction, traversal, refitting, and update strategies.
5. Explore meshlets, clusters, LOD, streaming, and massive geometry systems.
6. Track frontiers such as ray-tracing-aware LOD, dynamic massive geometry,
   neural geometry, and differentiable geometry processing.

## Foundations

- [Stanford CS468: Geometry Processing Algorithms](https://graphics.stanford.edu/courses/cs468-10-fall/)
  - Classic graduate course on geometry processing algorithms.
- [Geometry Processing CSC2520](https://github.com/alecjacobson/geometry-processing-csc2520)
  - Course materials from Alec Jacobson, with practical geometry processing topics.
- [Discrete Differential Geometry](https://www.cs.cmu.edu/~kmcrane/Projects/DDG/)
  - Strong foundation for curvature, meshes, and differential geometry in graphics.
- [Polygon Mesh Processing](https://www.pmp-book.org/)
  - Book focused on mesh data structures, smoothing, parameterization, and simplification.
- [Skinning: Real-time Shape Deformation](https://skinning.org/)
  - Focused resource on deformation, skinning, and animation-related geometry.

## Geometry Processing

- Mesh simplification and remeshing
  - Important for LOD, compression, and rendering large scenes efficiently.
- Surface parameterization
  - Important for texture mapping, UV generation, and signal storage on surfaces.
- Subdivision surfaces
  - Important for smooth modeling, displacement, and production asset pipelines.
- Shape deformation
  - Important for animation, simulation, and dynamic geometry.
- Reconstruction and point clouds
  - Important for scanned assets, neural reconstruction, and real-world geometry.

## Geometry For Rendering

- [Scratchapixel: Introduction to Acceleration Structures](https://www.scratchapixel.com/lessons/3d-basic-rendering/introduction-acceleration-structure/introduction.html)
  - Beginner-friendly explanation of why acceleration structures are needed.
- [Ray Tracing in One Weekend](https://raytracing.github.io/)
  - Practical introduction to ray tracing and geometry intersections.
- Ray-triangle and ray-primitive intersection
  - Core operation behind ray tracing and path tracing.
- Displacement and micromeshes
  - Compact ways to represent high-frequency geometric detail.
- Visibility and occlusion
  - Connects geometry representation to shadows, culling, and rendering cost.

## Acceleration Structures And BVH

- [Acceleration Datastructures for Raytracing](https://geometrian.com/resources/tutorials/rtaccel/)
  - Practical overview of acceleration structures for ray tracing.
- [Intel Embree](https://github.com/RenderKit/embree)
  - High-performance CPU ray tracing kernels and acceleration structures.
- BVH construction
  - Study SAH, LBVH, HLBVH, spatial splits, and build-quality tradeoffs.
- BVH traversal
  - Study traversal cost, ray coherence, stackless traversal, and packet tracing.
- BVH update and refit
  - Important for dynamic scenes, deformation, animation, and real-time ray tracing.

## Real-Time Massive Geometry

- [NVIDIA RTX Mega Geometry](https://github.com/NVIDIA-RTX/RTXMG)
  - NVIDIA sample for cluster-based geometry and ray tracing acceleration.
- [NVIDIA RTX Mega Geometry technical blog](https://developer.nvidia.com/blog/nvidia-rtx-mega-geometry-now-available-with-new-vulkan-samples/)
  - Overview of RTX Mega Geometry and its Vulkan samples.
- [Nanite Virtualized Geometry](https://dev.epicgames.com/documentation/unreal-engine/nanite-virtualized-geometry-in-unreal-engine)
  - Unreal Engine documentation for virtualized geometry and high-detail assets.
- [A Deep Dive into Nanite Virtualized Geometry](https://www.wihlidal.com/projects/nanite-deepdive/)
  - Detailed technical discussion of Nanite-style massive geometry rendering.
- [Using Mesh Shaders for Professional Graphics](https://developer.nvidia.com/blog/using-mesh-shaders-for-professional-graphics/)
  - NVIDIA introduction to mesh shaders for GPU-driven geometry pipelines.

## Libraries And Frameworks

- [libigl](https://libigl.github.io/)
  - Geometry processing library with many educational examples.
- [Geometry Central](https://geometry-central.net/)
  - C++ geometry processing library for surface and point cloud algorithms.
- [OpenMesh](https://www.graphics.rwth-aachen.de/software/openmesh/)
  - Half-edge mesh data structure and mesh processing toolkit.
- [CGAL](https://www.cgal.org/)
  - Broad computational geometry algorithms library.
- [Intel Embree](https://github.com/RenderKit/embree)
  - Useful reference for high-performance ray tracing acceleration.

## Research Frontiers

- Ray-tracing-aware LOD and simplification
- Cluster-based geometry for real-time rendering
- Dynamic BVH construction, update, and refit
- Massive scene streaming and out-of-core geometry
- Displacement, micromeshes, and compact geometric detail
- Neural geometry representations and 3D reconstruction
- Differentiable geometry processing
- Geometry pipelines for real-time path tracing

## Related Awesome Lists

- [awesome-geometry-processing](https://github.com/zishun/awesome-geometry-processing)
  - Closest existing list for geometry processing resources.
- [awesome-computational-geometry](https://github.com/atkirtland/awesome-computational-geometry)
  - More focused on computational geometry algorithms.
- [awesome-computer-graphics](https://github.com/luisdnsantos/awesome-computer-graphics)
  - Broad computer graphics resource list.
- [awesome-graphics-programming](https://github.com/shlomif/awesome-graphics-programming)
  - Broad graphics programming resource list.

## Contribution Style

For each new resource, prefer this shape:

```md
- [Title](link), Author or organization, year if relevant.
  - Why it matters.
  - Best read after: prerequisite topic.
  - Code/slides/video: links if available.
```

Keep the list curated. Prefer resources that help explain research questions,
implementation tradeoffs, or modern geometry systems.

