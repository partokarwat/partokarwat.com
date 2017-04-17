+++
date = "2017-03-12"
topics = ["Development"]
tags = ["udacity","android", "google"]
description = "Improve on app's performance"
title = "Android Performance"

+++
You can find the corresponding udacity course [here] (https://www.udacity.com/course/android-performance--ud825).

# Table of Contents
1. [Rendering performance](#rendering-performance)
2. [Compute performance](#compute-performance)
1. [Memory performance](#memory-performance)
1. [Battery performance](#battery-performance)

Why performance? Bad performance is the most common cause for bad reviews. Perf matters for usability and user exerience.

# Rendering performance

Is the most common issue.

Jank is a dropped frame, when calculations to draw take too long (more than 16ms).

The rentering pipeline goes from CPU to GPU an then to the Screen:
![The rentering pipeline](/media/rendering-pipeline.png)

Rule of thumb: Get as much data onto the GPU as fast as possible and leave it there without modifying it for as long as possible.

## Overdraw Problem

Diagnotstic on mobile device:

1. Go to Settings > Developer Options 
2. Turn on Debug GPU Overdraw. 
3. In the popup, choose Show overdraw areas.

Now you can see how often you redraw a pixel:

- <span style="color:red">4x Overdraw</span>
- <span style="color:lightpink">3x Overdraw</span>
- <span style="color:lime">2x Overdraw</span>
- <span style="color:blue">1x Overdraw</span>

The 2 ways to remove overdraw:

- Eliminate unneeded backgrounds and drawables from views that won't contribute to the final rendered image
- Define areas of your screen that you know will hide portions of your view

# Compute performance

# Memory performance

# Battery performance

**Written with <span style="color:orange">&#x263B;</span> in Kiel.**