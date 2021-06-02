---
title: OnCanvas Alignment Guides in Inkscape
date: "2021-05-25T06:31+00:00"
template: "post"
draft: false
slug: "gsoc2021-project"
category: "Inkscape"
tags:
  - GSoC'21
  - Inkscape
description: "This blog breifly explains by GSoC Project at Inkscape"
socialImage: '/media/snap.png'
---

_The following is an excrept from my actual GSoC proposal_

### TLDR
I propose to add OnCanvas Alignment Guides to Inkscape. When enabled, while moving objects around in the canvas, the selection will snap to temporary Horizontal or Vertical guide lines that will appear if the selected object can be aligned relative to another object on the canvas.

## Motivation

Currenty on Canvas Snapping in Inkscape is limited only to snapping points in close poximity.
Points on objects are snapped based on their distance (_L2 Norm_). However there is no provision
for snapping objects that may align with each other. Currently the Align & Distribute dialog is the 
only way to align objects. 
Alignment Snapping or __Smart Snaping__ as some call it is an integral feature of modern
graphics software.

## So what are Alignment Guides?

Alignment guides are Horizontal or Vertical lines that only appear when you're 
editing objects on the canvas. They provide more contextual information about and
objects X/Y position relative to other nearby objects. As you get closer to align
the selection with the edge of another nearby object, the selection will automatically 
snap to that position and an Alignment Guide that coincides with the (now aligned)
edges will appear to indicate that a snap has indeed occurred. This guide can be
in vertical or horizontal direction depending on the optimum snap found

![Image](/media/b1-1.png)

## Searching for Snap Candidates

The easiest way to find candidate alignment positions is by looking at the corner
and edge midpoints of bounding boxes of the surrounding objects.
Once the candidate points are found we can find the best snap position in the following way:
- Extend two lines from the source point in X and Y direction.
- Find the perpendicular distance of all candidate points to these lines
- Let's say point Q has the least distance from one of the lines, then the position
to snap to is a point R which is the projection of Q on the line perpendicular to the one from which the distance is measured. (This process can be simplified by just moving the point P the same amount perpendicular to the line from which the distance is measured).

![Image](/media/snap.png)

## Settings and Toggles

After some discussion with #team_ux, I feel the following scheme would be the 
best in terms of giving extra control but at the same time not making this feature
too complicated.

### Toggle Buttons:

- Alignment Snapping (enable/disable alignment guides to snap to bounding boxes of the objects, no snapping when editing nodes) (enabled by default)
  - Snap only to itself (enable/disable alignment guides while editing nodes to other nodes in the path that is being edited) (disabled by default)

## What More?

This is just an early assesment in terms of what we can do with Alignment Guides
One of the future possible goals of this project is use Alignment Guides to distribute objects
![Image](/media/distribute.png)


