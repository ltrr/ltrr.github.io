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

### Root System Generation

Topologically, the skeleton of the root system is a tree graph.
Our first step is to define the topology and position of the nodes of that
graph.


After the topological skeleton generation,
we must give volume to the roots.
Blender's Skin modifier is adequate to the job,
but it requires us to define the fill
radius for each vertex.

A Subdivide Surface modifier is afterwards added to give
the roots an organic look.

### Mushroom Caps Generation

A reference mushroom head mesh was created manually.

In the root system generation stage,
the position for the mushroom caps and relative skin radius are stored.
Afterwards, mushroom cap objects based on the reference mesh are created
in the defined positions, and scaled proportionally to the radius.
The relative cap proportions are given by the user as parameters.



## Result

Below we see a complete result,
after manual addition of textures and lightning.

{% include image.html name="textured_result.png" width="800px" caption="Textured result" %}

## Links
* [Source](https://example.com)
