# PyMOL tutorial
This tutorial was written for PyMOL workshop by CCBRC, March 8-9, 2022. This is an intermediate tutorial to powerful molecular visualizer PyMOL. We will only selected things to prepare high resolution publication quality umages.

Download and install one of the floowing PyMOL, if you do not have one :

[Open source version](https://pymolwiki.org/index.php/Windows_Install) : Freely available

[Incentive version](https://pymol.org/2/#download)  : License required (Individual/Student/Teacher/Site wide]
  
## 2.1 PyMOL Graphical Interface
![fig-1-hSig7-complex](https://github.com/glycodynamics/pymol/blob/main/images/Screen%20Shot%202022-03-03%20at%207.40.34%20PM.png)

  
## 2.2.Loading structure to PyMOL:
1. Open locally structure: Open PyMOL → File → Open → Brows PDB/CIF/Mol2 file → Open
2. Get structure from Protein Data Bank: File → Get PDB → Fillup 'PDB ID' of the structure (3CHB) → Download: will open multiple units
3. Using commands: keyword ```fetch 1qoh``` will open multiple units
5. Using commands: keyword ```fetch 1qoh, type=pdb1``` will open biological assembly  

## 2.3 Modes
There are two modes in PyMOL: (1) Viewing and (2) Editing. You can switch between these modes my clicing next to "Mouse Mode" on the bottom right corner panel.\
Viewing Mode: Primarily used to view, rotate, translate, and change the representations of objects.\
Editing Mode: Used to rotate bonds, replace atoms, physically move atoms and residues, etc.\

![Figure: PyMOL Modes](https://github.com/glycodynamics/pymol/blob/main/images/Image_modes.png)

• Bottom line has 'drag window option', 'States control', 'sequence view', 'rock camera' and 'full screen' options.\
• Download PDB 7LOI ```fetch 7LOI`` and play all 15 models.\
• Change "Mouse Mode : Editing" and "Selecting " Atoms" and then try selecting 2, 3 and 4 atoms.\

## 2.3 Mouse control
Things are easier with three button mouse rather than magic mouse or using laptop's touchpad.

Viewing mode
```
L-click	: Make selection
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
PyMOl can align one structure on anther and all the structures in name list panel on another.\
Action  →  Align  → to molecule\
Command line allows you some better options. try:
```
fetch 1qoh, type=pdb1
fetch 2chb
align 1qoh, 2chb
```
now try following two alignemnt options one by one and analyze the difference between these three approaches:
```
cealign 1qoh, 2chb
super 1qoh, 2chb
```
![Alignment in PyMOL](https://github.com/glycodynamics/pymol/blob/main/images/Image_align.png)

## 2.5 Selection
• Selectin can be made my changing "Selecting" option and then clicking on particuler unit.\
• You can display protein sequences and select particuler residues from the chain\
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
| model 1ubq|m.	1qoh| Alll the atoms from object "1qoh"|
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
|label "Hello World"|		|Atoms with label "Hello World" (new in PyMOL 1.9)|

## 2.6 Colors
Download 1qoh using following commands and then try different coloring options as described below:
```
fetch 1qoh, type=pdb1
bg_color white

```
#### By using color option:
• By element: Six sets with each having 8-9 color schemes.\
• By Chain: Each chain will be colored by a different "element" scheme.\
• By ss: "helix (red/cyan)" "loop (yellow/purple/red" and "sheet (green/pink/purple)".\
• Spectrom: Rainbow color scheme.\
#### By using commands:
• ```util.chax``` : Wrapper around "color atomic" (x=g(green), b(blue), m, k, o, p s, w, y so on).\
• ```util.cbc``` : Color all chains a different color.\
• ```util.chainbow``` : Wrapper around "Rainbow color scheme".\
• ```util.ss```       : Legacy secondary structure assignment routine. **Don't use**.

## 2.7 Rendering
High-resolution photos fit for publication can be prepared by rendeing images using ```ray``` in PyMOL. Please note, the ray command can take some time (up to several minutes, depending on image complexity, size and computer power). Lets prepare a system for rensering using follwoing commands:

```
rein 
fetch 1nqu, type=pdb1 
split_states 1nqu
bg_color white
orient
util.cbc
remove ! polymer
```
Then render using Draw/ray Options or command ```ray```. When you have got somehting large and have various light points, rendering can be time taking. Rendering speed can be controlled using by setting ```hash_max```. Check current hash_max using:
```
get hash_max
```
You can set heigher hash_max rate and get better performance. Heigher hash_max uses more memory for image processing? (make sure you don’t crash it!)

```hash_max set to 100``` : 11 gb, Ray: render time: 9.69 sec. = 371.4 frames/hour (61.48 sec. accum.).\
```hash_max set to 200``` : 12 bg, Ray: render time: 4.36 sec. = 825.3 frames/hour (65.84 sec. accum.).\
```hash_max set to 400``` : 13 bg, Ray: render time: 6.28 sec. = 573.4 frames/hour (72.12 sec. accum.).\
```hash_max set to 800``` : 18 bg, Ray: render time: 9.95 sec. = 361.8 frames/hour (104.13 sec. accum.)
 
## 2.7 Image Options
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
You can change those options using ```set``` command:
```
set spec_reflect, off
set ray_shadows, off
set ray_trace_color, black
set ray_trace_fog, 0
set ray_opaque_background, on
```


### 2.7.1 Ray Trace Modes
```
rein
fetch 1nqu, async=0
bg_color white
util.cbc
remove ! polymer
set ray_trace_mode, 1   # line thickness independent of magnification
```
```
ray 			              # this is nice when zoomed in, but thick lines at low mag
ray 2400, 2400		      # line thickness is dependent on resolution
```
![Ray Trace Modes](https://github.com/glycodynamics/pymol/blob/main/images/image_ray_trace.png)

### 2.7.2 Ray Gain
You can tweek line thickness by setting up following option:

```
set ray_trace_gain, 1
set ray_trace_gain, 2
set ray_trace_gain, 0.12
```
![Ray Gain](https://github.com/glycodynamics/pymol/blob/main/images/image_ray_gain.png)
## 2.8 Representation
### 2.8.1 Sticks
```
set valence,0 
set stick_radius, 1
```

![Sticks representation](https://github.com/glycodynamics/pymol/blob/main/images/image_stick_radius.png)
### 2.8.2 Cartoon
```
as cartoon
cartoon rect
cartoon oval
cartoon tube
cartoon loop
cartoon automatic
cartoon putty.   # style the cartoon form
```
![Cartoon representation](https://github.com/glycodynamics/pymol/blob/main/images/image_cartoon.png)

### 2.8.3 Cartoon Representation Options

```
as cartoon
set cartoon_fancy_helices=1
set cartoon_flat_sheets = 0
set cartoon_smooth_loops = 1
```

![Cartoon Fancy](https://github.com/glycodynamics/pymol/blob/main/images/image_cartoon_types.png)


## 2.8.3 Secordry structure determination:
Please note that pymols internal validation of secondary structure may not always be correct. If you have any such situation, you can set the secondry structure youfelf:

```
rein
fetch 1nqu, async=0
bg_color white
orient
util.cbc
remove ! polymer
select c. C & i. 85-109       #just to see where is this selection
alter c. C & i. 85-109, ss='L'
as cartoon
```
![Sec Str](https://github.com/glycodynamics/pymol/blob/main/images/image_set_secondry_str.png)

You can set color of different secondry structure types and make it more appealing: 
```
as cartoon
color red, ss h
color blue, ss s
color yellow, ss l+
set cartoon_smooth_loops = 1
set cartoon_flat_sheets = 0
```
![Cartoon Color](https://github.com/glycodynamics/pymol/blob/main/images/image_color_options.png)

### 2.8.5 Surface
Surface of the protein can be shouws from gui (S->surface) as well as with a few commands:
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

#### Surface Quality

```
get surface_quality
set surface_quality, 2
ray
```
![Surf Quality](https://github.com/glycodynamics/pymol/blob/main/images/image_surf_quality.png)

#### Surface Reflection

```
get spec_refl
set spec_refl=11.5
ray
set spec_refl=5
ray
```
![Surf Reflection](https://github.com/glycodynamics/pymol/blob/main/images/Image_surf_spec_refl.png)

#### Solven Radius
```
get solvent_radius
set solvent_radius, 2.0
set surface_solvent = on
```
![Surf Refpection](https://github.com/glycodynamics/pymol/blob/main/images/image_solvent_radius.png)

## 2.9 Slices:

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
set opaque_background
ray
```
```
# Change sorface color to gray
set surface_color, white
ray
```

```
# render foreground image 
cmd.clip("near", near_dist)
cmd.clip("far", far_dist)
as cartoon
util.cbc
unset opaque_background # dont miss this!
ray
```
You can superimpose surface and cartoon representation in powerpoint or any image editor of your choice. 
![Surf Slices](https://github.com/glycodynamics/pymol/blob/main/images/image_surf_slices.png)


## Exploiting PyMOL to get images like other packages
### QuteMol: 
QuteMol visualization techniques are aimed at improving clarity and an easier understanding of the 3D shape and structure of large molecules or complex proteins. Ball and Sticks, Space-Fill and Liquorice visualization modes are most common.

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
Note that ray_shadow whould not be switched off on this task!
![QuteMol](https://github.com/glycodynamics/pymol/blob/main/images/image_quietmol.png)


###  David Goodsell like images:
Prof David S. Goodsell is especially known for his watercolor paintings of cell interiors. We can use pymol to create images something similar to his water paining image of Cascade surveillance complex of the Type I CRISPR bacterial immune system from Escherichia coli (2015) shown below. 

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

Now set the lights, ray tracing setttings to get the Goodsell-like rendering

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


## Acknowledgement:
PyMOL Roos tutorials
pymol.org
NIH, UM and GlyCORE


