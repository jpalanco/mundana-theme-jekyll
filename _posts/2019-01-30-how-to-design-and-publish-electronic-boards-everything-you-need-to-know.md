---
title: "How to Design and Publish Electronic Boards – Everything You Need to Know"
date: "2020-8-9"
image: assets/images/electronicboard.jpg
author: name
layout: post
tags: [ publishing, electronic boards ]
categories: [ electronic board ]
---

The Kitspace, formerly known as Kitnic, is a registry of open-source hardware electronic projects which are ready to order and build.

This means that they could be described as thingiverse for electronics.

The most important element of a Kit Space project page is what you are allowed to design for it to be actually manufactured.

You need to provide a preview of the printed circuit board and prominent link to download the Gerber manufacturing files as well as have the ability to quickly add the required components to a distributor shopping cart.

## How to Make a Circuit Board

There are three basic methods to make a PCB such as:

<![if !supportLists]>· <![endif]>Iron on Glossy Paper

<![if !supportLists]>· <![endif]>Circuit by hand on PCB

<![if !supportLists]>· <![endif]>Laster cutting edge etching

The PCB design is done by converting circuit schematic diagrams into a PCB layout using PCB layout software such as Autodesk Eagle or PCB Wizard.

Take a printout of the circuit board layout.

Take the mirror print out and select the output in black both from the PCB design software and the printer driver settings while making sure that the printout is made on the glossy side of the paper.

Cut the Copper Plate for the circuit board and transfer the PCB print onto the copper plate.

Iron the Circuit from the paper on to the PCB plate and Etch the plate.

By drilling holes using a PCB driller, solder all of the control components onto the board and your board should be ready.

## How to Add Your Project to Kitspace

<![if !supportLists]>1. <![endif]>Previewing the board.

Plot Gerbers or RS274-X and data drill from your CAD program need to be added.

To do this, put the files in a publicly accessible Git repository which can be done either through GitHub or GitLab for example, and preview your board by entering the repository URL.

If you think it has not found the right gerbers, you can add kitspace.yaml with a gerbers field.
```

gerbers: path/to/your/gerber-folder
```

Adding multiple projects in one repository is supported by Kitspace.

When it comes to the terms and conditions, Kitspace developers do not claim any ownership of your work, and it remains yours.

By submitting a project to the site, you give them permission to host copies of your files for other people to download.

If you were to change your mind, the project can be removed at any time by removing the public git repository and sending a pull-request to remove it from boards.txt.

<![if !supportLists]>2. <![endif]>Previewing the bill of materials.

You can add a bill of materials to your repository which can be done in a csv, tsv, Excel or LibreOffice spreadsheet with fields that are recognized.

You can add a kitspace.yaml with:

bom: path/to/bom.csv

<![if !supportLists]>3. <![endif]>Reviewing the readme.

Add a README.md to your repository where you will carefully explain more about the project.  
It needs to be written as a Markdown, so you can add a summary and a link to your kitspace.yaml that will appear on the top of your specific page.

summary: <a summary for your project>

