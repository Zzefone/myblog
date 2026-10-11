+++
title = "Edge detection: gradients and Laplacian zero crossings"
date = 2026-10-11
description = "Comparing edges in buildings, roads, people and a car. The tiger shows where edge detection falls short."
tags = ["BCV", "edge detection", "image processing", "Python"]
categories = ["BCV"]
courses = ["BCV"]
source_files = ["BCV/output/EdgeDetection_Report_Wang Zhaofeng.pdf", "BCV/output/run_metadata.json", "BCV/tmp/make_blog_figures.py"]
+++

The same photograph can give quite different edge maps. For this BCV lab, I compared a gradient detector with a Laplacian zero-crossing detector. The teacher's notebooks weren't available, so these results come from an independent Python implementation.

Both methods start with grayscale conversion and Gaussian smoothing. The gradient pipeline uses Sobel derivatives, thinning and hysteresis. The Laplacian pipeline looks for sign changes in the filtered response. Small fragments are removed at the end.

In each comparison below: original on the left, gradient in the middle, Laplacian on the right.

## Buildings and roads

{{< portfolio-image src="images/bcv/edge-detection/building-comparison.png" alt="Building photograph beside gradient and Laplacian edge maps, showing roof, window and tree contours." >}}

*Building.* The roof, towers and windows remain readable. The gradient map is cleaner here; the Laplacian keeps more stone and tree texture. Some weak wall details disappear in both.

{{< portfolio-image src="images/bcv/edge-detection/carrefour-comparison.png" alt="Road junction photograph beside gradient and Laplacian maps of road markings, vehicles and vegetation." >}}

*Carrefour.* Small cars and road markings are easy to lose. Keeping them also leaves tree texture and shadows. More smoothing clears some clutter, but distant vehicles disappear too.

{{< portfolio-image src="images/bcv/edge-detection/street-comparison.png" alt="Street building photograph beside gradient and Laplacian edge maps of the roof, facade and surrounding plants." >}}

*Street.* A clear main building outline, with missing sections along weaker wall boundaries. The Laplacian keeps more facade strips and plant detail. Shadows remain in both maps.

## People and the car

{{< portfolio-image src="images/bcv/edge-detection/people-comparison.png" alt="Group photograph beside gradient and Laplacian edge maps showing heads, clothing outlines and background details." >}}

*People.* Heads and body outlines are recognisable. Dark clothing boundaries break in places, while clothing details, the background and even the watermark produce edges. No separation into individual people.

{{< portfolio-image src="images/bcv/edge-detection/porsche-comparison.png" alt="Silver Porsche photograph beside gradient and Laplacian edge maps showing the body outline, wheels, windows and reflections." >}}

*Porsche.* The wheels and windows are clear. The silver body against the grey background is harder to keep continuous. Reflections and the ground shadow also show up, especially among the extra detail in the Laplacian map.

## Why the tiger is different

{{< portfolio-image src="images/bcv/edge-detection/tiger-comparison.png" alt="Tiger photograph beside gradient and Laplacian edge maps, with strong internal stripes and fragmented outer boundaries." >}}

Strong stripes, fur and whiskers. A much less reliable outer boundary. Raising the threshold can remove parts of the silhouette before it removes the stripes.

An edge map alone doesn't give a tiger region. Colour or region information would be needed to tell the animal's boundary from its internal texture.

Across these examples, the gradient method usually gives thinner, cleaner outlines. Hysteresis helps connected weak sections survive. The Laplacian often retains more local texture and needs stronger smoothing. That smoothing also costs fine detail.

Noise creates false edges; weak contrast breaks real contours. Neither method avoids that trade-off completely. These are visual comparisons without reference edge masks, so they don't establish an accuracy ranking. The main limitation remains: an intensity change can belong to an object boundary, a shadow, a reflection or a stripe.
