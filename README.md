# PyMOL tutorial
 This is an intermediate tutorial on a powerful molecular visualizer, PyMOL. We will go through only selected things to prepare high-resolution publication-quality images.

Download and install one of the following PyMOL if you do not have one :

[Open source version](https://pymolwiki.org/index.php/Windows_Install) : Freely available

[Incentive version](https://pymol.org/2/#download): License required (Individual/Student/Teacher/Site wide]

PyMOL is free for teachers/and students, and an educational use only license can be obtained by registering [here](https://pymol.org/edu) 
## 2.1 PyMOL Graphical Interface
![fig-1-hSig7-complex](https://github.com/glycodynamics/pymol/blob/main/images/Screen%20Shot%202022-03-03%20at%207.40.34%20PM.png)

  
## 2.2.Loading structure to PyMOL:
1. Open structure locally: Open PyMOL → File → Open → Browse PDB/CIF/Mol2 file → Open
2. Get structure from Protein Data Bank: File → Get PDB → Fill up 'PDB ID' of the structure (3CHB) → Download: will open multiple units
3. Using commands: keyword ```fetch 1qoh``` will open multiple units
5. Using commands: keyword ```fetch 1qoh, type=pdb1``` will open biological assembly  

## 2.3 Modes
There are two modes in PyMOL: (1) Viewing and (2) Editing. You can switch between these modes by clicking next to "Mouse Mode" on the bottom right corner panel.
Viewing Mode: Primarily used to view, rotate, translate, and change the representations of objects.
Editing Mode: Used to rotate bonds, replace atoms, physically move atoms and residues, etc.

![Figure: PyMOL Modes](https://github.com/glycodynamics/pymol/blob/main/images/Image_modes.png)

• Bottom line has 'drag window option', 'States control', 'sequence view', 'rock camera', and 'full screen' options.

• Download PDB 7LOI ```fetch 7LOI`` and play all 15 models.

• Change "Mouse Mode: Editing" and "Selecting " Atoms" and then try selecting 2, 3, and 4 atoms.


## 2.3 Mouse control
Things are much easier with a three-button mouse rather than a magic mouse or using a laptop's touchpad.

Viewing mode
```
L-click	: Make a selection
M-click	: Center Camer
M-wheel	: z-plane-clipping
R-click	: Open menu
L-drag	: Camera rotate
M-drag	: Camera translate
R-drag	: Camera zoom
```

Editing mode:
```
L-click	: Make pick
M-click	: Center Camera
R-click	: Open menu
```

## 2.4 Aligning Structures
PyMOL can align one structure onto another and all the structures in the name list panel on another.
Action  →  Align  → to molecule
The command line allows some more useful options to perform the alignment. Try:
```
fetch 1qoh, type=pdb1
fetch 2chb
align 1qoh, 2chb
```
now try following two alignment options one by one and analyze the difference between these three approaches:
```
cealign 1qoh, 2chb
super 1qoh, 2chb
```
![Alignment in PyMOL](https://github.com/glycodynamics/pymol/blob/main/images/Image_align.png)

## 2.5 Selection
• Selection can be made by changing the "Selecting" option and then clicking on the particular unit.\
• You can display protein sequences and select particular residues or the chain\
• PyMOL also has a selection language that can be used with ```sel``` to select atoms based on identifiers and properties. Many commands (like color, show, etc.) take an atom selection argument to only operate on a subset of all atoms in the scene. 
Example:
```
show spheres, solvent and chain A

```
### Selection Operator/Modifier Table
| Operator|Alias|Full Descriptio|
| --------| ------------- | ------------|
|**Generic**| | |
| all|*| All atoms currently loaded into PyMOL|
| none| | Empty selection|
| model 1ubq|m.	1qoh| All the atoms from object "1qoh"|
| chain C|c.	C| Chain identifier "C"| 
| resn ALA|r.	ALA| Residue name "ALA"|
|resi 100-200	|i.	|Residue identifier between 100 and 200|
|**Chemical classes**| | |
|organic|	org.	|Non-polymer organic compounds (e.g. ligands, buffers)|
|inorganic|	ino.	|Non-polymer inorganic atoms/ions|
|solvent|	sol.	|Water molecules|
|polymer|	pol.	|Protein or Nucleic Acid|
|polymer.protein|		|Protein (New in PyMOL 2.1)|
|polymer.nucleic|		|Nucleic Acid (New in PyMOL 2.1|
|hetatm	|	|Atoms loaded from PDB HETATM records|
|hydrogens|	h.	|Hydrogen atoms|
|backbone|	bb.	|Polymer backbone atoms (new in PyMOL 1.6.1)|
|sidechain|	sc.	|Polymer non-backbone atoms (new in PyMOL 1.6.1)|
|metals|	|	Metal atoms (new in PyMOL 1.6.1)|
|donors|	don.|	Hydrogen bond donor atoms|
|acceptors|	acc.|	Hydrogen bond acceptor atoms|
|label "Hello World"|		|Atoms with the label "Hello World" (new in PyMOL 1.9)|

## Centers
Center of mass: Select atoms you want to include in the center of mass calculation.
```
centerofmass sele
```
Create Pseudoatoms:
```
pseudoatom com, pos=[ -35.972,  42.456,  14.847]
show spheres, com
```
## 2.6 Colors
Download 1qoh using the following commands and then try different coloring options as described below:
```
fetch 1qoh, type=pdb1
bg_color white

```
#### By using the color option:
• By element: Six sets with each having 8-9 color schemes.\
• By Chain: Each chain will be colored by a different "element" scheme.\
• By ss: "helix (red/cyan)" "loop (yellow/purple/red" and "sheet (green/pink/purple)".\
• Spectrom: Rainbow color scheme.\
#### By using commands:
• ```util.cbax``` : Wrapper around "color atomic" (x=g(green), b(blue), m, k, o, p s, w, y so on).\
• ```util.cbc``` : Color all chains a different color.\
• ```util.chainbow``` : Wrapper around "Rainbow color scheme".\
• ```util.ss```       : Legacy secondary structure assignment routine. **Don't use**.

## 2.7 Rendering
High-resolution photos fit for publication can be prepared by rendering images using ```ray``` in PyMOL. Please note that the ray command can take some time (up to several minutes, depending on image complexity, size, and computer power). \
**Ray Use:**\
```
ray [width,height [,renderer [,angle [,shift ]]]
```
width and height can be set to any non-negative integer\
If both are set to zero then the current window size is used and is equivalent to just using ray with no arguments.\
If one is set to zero (or missing) while the other is a positive integer, then the argument set to zero (or missing) will be scaled to preserve the current aspect ratio.\

Let us prepare a system for rendering using the following commands:

```
rein 
fetch 1nqu, type=pdb1 
split_states 1nqu
bg_color white
orient
util.cbc
remove ! polymer
ray 1024,1024.  # ray trace the current scene, but scaled to 1024x1024 pixels

```
Then render using Draw/ray Options or command ```ray```. When you have a large system with various light points, rendering can be time-consuming. Rendering speed can be controlled using by setting ```hash_max```. Check current hash_max using:
```
get hash_max
ray
set hash_max, 200
```
You can set a higher hash_max rate and get better performance. Higher hash_max uses more memory for image processing (make sure you don’t crash PyMOL!).

```hash_max set to 100``` : 11 gb, Ray: render time: 9.69 sec. = 371.4 frames/hour (61.48 sec. accum.).\
```hash_max set to 200``` : 12 bg, Ray: render time: 4.36 sec. = 825.3 frames/hour (65.84 sec. accum.).\
```hash_max set to 400``` : 13 bg, Ray: render time: 6.28 sec. = 573.4 frames/hour (72.12 sec. accum.).\
```hash_max set to 800``` : 18 bg, Ray: render time: 9.95 sec. = 361.8 frames/hour (104.13 sec. accum.)

**Save Image**
Image can be saved using ```save``` option after ```ray``
```
save pymol_image.png
```

Ray and save can be combined together and ```png``` can be used to write images as below:
```
png filename[, width[, height[, dpi[, ray[, quiet]]]]]
```
• ```filename``` = string: file path to be written\
• ```width``` = integer or string: width in pixels (integer or string without units), inches (in), or centimeters (cm). If the unit suffix is given, `dpi` argument is required as well. If only one of `width` or `height` is given, the aspect ratio of the viewport is preserved. {default: 0 (current)}\
• ```height``` = integer or string: height (see width) {default: 0 (current)}\
• ```dpi``` = float: dots-per-inch {default -1.0 (unspecified)}\
• ```ray``` = 0 or 1: should ray be run first {default: 0 (no)}

try:
```
png ~/Desktop/pymol_image.png width=10cm, dpi=300, ray=1
png ~/Desktop/pymol_image.png width=1200, height=1200, dpi=300, ray=1
```
Later will output a four-inch square image at 300dpi. Leaving off the dpi parameter would yield a 1200x1200 image at your system's default pixel density (e.g. 72 or 96 dpi). This saves the intermediate step of having to use GIMP/PhotoShop/etc to rescale your photos for publication.

## 2.8 Image Options
```
rein
fetch 1nqu, async=0
bg_color white
util.cbc
remove ! polymer
set hash_max, 200
select none
```
Check defaults:
```
get ray_shadows
get ray_trace_color
get ray_trace_fog
get depth_cue
get ray
```
Those options can be changed using ```set``` command:
```
set spec_reflect, off
set ray_shadows, off
set ray_trace_color, black
set ray_trace_fog, 0
set ray_opaque_background, on
```


### 2.8.1 Ray Trace Modes
```
rein
fetch 1nqu, async=0
bg_color white
util.cbc
remove ! polymer
set ray_trace_mode, 1   # line thickness independent of magnification
```
```
ray 			              # This is nice when zoomed in, but thick lines at low magnification
ray 2400, 2400		      # line thickness is dependent on the resolution
```
![Ray Trace Modes](https://github.com/glycodynamics/pymol/blob/main/images/image_ray_trace.png)

### 2.8.2 Ray Gain
Line thickness can be tweaked by setting up the following option:

```
set ray_trace_gain, 1
set ray_trace_gain, 2
set ray_trace_gain, 0.12
```
![Ray Gain](https://github.com/glycodynamics/pymol/blob/main/images/image_ray_gain.png)
## 2.9 Representation
### 2.9.1 Sticks
```
set valence,0 
set stick_radius, 1
```

![Sticks representation](https://github.com/glycodynamics/pymol/blob/main/images/image_stick_radius.png)
### 2.9.2 Cartoon
```
as cartoon
cartoon rect
cartoon oval
cartoon tube
cartoon loop
cartoon automatic
cartoon putty   # Cartoon form style
```
![Cartoon representation](https://github.com/glycodynamics/pymol/blob/main/images/image_cartoon.png)

### 2.9.3 Cartoon Representation Options

```
as cartoon
set cartoon_fancy_helices = 1
set cartoon_flat_sheets = 0
set cartoon_smooth_loops = 1
```

![Cartoon Fancy](https://github.com/glycodynamics/pymol/blob/main/images/image_cartoon_types.png)


### 2.9.4 Secondary structure determination:
Please note that PyMOL's internal validation of the secondary structure may not always be correct. If you notice any such mistake, you can always set the secondary structure yourself in PyMOL:

```
rein
fetch 1nqu, async=0
bg_color white
orient
util.cbc
remove ! polymer
select c. C & i. 85-109       #just to see what are we selecting selection
alter c. C & i. 85-109, ss='L'
as cartoon
```
![Sec Str](https://github.com/glycodynamics/pymol/blob/main/images/image_set_secondry_str.png)

Color of different secondary structure types  can be set to make the figure more appealing: 
```
as cartoon
color red, ss h
color blue, ss s
color yellow, ss l+
set cartoon_smooth_loops = 1
set cartoon_flat_sheets = 0
```
![Cartoon Color](https://github.com/glycodynamics/pymol/blob/main/images/image_color_options.png)

### 2.9.5 Surface
The surface of the protein can be shown from GUI (S->surface) as well as with a few commands:
```
reinitialize
fetch 1nqu, async=0
remove solvent
orient 
bg_color white
color red, ss h
color marine, ss s
color yellow, ss l+''
as surface
```

**Surface Quality**
This controls how well PyMOL draws surfaces. Lower values, like 0, are rough surface approximations. These low values are good for speed--especially for larger surfaces. For rendering of publication-quality photos, and truer representations of the biological surface, set the value higher--to something like 2, 3, or 4. In practice, typical values are 1, 2, and 3.
```
get surface_quality
set surface_quality, 2
ray
```
![Surf Quality](https://github.com/glycodynamics/pymol/blob/main/images/image_surf_quality.png)

**Specular Reflection**
This setting changes how PyMol handles specular reflections. Essentially, this setting, when combined with spec_power adjusts how sharp or diffuse the reflection is, giving you shiny-looking surfaces or duller surfaces.

```
get spec_refl
set spec_refl=1.5
ray
set spec_refl=5
ray
```
![Surf Reflection](https://github.com/glycodynamics/pymol/blob/main/images/Image_surf_spec_refl.png)

**Solvent Radius**:This defines the solvent radius. Changing the solvent radius in PyMOL affects how PyMOL interprets surfaces and surface area. The default solvent radius is 1.4 Angstroms.

```
get solvent_radius
set solvent_radius, 2.0
set surface_solvent = on
```
![Surf Refpection](https://github.com/glycodynamics/pymol/blob/main/images/image_solvent_radius.png)


## 2.10 Show Specific Properties

Let us Show the hydrophobic cores of the protein 1nqu. 

```
reinitialize
fetch 1nqu
orient 
bg_color white
set hash_max, 400
as cartoon, all
color gray, all
remove solvent
```

Now select hydrophobic residues and name them hydrophobes. 

```
select hydrophobes, (r. ala+gly+val+ile+leu+phe+met)
show spheres, (hydrophobes and (!name c+n+o))
color orange,hydrophobes
disable hydrophobes
show surface, polymer
set transparency, 0.5
show sticks, organic
color green, organic
ray 1200
save hydrophobes_low.png
```
![Image Hydrophobes](https://github.com/glycodynamics/pymol/blob/main/images/image_hydrophobes.png)

Do the following only if you have a powerful computer:

```
set spec_power = 200
set spec_refl=1.5
set surface_quality, 2
set antialias, 2
ray 1200
save hydrophobes_high.png
```

## 2.11 Slices:

```
reinitialize
fetch 1nqu, async=0
remove solvent
orient 
bg_color white
color red, ss h
color marine, ss s
color yellow, ss l+''
as surface
```
Disable these options before proceeding

```
set depth_cue, 0
set ray_shadows, 0
set ray_trace_mode, 0
```
We can clip a molecule by moding the wheel or following Python code. This Python code will give us 100% reproducibility compared to clipping by using a mouse.  
```
fraction = 0.42
view = cmd.get_view()
near_dist = fraction*(view[16]-view[15])
far_dist = (view[16]-view[15]) - near_dist
cmd.clip("near", -near_dist)
ray
```

```
# Change interior color to gray
set ray_interior_color, grey90
set opaque_background  # solid background
ray
```
```
# Change surface color to gray
set surface_color, white
ray
```

```
# render foreground image 
cmd.clip("near", near_dist)
cmd.clip("far", far_dist)
as cartoon
util.cbc
unset opaque_background # Don't miss this!
ray
```
One can superimpose surface and cartoon representation in PowerPoint or any image editor of your choice. 
![Surf Slices](https://github.com/glycodynamics/pymol/blob/main/images/image_surf_slices.png)


## 2.12 Exploiting PyMOL to get images like other packages
### 2.12.1 QuteMol: 
QuteMol visualization techniques are aimed at improving clarity and an easier understanding of the 3D shape and structure of large molecules or complex proteins. Ball and Sticks, Space-Fill, and Liquorice visualization modes are the most common.

See more at: http://qutemol.sourceforge.net/

```
reinitialize
fetch 1nqu, async=0
bg_color white
remove solvent
orient
```
```
set_color oxygen, [1.0,0.4,0.4]
set_color nitrogen, [0.5,0.5,1.0]
as spheres
util.cbaw
bg white
```
```
set light_count,8
set spec_count,1
set shininess, 10
set specular, 0.25
set ambient,0
set direct,0
set reflect,1.5
set ray_shadow_decay_factor, 0.1
set ray_shadow_decay_range, 2
```
Note that ray_shadow should not be switched off on this task!
![QuteMol](https://github.com/glycodynamics/pymol/blob/main/images/image_quietmol.png)


###  2.12.2 David Goodsell like images:
Prof David S. Goodsell is primarily known for his watercolor paintings of cell interiors. For example, Cascade surveillance complex of the Type I CRISPR bacterial immune system from Escherichia coli (2015) is shown below. We can use PyMOL to create something similar to his water painting images. 

```
reinitialize
fetch 1nqu, tmp, async=0
bg_color white
set hash_max, 400

as sticks
set valence, 0
set stick_radius = 1.7

color lightblue, not org
color magenta, org
remove solvent
```

Now set the lights ray tracing settings to get the Goodsell-like rendering.

```
unset specular
set ray_trace_gain, 0
set ray_trace_mode, 3
bg_color white
set ray_trace_color, black
unset depth_cue
ray
```
![David GoodSell](https://github.com/glycodynamics/pymol/blob/main/images/image_david_goodsell.png)

## Explore different plugins
Plugin --> Plugin Manager --> Install New Plugin 

## APBS electrostatics calculation 
APBS, the Adaptive Poisson-Boltzmann Solver, is a freely available macromolecular electrostatics calculation program in PyMOL. It  displays the results of the calculations as an electrostatic potential molecular surface.

Plugin --> APBS Electrostatics

## Acknowledgement:
[PyMOL wiki](https://pymolwiki.org/index.php/Main_Page) 

[Dr. Ross PyMOL's tutorials](https://www.rosswilsonlab.org/pymol)

This workshop is supported by an Institutional Development Award (IDeA) from the National Institute of General Medical Sciences of the US National Institutes of Health under award number P20GM130460.
### Author:
```
Sushil Mishra, PhD
Research Scientist
Computational Chemistry and Bioinformatics Research Core
Glycoscience Centre of Research Excellence (GlyCORE) 
The University of Mississippi, P.O. Box 1848
University, MS 38677-1848, USA
sushil_at_olemiss.edu
```
[Twitter](https://twitter.com/glycodynamics)\
[GlyCORE Twitter](https://twitter.com/UM_glycore)\
[CCBRC Web-page](https://pharmacy.olemiss.edu/glycore/computationalchemistrybioinformaticscore)

 


