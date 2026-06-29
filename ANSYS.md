### General & administration
- `$ <directory for ansys_inc>/<version>/Framework/bin/Linux64/runwb2` to spin up workstation
- `$ <directory for ansys_inc>/<version>/fluent/bin/fluent`
- `$ <directory for ansys_inc>/Shared Files/Licensing/winx64/lmutil lmstat -a -c <license server>` to show license usage

#### Workbench
- 'Archive' instead of 'Save' to save smaller file w/o solutions / other details

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
- Geometry creation  
    1. Select plain & sketch mode (2D must use XY plane)
    2. Select object & drag & press space; enter dimension & press Tab to enter the next dimension
    3. Select 3D mode to generate surface
- Geometry manipulation
  	- press `x` & `d` to toggle cross-section view & full view
  	  	- in cross-section view, select `design` - `move`, then use `options - move` - `move grid` to rotate the cut plane
- Pre-processing for simulation  
    - For multi-fluid-zones, check the parts that share interface, `Workbench` - `share` to auto-identify, click checkmark to accept if correct
    - Select the surfaces, Ctrl+G, in `Groups` - `Named selections`, rename the defined group to Fluent keywords, e.g., inlet, outlet, etc.

---

### Meshing
- Check mesh quality: Fluent - `Domain` - `Mesh` - `Check` & `Quality`  

#### Workbench
- right click on `mesh` - `duplicate` for validation case with finer resolution

#### ANSYS Meshing
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

--- 

### Fluent Simulation

#### Workbench
After updating mesh, can right-click `Fluid Flow` - `update` to get new solution  

#### Fluent
1. `setup`, always choose 'double precision'
2. When not starting from scratch, to match zones:
    - `File` - `Recorded Mesh operations` - `match zone names`
3. check `general` - `mesh` - `scale` and `display`; check `domain` - `mesh` - `check` - `perform mesh check`
    - Can use `domain` - `mesh` - `units` to change unit system
4. `User-defined` - `Scalars`
    - for mean age-of-fluid, uncheck 'inlet diffusion', select 'all fluid zones' & 'mass flow rate'
4. go through `setup`: `general`, `model`
5. add `material` from fluent database (check `material` - `fluid`, `cell zone condition` - `fluid`)
    - For porous zone: go to `cell zone condition` - `fluid`, select the zone, then select `porous zone`, specify `viscous resistance` & `fluid porosity`
    - For mean age-of-fluid, set `UDS diffusivity` - `defined-per-uds` as 'constant' & 0 (or very small number such as 1e-9 to avoid instability). Each fluid zone needs to enable `source terms` - `user scalar` - `1 source`, and equal to fluid density.
6. set B.C. (vector direction follows right-hand-rule), right-click & choose the right type
    - `boundary conditions` - `operating conditions`: specify ref. p; simulation uses gauge p
    - Axis - cylindrical coordinate; symmetry
    - `wall` - a shadow wall is created; for actual wall, can use it to assign different BCs for liquids on both sides; for porous media interface, right-click & assign it to internal / merge it
    - For mean age-of-fluid, velocity inlet & pressure outlet need UDS as `specified value` 0; wall needs UDS as `specified flux` 0.
7. in solution, specify `methods` (`scheme` - 'SIMPLE' for slow flow; 'Coupled' for high flow)
    - `controls` - `under relaxation factor`, smaller values solves slower but are more stable: e.g., p = 0.2, rho = 1, F = 1, mv = 0.4, Ek = 0.8, ksi = 0.8, mu = 1
    - For mean age-of-fluid, first order upwind is good starting point. Can keep only USD in `Controls` - `Equations` to freeze flow field.
8. `Monitors`
    - `residual`, e.g., 1e-6
    - `report definitions` - `new` & choose other parameter to monitor
        1. Select `zones` - where to calculate; `force vector` - which F direction to calculate (force vector indicates the direction)
		2. For non-dimensionalized params, set correct ref params in `setup` - `reference values`
		3. Can report to file &/ console &/ plot. After calculation completion, can find file location at `monitors` - `report files`
9. `initialization` - `standard initialization` - `initial values`; can view `contours` under `results` - `graphics` to verify
    - Use `hybrid initialization` for 3D complex geometry
    - Use `patch` to partially initialize certain variables / zones, while continuing from previous solutions for the rest
10. `autosave` in `calculation activities`, `no. of iterations` in `run calculations`, then `calculate`

Porous flow:
- first run w/o adding porous to make sure it converges
- For faster convergence: start w/ lower vel &/ higher km & use them for initialization
- Can use 'porous jump' for quick solution w/o adding a volume of porous fluid material

---

### Post-processing

#### Workbench
- Click & drag solution 1 onto solution 2 (finer mesh) & `update` CFD-post
    - `report` - `chart` will automatically include 2 solutions
    - For other plot types, check 'sync camera in displayed views' & de-select 'sync visibility'; click each view in '3D viewer' to enable the graph for each view (solution)

#### Fluent
- after converging, view `graphics`
    - from `Viewing` - `Display` - `Views`, can flip view about axis-of-symmetry to get whole picture; deselect 'node values' to display cell center values
        - `graphics` - `colormap` can change log scale
        - `Graphics` - `Compose`: selecting 'overlays' can put figures on the same plot
- `Vectors` - scale changes length of arrow
- Add `iso-surface` & select 'mesh' as 'surface of constant' to view results on selected plane
- `pathlines`: specify 'path skip', mode 'single' / 'continuous', 'release from', to show how particles would have traveled along flow paths
    - Can color pathlines by 'time' to sample residence time
- XY plot
    - to show reference values: `Setting up physics` - `reference values` - specify - choose corresponding variables in plot 'axis function' dropdowns
    - in 'axes', adjust axis ranges & grids
    - to plot y-axis as position: check 'position on y axis', change 'plot direction' to x=0, y=1
    - to compare against reference data, use 'load file'
    - use 'new surface' to create new locations at which to view the data
- `file` - `save picture`
- `Results` - `reports`:
    - `surface integrals`: Check volume flow rate, etc., should match
    - `fluxes`: can check mass conservation (blank value = 0)
- `File` - `Export` - `Solution Data` to freeze & refer back to

#### CFD-Post
1. Click to open `results` from workbench
    - check 'keep current cases loaded' to view multiple solutions in the same graph
3. Click `contour` / `vector` / `chart` / other plots on toolbar; choose location, variable, range & no. of contour levels
    - To get a mirror image around axis of symmetry, go to `outline` - `user locations and plots` - `default transform`, deselect 'instancing info from domain', check 'apply rotation' / 'apply reflection' & choose appropriate settings if needed
    - To change axis scaling (default is axis equal), go to `view` - `apply scale`
    - To show distribution along certain line, click `location` - `line` on toolbar; then add that location in the created plot (such as 'vector'); use ctrl & select, when multiple locations are needed
    - Under `chart`, use `export` to save the data used for graph
4. To inspect specific location, click `probe` from the toolbar, then click on the graph
5. To view 3D volume: `volume rendering` from the toolbar or toolbar - `location` - `volume`
    - can select 'isovolume' to view by thresholding
