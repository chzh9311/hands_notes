# Rendering
## Rasterization
From volume to a raster image.
![[Rasterization.png]]
1. Painter's Algorithm:
	1. Needs sorting
	2. Cannot handle intersection
Z-buffer Rasterization
Store RGBA+$z$ (depth) values for each pixel (the centre of the pixel). Actually sorting the pixels (only one $z$)
- Needs sorting for semi-transparency.
A-Buffer Rasterization
Store all RGBA+$z$ values.

## Ray-Tracing#
does the opposite
![[Pasted image 20241104194047.png]]


# Shading
## Per-vertex shading
The norm of a vertex is calculated by the average of its adjacent planes.
![[Pasted image 20241024195057.png]]