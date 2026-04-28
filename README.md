# Flamethrower's Polygon Packer for irregular shapes

This repository is based on [Flamethrower's polygon-packer](https://github.com/Flamethr0wer/polygon-packer), a fast 2D polygon packing tool originally written to solve polygon packing problems.

The original project was used to find several optimal packings listed under the name **Ignacio Vallejo** on [Erich's Packing Center](https://erich-friedman.github.io/packing/).

This fork extends the original project by adding support for file-based irregular shape input, especially **SVG outlines** and **PNG/JPG silhouette masks**.

<img width="640" height="480" alt="30 triangles in a hexagon" src="https://github.com/user-attachments/assets/48591a93-3ed9-4031-9c42-8b6eb579d91e" />


## Original project
The original version generates regular polygons directly from command-line parameters.
```bash
python3 polygon_packer.py [n] [nsi] [nsc]
```
Where:
- `[n]` is the number of inner polygons to pack
- `[nsi]` is the number of sides of each inner polygon  
  For example, `4` creates squares.
- `[nsc]` is the number of sides of the container polygon  
  For example, `6` creates a hexagonal container.
Example:
```bash
python3 polygon_packer.py 30 3 6
```
This attempts to pack 30 triangles inside a hexagon.

### Original optional parameters
```bash
--attempts
```
The total number of attempts to run. Increase this to explore more possible packings. Defaults to `1000`.
```bash
--tolerance
```
Tolerance for the penalty function. More penalty reduces the margin of overlap but may limit exploration. Defaults to `0.00000001`.
```bash
--finalstep
```
The container size is decreased by a smaller factor each time to save compute at the beginning and improve precision near the end. This sets the shrinkage step size toward the theoretical minimum container size. Defaults to `0.0001`.


## This fork
The goal of this fork is to allow users to provide their own 2D shapes instead of only generating regular polygons from side counts.
The intended workflow is:
```text
container.svg + part.svg/png + copy count
→ convert outlines into polygon geometry
→ optimize position and rotation
→ export packed layout as SVG
```
This makes the tool more suitable for irregular-shape packing, laser-cutting layouts, material nesting, silhouette packing, and custom 2D fabrication planning.

## Planned input modes

### SVG input

SVG is the main recommended input format.
Use SVG when the shape is already a clean vector outline from software such as Inkscape, Illustrator, Figma, Fusion, or other CAD/vector tools.

### PNG/JPG silhouette input
PNG/JPG input is intended as a fallback for hand-drawn, scanned, or raster shapes. 
The program will extract the largest external contour from the image, simplify it, convert it into polygon geometry, and then pack it.
PNG/JPG mode is less precise than SVG mode(for obvious reasons).

## Planned output
The main output is an SVG layout.
Mostly cuz i like SVGs and anyone who doesn't can go get some tylenol and realize i'm right.
....
but there will also be a png output so seeing the irregular shape in a container is easier

## Limitations
This project WILL NOT support every possible SVG or image file.
- SVG text elements
- decorative strokes without filled outlines
- gradients
- open paths
- compound paths with holes
- self-intersecting paths
- complex grouped SVG transforms
- multiple different part types in one run
- fully CAD-accurate DXF workflows

this is just an experiment made out of interest so don't expect some high level stuff, svg shapes should still be simple

### Credits:
{I'll Fill this in later}
