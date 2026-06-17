### General & administration
- `$ <directory for ansys_inc>/<version>/Framework/bin/Linux64/runwb2` to spin up workstation
- `$ <directory for ansys_inc>/<version>/fluent/bin/fluent`
- `$ <directory for ansys_inc>/Shared Files/Licensing/winx64/lmutil lmstat -a -c <license server>` to show license usage

---

### Geometry
- right-click `property` of geometry in workbench, can specify 2D / 3D

#### Design modeler
1. select surface
2. from `sketching`, draw edges, assign constraints & dimensions, click `generate` to complete
  - to move dimension notations, specify in `dimension`
	- to create from sketch, click any where in the sketch & click `apply`
3. from `concept`, create surfaces & choose fluid / solid, click `generate` to complete

#### SpaceClaim 
Geometry creation  
1. Select plain & sketch mode (2D must use XY plane)
2. Select object & drag & press space; enter dimension & press Tab to enter the next dimension
3. Select 3D mode to generate surface  
Pre-processing for simulation  
- For multi-fluid-zones, check the parts that share interface, `Workbench` - `share` to auto-identify, click checkmark to accept if correct
- Select the surfaces, Ctrl+G, in `Groups` - `Named selections`, rename the defined group to Fluent keywords, e.g., inlet, outlet, etc.

---

### Meshing
- Check mesh quality: Fluent - `Domain` - `Mesh` - `Check` & `Quality`  

#### Workbench Mesh
1. right click `mesh` - insert `sizing`, click geometry, select the edge & apply, specify the divisions & behavior (hard / soft)
2. right click `mesh` - insert `face meshing`, select the surface & specify the divisions
3. `mesh` - `sizing` - `use adaptive sizing`: 'yes' produces orthogonal quadrilaterals
4. right click `mesh` - insert `refinement`
5. `generate mesh`
6. select object & right click -> create `name selection` & provide names (e.g., wall) for referencing later, e.g., assigning BCs
7. may need to update `mesh` in workbench
8. Mesh properties:
  - Defaults - Physics Preference - CFD
  - Quality - Mesh Metric - Orthogonal quality (>.03)
  - Elements - less than 1M for laptop work

#### Fluent-Meshing
- Water tight geometry
- `Describe geometry`:
  - Change fluid-fluid boundary from `wall` to `internal` - interfaces
  - If interfaces have been identified (`share`) in SpaceClaim, do NOT apply share Topolgy
- After generating surface mesh, can right-click to add `improve surface mesh` to reduce low quality (e.g., skewness > 0.8) faces
- `generate volume mesh`:
  - Polyhedron is usually good as default. Poly-hexcore = hex in core + poly/tet near BL
  - can right-click to add `improve volume mesh` to reduce low quality (e.g., orthogonality < 0.1) cells
