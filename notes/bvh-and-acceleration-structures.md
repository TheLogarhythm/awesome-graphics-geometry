# BVH And Acceleration Structures

BVHs are the acceleration structure to learn first for ray tracing geometry.
This note keeps only strongly related resources so the study path stays fast:
understand why acceleration structures are needed, how BVHs are built, how they
are traversed, how fast builders work, and how production systems expose them.

Prerequisite: know what a ray, primitive intersection, and hit record are. Do
not spend much time here on general ray tracing or ray-triangle details; those
are inputs to the BVH topic, not the topic itself.

## Core Learning Path

- [Introduction to Acceleration Structures](https://www.scratchapixel.com/lessons/3d-basic-rendering/introduction-acceleration-structure/introduction.html), Scratchapixel.
  - Why it matters: fastest entry point for the core problem: brute-force
    ray-object testing does not scale, so geometry needs a hierarchy of cheap
    rejection tests.
  - Best read after: basic ray tracing and ray-object intersection.
  - Code/slides/video: web tutorial.
- [Ray Tracing: The Next Week](https://raytracing.github.io/books/RayTracingTheNextWeek.html), Peter Shirley, Trevor David Black, Steve Hollasch.
  - Why it matters: gives a small, concrete BVH implementation after the basic
    ray tracer, which is useful before reading renderer or research code.
  - Best read after: Ray Tracing in One Weekend, or equivalent ray tracing
    basics.
  - Code/slides/video: book source and code are available from the Ray Tracing
    in One Weekend series.
- [Bounding Volume Hierarchies](https://www.pbr-book.org/4ed/Primitives_and_Intersection_Acceleration/Bounding_Volume_Hierarchies), PBRT v4.
  - Why it matters: main deep learning resource for BVH construction,
    primitive bounds, SAH, tree flattening, and traversal in a renderer.
  - Best read after: Scratchapixel and Ray Tracing: The Next Week.
  - Code/slides/video: PBRT book text and renderer source.

## Acceleration Structure Overview

- [Acceleration Datastructures for Raytracing](https://geometrian.com/resources/tutorials/rtaccel/), Geometrian.
  - Why it matters: compact comparison of grids, k-d trees, BVHs, SAH, LBVH,
    HLBVH, and practical acceleration structure choices.
  - Best read after: Scratchapixel's acceleration structure introduction.
  - Code/slides/video: web tutorial.

Use this resource to understand why BVHs are usually the default for modern ray
tracing. Do not get pulled too far into every alternative structure on a first
pass; compare them only enough to understand the BVH design tradeoff.

## BVH Construction And SAH

- [Bounding Volume Hierarchies](https://www.pbr-book.org/4ed/Primitives_and_Intersection_Acceleration/Bounding_Volume_Hierarchies), PBRT v4.
  - Why it matters: best single resource for learning BVH construction choices,
    surface area heuristic intuition, bucketed SAH, and flattened tree layout.
  - Best read after: basic acceleration structure motivation.
  - Code/slides/video: PBRT source.
- [Acceleration Datastructures for Raytracing](https://geometrian.com/resources/tutorials/rtaccel/), Geometrian.
  - Why it matters: useful companion for seeing SAH, binned SAH, LBVH, and
    HLBVH side by side.
  - Best read after: PBRT BVH construction if you want implementation detail
    first; before PBRT if you want taxonomy first.
  - Code/slides/video: web tutorial.

Focus questions:

- What cost model is used to choose a split?
- Is the builder optimizing traversal quality, build time, memory, or update
  speed?
- Does the builder assume static geometry, dynamic geometry, or GPU parallelism?

## BVH Traversal

- [Bounding Volume Hierarchies](https://www.pbr-book.org/4ed/Primitives_and_Intersection_Acceleration/Bounding_Volume_Hierarchies), PBRT v4.
  - Why it matters: shows practical traversal over a flattened BVH and connects
    the tree representation to renderer implementation.
  - Best read after: BVH construction and SAH.
  - Code/slides/video: PBRT source.
- [Understanding the Efficiency of Ray Traversal on GPUs](https://research.nvidia.com/publication/2009-08_understanding-efficiency-ray-traversal-gpus), Timo Aila and Samuli Laine, 2009.
  - Why it matters: classic paper for understanding why traversal performance
    depends on memory behavior, divergence, SIMD/SIMT utilization, and ray
    coherence.
  - Best read after: PBRT BVH traversal and basic GPU architecture.
  - Code/slides/video: paper PDF.

Focus questions:

- How many bounding boxes and primitives does a typical ray test?
- How does traversal order affect early hit termination?
- How do incoherent rays change performance?

## Fast And Parallel BVH Construction

- [Maximizing Parallelism in the Construction of BVHs, Octrees, and k-d Trees](https://research.nvidia.com/publication/2012-06_maximizing-parallelism-construction-bvhs-octrees-and-k-d-trees), Tero Karras, 2012.
  - Why it matters: core paper for fast parallel hierarchy construction using
    Morton codes and radix-tree style generation.
  - Best read after: SAH and basic BVH construction.
  - Code/slides/video: paper PDF.
- [Fast Parallel Construction of High-Quality Bounding Volume Hierarchies](https://research.nvidia.com/publication/2013-07_fast-parallel-construction-high-quality-bounding-volume-hierarchies), Tero Karras and Timo Aila, 2013.
  - Why it matters: improves the quality of fast GPU-friendly BVH construction,
    making the build-speed vs traversal-quality tradeoff more explicit.
  - Best read after: Karras 2012 and PBRT's SAH discussion.
  - Code/slides/video: paper PDF.

Focus questions:

- What quality is lost when construction is made highly parallel?
- How does Morton ordering approximate spatial locality?
- When is a fast lower-quality build better than a slower high-quality build?

## Dynamic BVHs And Refit

- [Acceleration Datastructures for Raytracing](https://geometrian.com/resources/tutorials/rtaccel/), Geometrian.
  - Why it matters: gives enough context for the main dynamic-scene choices:
    rebuild, refit, partial rebuild, and build-quality degradation.
  - Best read after: static BVH construction and traversal.
  - Code/slides/video: web tutorial.
- [Intel Embree](https://www.embree.org/), Intel.
  - Why it matters: production reference for scene build quality, update flags,
    geometry types, and CPU ray tracing kernels.
  - Best read after: PBRT BVH implementation.
  - Code/slides/video: library source and documentation.

Focus questions:

- When can a BVH be refit by updating bounds instead of rebuilding topology?
- How quickly does traversal quality degrade after deformation or animation?
- How do instances separate object-level geometry from scene-level transforms?

Modern APIs often expose this split through bottom-level and top-level
acceleration structures, but the API details can wait. Learn the rebuild/refit
idea first.

## Production Reference

- [Intel Embree](https://www.embree.org/), Intel.
  - Why it matters: the most useful production reference after PBRT if you want
    to see what a high-performance CPU ray tracing library exposes.
  - Best read after: PBRT BVH construction and traversal.
  - Code/slides/video: library source and documentation.

When skimming Embree, focus on API concepts rather than internals first:
devices, scenes, geometry buffers, build quality, dynamic scenes, and supported
primitive types.

## Suggested Reading Path

Fast path:

1. Scratchapixel: Introduction to Acceleration Structures.
2. Ray Tracing: The Next Week BVH section.
3. PBRT v4: Bounding Volume Hierarchies.
4. Embree overview.

Research path:

1. Geometrian acceleration structure overview.
2. PBRT v4 BVH construction and traversal details.
3. Aila and Laine 2009 for traversal efficiency.
4. Karras 2012 for parallel BVH construction.
5. Karras and Aila 2013 for high-quality parallel construction.
6. Embree as the production CPU reference.

## Next Step

After BVH, study
[Meshlets, Clusters, LOD, And Massive Geometry](meshlets-clusters-lod-and-massive-geometry.md).

Keep those resources out of this note for now. The next topic should connect
BVH knowledge to mesh shaders, meshlets, cluster hierarchies, Nanite-style
virtualized geometry, RTX Mega Geometry, streaming LOD, and ray-tracing-aware
simplification.
