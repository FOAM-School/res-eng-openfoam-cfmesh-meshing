# Introduction to "Reservoir Engineering with OpenFOAM"

> This case works with Foam-Extend 4.0

## Meshing a sample porous medium with cfMesh

This repo holds a dummy case used only for meshing (no initial state, no solver-specific files).

### Building the model's STL geometry

- We have used `porespy` python library to create an image with blobs.
- We then vectorize it into an SVG and use svg2stl.com to extrude the shape and save it as an STL file.
- For the 2D mesh, we save another copy of the STL file where all face whose normals are in
  the z-direction were removed.

### Generating the mesh

It only takes one command to generate the mesh using a specific workflow

- `cartesian2DMesh` for 2D hex-based meshes
- `cartesianMesh` for 3D hex-based meshes
- `tetMesh` for 3D tetrahedral meshes
- `pMesh` for 3D poly-meshes.

Then you can fix the boundary patches with:

```bash
autoPatch 75 -overwrite
setSet -batch extractInletFaces
setSet -batch extractOutletFaces
setSet -batch extractFrontAndBackFaces
setSet -batch extractGrainsFaces
createPatch  -overwrite
```
