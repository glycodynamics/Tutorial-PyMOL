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

## 2.1 Aligning Structures
PyMOl can align one structure on anther and all the structures in name list panel on another.\
Action  →  Align  → to molecule\
Command line allows you some better options. try:
```
fetch 1qoh, type=pdb1
fetch 2chb
align 1qoh, 2chb
```
now try following two alignemnt options one my one"
```
cealign 1qoh, 2chb
super 1qoh, 2chb
```

## 2.1 PyMOL Graphical Interface
Text
## 2.1 PyMOL Graphical Interface
Text
## 2.1 PyMOL Graphical Interface
Text
## 2.1 PyMOL Graphical Interface
Text