site: [https://example.com](https://example.com)

When it comes to the kitspace.yaml format, it makes use of the following fields, including:

summary: A description for your project

site: A site you would like to link to (include http:// or https://)

color: The solder resist color of the preview rendering. Can be one of:

<![if !supportLists]>Ø <![endif]>green

<![if !supportLists]>Ø <![endif]>red

<![if !supportLists]>Ø <![endif]>blue

<![if !supportLists]>Ø <![endif]>black

<![if !supportLists]>Ø <![endif]>white

<![if !supportLists]>Ø <![endif]>orange

<![if !supportLists]>Ø <![endif]>purple

<![if !supportLists]>Ø <![endif]>yellow
```

<![if !supportLists]>· <![endif]>bom: A path to your 1-click-bom in case it isn't `1-click-bom.tsv`.

<![if !supportLists]>· <![endif]>gerbers: A path to your folder of gerbers in case it isn't `gerbers/`.

<![if !supportLists]>· <![endif]>eda:

<![if !supportLists]>· <![endif]>type: kicad

<![if !supportLists]>· <![endif]>pcb: path/to/your/file.kicad_pcb
```

readme: A path to your README file in case it isn't in the repository root directory.

multi: Identifier field only used if the repository contains multiple projects.

The paths need to be in an UNIX style, which means that you need to use “/” and not “\”, as well as remain relative to the root of your repository.

On the other end of the spectrum, if you used KiCad for your design, you can specify a KiCad PCB file to use by adding an eda field.
```

<![if !supportLists]>· <![endif]>eda:

<![if !supportLists]>· <![endif]>type: kicad

<![if !supportLists]>· <![endif]>pcb: path/to/your/file.kicad_pcb
```

If you project has a KiCad PCB file however, the interactive assembly guide for the board can be created using the interactive HTML BOM plugin from the Open Scope Project.

If both the eda and the garbers are present, the Gerber files will be used.

To check out the repo links of the projects listed on kitspace.org already, the minimum required file tree is as shown here:
```
.

├── 1-click-bom.tsv

└── gerbers

├── example.cmp

├── example.drd

├── example.dri

├── example.gko

├── example.gpi

├── example.gto

├── example.plc

├── example.sol

├── example.stc

└── example.sts
```
A more advanced example should look something like this:
```
.

├── kitspace.yaml

└── manufacture

├── advanced-example-BOM.tsv

└── gerbers-and-drills

├── advanced-example-B_Adhes.gba

├── advanced-example-B_CrtYd.gbr

├── advanced-example-B_Cu.gbl

├── advanced-example-B_Fab.gbr

├── advanced-example-B_Mask.gbs

├── advanced-example-B_Paste.gbp

├── advanced-example-B_SilkS.gbo

├── advanced-example.drl

├── advanced-example-Edge_Cuts.gbr

├── advanced-example-F_Adhes.gta

├── advanced-example-F_CrtYd.gbr

├── advanced-example-F_Cu.gtl

├── advanced-example-F_Fab.gbr

├── advanced-example-F_Mask.gts

├── advanced-example-F_Paste.gtp

└── advanced-example-F_SilkS.gto
```

With kitspace.yaml containing:

<![if !supportLists]>· <![endif]>summary: A more advanced example

<![if !supportLists]>· <![endif]>site: https://example.com

<![if !supportLists]>· <![endif]>color: red

<![if !supportLists]>· <![endif]>bom: manufacture/advanced-example-BOM.tsv

<![if !supportLists]>· <![endif]>gerbers: manufacture/gerbers-and-drills

## Multiple Projects

Kitspace can also support multiple projects with one repository with the multi field as-well.

When multiple projects exist, multi will be the first field in the kitspace.yaml, always, and with the paths to your projects folder underneath it.

An example will look something like this:
```
├── kitspace.yaml

├── project_one

│  ├── 1-click-bom.tsv

│  ├── README.md

│  └── gerbers

│  ├── example.cmp

│  ├── example.drd

│  ├── example.dri

│  ...

│  ├── example.stc

│  └── example.sts

└── project_two

├── 1-click-bom.tsv

├── README.md

└── gerbers

├── example.cmp

├── example.drd

├── example.dri

...

├── example.stc

└── example.sts
```
And kitspace.yaml will contain:

<![if !supportLists]>· <![endif]>multi:

<![if !supportLists]>· <![endif]>project_one:

<![if !supportLists]>· <![endif]>summary: First project in a repository.

<![if !supportLists]>· <![endif]>color: blue

<![if !supportLists]>· <![endif]>site: https://example-one.com

<![if !supportLists]>· <![endif]>project_two:

<![if !supportLists]>· <![endif]>summary: Second project in a repository.

<![if !supportLists]>· <![endif]>color: red

<![if !supportLists]>· <![endif]>site: [https://example-two.com](https://example-two.com)

You can alos use custom paths for readme, bom and gerbers.

#References

- GitHub (https://github.com/kitspace/kitspace){:target="_blank"}