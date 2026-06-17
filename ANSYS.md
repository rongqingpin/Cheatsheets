### General & administration
- `$ <directory for ansys_inc>/<version>/Framework/bin/Linux64/runwb2` to spin up workstation
- `$ <directory for ansys_inc>/<version>/fluent/bin/fluent`
- `$ <directory for ansys_inc>/Shared Files/Licensing/winx64/lmutil lmstat -a -c <license server>` to show license usage


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
