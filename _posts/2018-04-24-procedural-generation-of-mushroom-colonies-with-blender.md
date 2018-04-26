---
layout: post
title: Procedural Generation of Mushroom Colonies with Blender
author: "Lucas Torres"
tags:
- 3D Graphics Systems
- assignment
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHT">
</script>

## Introduction

This project correspond to the assignment 1
of the 3D Graphics Systems course.
Our objective is to become familiar with Blender 3D modeling tool,
to create our own assets using some of the techniques described in the course,
and to develop procedural and parametrized models.
For this assignment, we developed a Blender API script
for the generation of mushroom colony models,
like the one shown below.

{% include image.html name="real_colony.jpg" caption="Reference Mushroom Colony" width="400px" %}

## Algorithm

The generation procedure can be divided in two parts:
* Creation of the root system and stems;
* Creation of the mushroom caps.

### Root and Stems Generation

Topologically, the skeleton of the roots and stems system is a tree graph.
Our first step is to define the topology and position of the nodes of that
graph.

Two kinds of structures are generated in the step:
* The root system, that spreads parallel to the ground;
* The stems, individual vertical protuberances that support the mushroom caps.


The root system is formed by branches, that originate from a base node,
and subbranches that recursively split from the main branches.

Each branch is constructed by a sequence of segments that follows a fixed angle
to a smooth 2D vector field;
If a radial vector field was used, for example,
branches with a 0° angle would be straight and move away from the origin,
while branches with a 90° angle would be approximately circular.
For the algorithm we used Blender's built-in smooth random vector field based on perlin noise.
Segment generation stops at a user defined maximal topological distance from the base node.

Subbranches are extruded from a branch at a 90° angle added to a random perturbation.
Splitting occurs randomly, internally treated as a Poisson event on length.

Root segment length decays exponentially with topological distance to the base node.

In the root generation process, the user can control
* Base segment length;
* Maximal topological depth for the roots;
* Expected length distance between branches;
* Perlin vector field scale (smaller scales generate more branch curvature).

Stems are formed by a group of segments moving vertically.
Like the root segment length, stem height decays
exponentially with topological distance to the origin node.
Optionally the stems can also move away horizontally from the origin,
defining a parabolic shape. Stem are generated randomly on
root nodes, as a Bernoulli event.

In the stem generation process, the user can control
* Base stem height;
* Stem generation probability;
* Horizontal displacement;

After the topological skeleton generation,
we must give volume to the roots.
Blender's Skin modifier is adequate to the job,
but it requires us to define the fill
radius for each vertex.

The root radius is such that
the root longitudinal area decays exponentially with the same rate
as the segment length. Stem radius is always equal to its base root node radius.

A Subdivide Surface modifier is afterwards added to give
the roots an organic look.

### Mushroom Caps Generation

A reference mushroom head mesh was created manually.

In the root system generation stage,
the position for the mushroom caps and relative skin radius are stored.
Afterwards, mushroom cap objects based on the reference mesh are created
in the defined positions, and scaled proportionally to the radius.
The relative cap proportions are given by the user as parameters.

## Examples
Some examples using different parameters but the same random seed.

{% include image.html name="example1.png" width="800px" %}
{% include image.html name="example2.png" width="800px" %}
{% include image.html name="example3.png" width="800px" %}
{% include image.html name="example4.png" width="800px" %}

## Result

Below we see a complete result,
after manual addition of textures and lightning.

{% include image.html name="textured_result.png" width="800px" caption="Textured result" %}

## Links
* [Source](https://example.com)
