---
title: BSidesCBR23 Badge Add-on Workshop
date: 2023-08-31 00:30:00 -10
categories: []
tags: []
img_path: /assets/2023-09-01-bsidescbr23-workshop/
---

# Introduction

The goal of today's workshop is to design and assemble a printed circuit board (PCB) which takes the form of a magpie with a blinking eye. Once assembled, the add-on will plug into your badge and scare everyone within swooping distance whilst reminding them that [Birds Aren't Real](https://en.wikipedia.org/wiki/Birds_Aren%27t_Real).

By the end of the workshop you'll have learnt how to design a schematic and layout a PCB using KiCad, along with how to solder through hole and surface mount components.

# Let's Begin!

Before we dive into designing the PCB, we need to pick a CAD tool to use. Whilst there are online tools such as [Easy EDA](https://easyeda.com/), they are limited in capability due to running in a browser and if you continue to design PCBs after this workshop may run into limitations. As such we will be using [KiCad](https://www.kicad.org/), an extremely powerful and open source EDA tool, which will handle whatever you can throw at it.

If you have not already installed KiCad, please download it from [here](https://www.kicad.org/download/). We will be using version 7 in this workshop, but if you have version 6 the UI is similar enough you'll be able to follow without issue. 

You will also need to download the [library](TODO) I have made for this workshop, as it contains custom symbols and most importantly the footprint to make our badge look like a magpie.

## KiCad Project Setup

Prior to starting the design, we need to make a new KiCad project and add the above downloaded library so we can use the symbols and footprints.

TODO: Insert project setup and library addition here

# Schematic Capture

Schematic capture is the first step of the PCB design process, and involves drawing the circuit we want to design and defining what pins connect to each other. During this step we don't have to follow the rules of physics which allows us to rearrange pins, use net labels to connect signals, and split the design across multiple sheets on a big design to draw the design in a way which is easy to read and understand.

## KiCad Schematic Hotkeys Reference

TODO: Insert table of keyboard shortcuts here

## Functional Description

For this workshop we'll be designing an [Astable 555 Timer](https://www.allaboutcircuits.com/tools/555-timer-astable-circuit/), which is a fancy way of toggling a pin (and in turn a LED) on and off forever. A Simplified version of the circuit we will be designing is shown below.

![simplified astable 555 timer circuit](astable-555.png)

By varying the values of R1, R2, and C, we can adjust the frequency (how fast the output toggles from high to low) and the duty cycle (percentage of time the pin is high in a given period). 

TODO: Insert maths here of how we picked the values

## Drawing the Schematic

## Footprint Association

# PCB Layout

During schematic capture we told KiCad how we wanted to connect the components together. In layout, KiCad uses this information to assist us to make the connections whilst ensuring we follow the rules of physics this time. It's like a big game of connect the dots!

## KiCad PCB Hotkeys Reference

## PCB Layers

## Import Schematic

## Define Board Outline

## Placing Components

## Adding Traces and Vias

## Exporting Gerbers and Ordering PCBs

# PCB Assembly

## Surface Mount Components

## Though Hole Components

## Smoke Test