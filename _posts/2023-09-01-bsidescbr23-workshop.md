---
title: BSidesCBR23 Badge Add-on Workshop
date: 2023-08-31 00:30:00 -10
categories: []
tags: []
img_path: /assets/2023-09-01-bsidescbr23-workshop/
---

# Introduction

The goal of today's workshop is to design and assemble a printed circuit board (PCB) which takes the form of a magpie with a blinking eye. Once assembled, the add-on will plug into your badge and scare everyone within swooping distance whilst reminding them that [Birds Aren't Real](https://en.wikipedia.org/wiki/Birds_Aren%27t_Real).

![3d render of the final product](magpie_render.png)

By the end of the workshop you'll have learnt how to design a schematic and layout a PCB using KiCad, along with how to solder through hole and surface mount components.

# Let's Begin!

Before we dive into designing the PCB, we need to pick a CAD tool to use. Whilst there are online tools such as [Easy EDA](https://easyeda.com/), they are limited in capability due to running in a browser and if you continue to design PCBs after this workshop may run into limitations. As such we will be using [KiCad](https://www.kicad.org/), an extremely powerful and open source EDA tool, which will handle whatever you can throw at it.

If you have not already installed KiCad, please download it from [here](https://www.kicad.org/download/). We will be using version 7 in this workshop, but if you have version 6 the UI is similar enough you'll be able to follow without issue.

You will also need to download the [library](https://github.com/joshajohnson/sao-workshop/releases/tag/0.1) I have made for this workshop, as it contains custom symbols and most importantly the footprint to make our badge look like a magpie.

## KiCad Project Setup

Prior to starting the design, we need to make a new KiCad project and add the above downloaded library so we can use the symbols and footprints.

- Open KiCad.
- File -> New Project.
- Give your project a fun name and a place to live.

![new project window](new_project_window.png)

- Extract the [library](https://github.com/joshajohnson/sao-workshop/releases/tag/0.1) files to within your newly created project folder.
- Preferences -> Manage Symbol Libraries
- Change tab to "Project Specific Libraries"
- Click on the "folder" button, and select the `sao-workshop.kicad_sym` file you downloaded earlier.

![add symbol lib](add_symbol_lib.png)

- Preferences -> Manage Footprint Libraries
- Change tab to "Project Specific Libraries"
- Click on the "folder" button, and select the `sao-workshop.pretty` folder you downloaded earlier.

![add footprint lib](add_footprint_lib.png)

With the project setup and libraries added, are now ready to draw up the schematic.

# Schematic Capture

Schematic capture is the first step of the PCB design process, and involves drawing the circuit we want to design and defining what pins connect to each other. During this step we don't have to follow the laws of physics which allows us to rearrange pins, use net labels to connect signals, and split the design across multiple sheets on a big design to draw the design in a way which is easy to read and understand.

## KiCad Schematic Hotkeys Reference

| Shortcut | Function           |
|----------|--------------------|
| A        | Place (add) symbol |
| E        | Edit symbol        |
| M        | Move symbol        |
| R        | Rotate symbol      |

## Functional Description

For this workshop we'll be designing an [Astable 555 Timer](https://www.allaboutcircuits.com/tools/555-timer-astable-circuit/), which is a fancy way of toggling a pin (and in turn a LED) on and off forever. A Simplified version of the circuit we will be designing is shown below.

![simplified astable 555 timer circuit](astable-555.png)

By varying the values of R1, R2, and C, we can adjust the frequency (how fast the output toggles from high to low) and the duty cycle (percentage of time the pin is high in a given period). The maths to determine the components values for a 50% duty cycle is below.

```
f = sqrt(2)/(C1(R1 + 2R2))
  = 1.4/(1u(1K + 2*470K))
  = 1.5 Hz
``````

## Drawing the Schematic

- Press `A` to add a new part, and select the 555 timer from the `sao_workshop` library.

![adding 555 timer](add_555_timer.png)

- Press `A` again and add resistors (search `R`), capacitor (search `C`) and LED (search `LED`) arrange as shown below. To rotate the symbol, press `R` whilst dragging the symbol.

![components added](components_added.png)

- Double click on each symbol and update the component values as shown below. The "K" stands for KiloOhms (1000 Ohms), and the ”u” for microfarads (0.000001 Farads).

![components values added](component_values_added.png)

- With the components placed, we can add the power and ground symbols by pressing `A` then searching for `+3V3` and `GND`. 
  - "+3V3" and "GND" are magic symbols that put the battery voltage and ground anywhere on the board, and means you don’t have to run a wire to connect power/ground to every point on the schematic.

![adding 3V3 and GND symbols](add_power_ground.png)

- Finally, with all these components placed, use the wire `W` tool to connect all the pins as shown below.

![wiring up all the components](wired_up.png)

At this stage, we have the 555 timer all wired up, however we don't have a way of supplying it with power. Your bPod has a [SAO](https://hackaday.com/2019/03/20/introducing-the-shitty-add-on-v1-69bis-standard/) header on it which supplies the required 3V3 and GND connections, so let's use that.

- Add the SAO connector by opening the choose symbol (`A`) screen and searching `SAO`. Then add +3V3 and GND symbols as shown below.

![adding SAO connector](adding_sao.png)

With this done, we've got all the electrical components required to blink a LED. However we don't yet have the board in the shape of a magpie. As "magpie" isn't a schematic symbol, we'll add a dummy component which we will later assign to be the footprint of our magpie.

- Add a `Housing` to the schematic and rename it to `Outline`.

![adding placeholder magpie outline](housing_placeholder.png)

This concludes placing parts in the schematic, and we can start setting things up for layout.

## Annotation, Electrical Rules Check, Footprint Association

Currently our symbols are abstract objects that don't have unique IDs or footprints associated to them, two things which are required to lay out the PCB.

- Annotate the schematic (assign unique numbers to each component) using the below button.

![annotate schematic](annotate_schematic.png)

Once this is complete, you should have unique numbers on each component on the PCB.

![annotated schematic](annotated_sch.png)

We can now run Electrical Rules Check (ERC). ERC is a basic sanity check designed to find obvious issues such as pins which are not connected, two inputs connected to each other, or no power being provided to an IC, and it's a good rule to not start PCB layout until your schematic is clear of ERC errors.

- Run ERC from the menu shown below, and you should get 8 errors.

![running erc, with all the errors shown](erc_errors.png)

- Five of these errors are due to unconnected pins, and can be fixed by placing no-connection directives `Q` on the unconnected pins to tell KiCad they've been left disconnected by design.

Run ERC again, and you'll see two remaining errors for "Input Power pin not driven by any Output Power pins". This is KiCad complaining because the 555 timer has power pins, but we haven't told it the SAO header provides power, so it thinks the IC won't get any power to turn on.

![showing no-connect with two remaining erc errors](first_pass_erc.png)

- This issue can be fixed by placing `PWR_FLAG` on the 3V3 and GND nets to tell KiCad these nets are being driven by a power source.

![adding PWR_FLAG](pwr_flag.png)

With this last step, ERC shouldn't have any errors (it'll still have two warnings, but they'll be ignored for this workshop), and we can continue to footprint association.

![finalised schematic](final_sch.png)

A given part (e.g. 1K resistor) can come in many different physical form factors, from large through hole power resistors, to tiny surface mount resistors found in modern electronics. To keep the number of components in the KiCad library down, they don't make different symbols for each and every possible permutation, but instead get the designer to specify the footprint before moving onto PCB design.

- Using the footprint association tool, assign the correct footprints to the symbols as shown below. Note the `sao-workshop:magpie_outline` library may be located at the bottom of the list, not in alphabetical order.

![footprint association](fp_assoc.png)

With the footprint association complete, we are ready to continue onto the PCB layout step!

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