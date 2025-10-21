---
title: "Unveiling the Construction Orb: Building with God Power in Grey"
meta_title: "Unveiling the Construction Orb: Building with God Power in Grey"
description: "Our first god power and how we visualized it."
date: 2025-10-21T08:31:16Z
image: "/title.gif"
categories: ["Development", "Game Design"]
author: "Diener Brothers"
tags: ["Grey", "God Simulation", "Game Mechanics"]
draft: false
---

We're thrilled to pull back the curtain on one of our most exciting new features: the **Construction Orb**. This powerful tool is designed to streamline your building process and add a touch of divine intervention to your gameplay.

## The World of Grey: A Quick Overview

For those new to our world, Grey is a god-game where you guide your followers to build sprawling settlements and manage resources. Our goal is to create a dynamic and engaging experience where every decision you make shapes the destiny of your civilization. Resource management, strategic placement, and adapting to an ever-changing environment are key to success.

## The Construction Orb: Instantaneous Creation

Building in Grey is a core mechanic, but sometimes you need a little extra push to get things done. That's where the Construction Orb comes in! This mystical artifact grants you the ability to **instantly complete buildings** that are currently under construction.

Imagine your workers toiling away on a crucial defensive structure, and a sudden threat emerges. With the Construction Orb, you can bypass the construction time, bringing your defenses online immediately. It's a powerful tactical option that can turn the tide of battle or accelerate your expansion.

## Visualizing Divine Intervention: The Metaballs Shader

To make the Construction Orb feel truly special and visually distinct, we've integrated a fantastic open-source [**metaballs shader**](https://godotshaders.com/shader/metaballs/). Instead of a static, generic orb, the Construction Orb is a dynamic, fluid entity composed of multiple "blobs" that smoothly blend and merge, creating an organic, almost liquid appearance.

When you pick up the orb, these metaballs animate and swirl, giving it a vibrant, living quality in your hand. And when you use it to complete a building, the orb doesn't just vanish; it gracefully **disappears by having its constituent metaballs shrink and fade away**, providing a satisfying visual cue that divine power has been expended.

This shader allows us to:
*   **Create a unique and captivating visual identity** for the orb.
*   **Provide clear feedback** to the player when the orb is active and when its power is consumed.
*   **Enhance the sense of magic and power** associated with the feature.

## A Low-Maintenance Approach to Construction Progress

Many games feature detailed construction animations where buildings are assembled piece by piece. While this can be visually impressive, it's also very time-consuming to create and maintain, especially for a small team. We opted for a more elegant and scalable solution: a progress shader.

Our shader creates a "build-up" effect by gradually revealing a transparent version of the building from bottom to top. This gives a clear indication of the construction progress without requiring us to create custom animations for each building. It's a simple and effective solution that saves us a lot of development time.

Here's the shader code:

```glsl
shader_type spatial;

uniform float progress : hint_range(0.0, 1.0) = 0.0;
uniform vec4 albedo : source_color = vec4(0.5, 0.5, 0.5, 0.5);
uniform float min_y = 0.0;
uniform float max_y = 1.0;

varying float world_y;

void vertex() {
	world_y = (MODEL_MATRIX * vec4(VERTEX, 1.0)).y;
}

void fragment() {
    float height_progress = (world_y - min_y) / (max_y - min_y);
    if (height_progress > progress) {
        discard;
    }
    ALBEDO = albedo.rgb;
    ALPHA = albedo.a;
}
```

This approach allows us to easily apply the same effect to any building in the game, making our assets much more maintainable in the long run.

## See it in Action!

We're incredibly excited for you to get your hands on the Construction Orb. Be sure to check out the accompanying video to see the metaballs shader and the orb's power in full effect!

{{< video src="2025-10-21 08-31-16_ConstructionOrb.mp4" >}}

Stay tuned for more updates, and happy building!

*The Diener Brothers*

{{< x user="dienerbrothers" id="1980723726980378918" >}}