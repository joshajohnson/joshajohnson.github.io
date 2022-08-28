---
title: Intro Keyboard Assembly Instructions
date: 2022-08-27 00:00:00 -10
categories: []
tags: []
img_path: /assets/2022-08-28-intro-keyboard/
---

## Introduction 

Building an DIY keyboard consists of three main components: soldering, mechanical assembly, and programming. The goal of this workshop is to provide an introduction to the above so you feel confident tackling a larger project of your own.

![finished product](48_final_product.jpg)

By the end of the workshop you should be walking away with a keyboard consisting off three keys and a rotary encoder, that you've programmed to perform any task you can imagine. This could span from a simple volume knob, to dedicated copy / paste keys, or even typing the entire bee movie script with one keypress.

## Soldering

### Required Parts

Before starting, ensure you have all the below components on hand.

- 1 x Sea-Picro
- 1 x PCB
- 2 x 12 pin headers
- 4 x Diodes (through hole or surface mount)
- 3 x WS2812 LEDs
- 1 x Reset Button
- 3 x Keyswitches and keycaps
- 1 x Rotary encoder

![required parts](0_parts_required.jpg)

You will also require the following tools.

- Soldering iron
- Solder
- Tweezers
- Flush cut side cutters

### Soldering Tips

The most important thing to remember with soldering is that the solder flows to wherever is hot. As such it's important to heat up the components you are trying to solder before feeding solder into the joint. A rough rule of thumb is to hold your iron against the components for a second before feeding solder **into the component being soldered, not the iron**. This will ensure the solder sticks to the parts you are trying to attach to the circuit board, and not just pool up on the iron.

### Reset Switch

The first step to assembling the board is to solder the reset switch, which is commonly used to put the board into bootloader mode so you can flash different firmware / keymaps to the microcontroller. The board we are using [Sea-Picro]({% post_url 2022-08-03-sea-picro %}) already has a reset button on it so this step is not required, but is good practice none the less.

First, put a small amount of solder onto one of the pads.
![tin rst pin](1_tin_rst.jpg)

Then using tweezers, place the reset switch in position and melt the solder you previously placed down to tack the reset switch in place.
![tack rst in pos](2_tack_rst.jpg)

Add solder to the remaining pins to secure the reset switch in place.
![solder reset pins](3_solder_rst.jpg)

### LEDs

Adding LEDs to your board is a simple way of adding some colour to your desk, but it can also be used to identify the state of your keyboard, e.g. if it's setup for macros or volume control. The LEDs used are known as "addressable LEDs" in that you send a serial sting of data to the LEDs to set their colour. As a result they can be a bit challenging to solder, so don't hesistate to ask for help.

Simiarly to the reset switch, tin one pad of the LED.
![tin led pin](4_tin_led.jpg)

Line up the white triangular marking in the corner of the LED with the "L" shaped corner of the marking on the PCB. **This is crucial otherwise your board won't work**.
![check orientation](6_align_led.jpg)

As with the reset switch, heat up the previously placed solder and tack the LED in place.
![tack led in place](7_tack_led.jpg)

Then solder the remaining pins. You may find the pin with the "L" shape more challenging to solder, and this is due to it being the ground plane which has a large thermal mass. If you get a blob of solder stuck to the LED like below, ensure you hold the iron to the PCB for a few seconds before adding solder.
![poor gnd conn](9_poor_led_joint.jpg)

Here is a video showing the entire process.
{% include youtube_embed.html id="uSRfHFco2eg" %}

Once you've soldered the first LED, continue doing the other two on the board until they are complete.
![all leds done](12_all_led_assembled.jpg)

### Diodes

On a normal keyboard, diodes are used to prevent an effect known as "ghosting", where the microcontroller thinks more keys are pressed than actually are when specific key combinations are pressed. You will see them in two different package types, a glass tube with leads (through hole) and a black rectangle with small pads (surface mount). This kit allows you to pick and choose what package you want depending on how challenging you want it to be.

### Through Hole Diodes

We first need to bend the leads on the diode to be the same width as the holes in the PCB.
![bend leads](13_tht_diode_bend_align.jpg)

Then insert it, ensuring the black bar on the diode is aligned with the white bar on the PCB.
![insert](14_tht_diode_insert.jpg)

To hold it in place whilst soldering, flip the board over and bend the leads outwards.
![bend leads](15_bend_diode_legs.jpg)

Solder one of the leads.
![solder one lead](16_solder_leg.jpg)

Flip the board back over and check the diode is still flush with the PCB, if not heat up the joint and move into position.
![check flush](17_check_flat.jpg)

With the diode in place, solder the remaining lead.
![solder other lead](18_solder_remaining.jpg)

Finally, trim the leads using the flush cut side cutters.
![trim leads](19_trim_legs.jpg)

### Surface Mount Diodes

Like the through hole diodes, the surface mount diodes are directional and won't work if installed backwards. They have a horizonal line on one end of the package which lines up with the line on the PCB. This can sometimes be hard to see, but shining light from the side of the package will help reveal the marking.
![diode marking](20_smd_diode_align.jpg)

As we have done previously, add solder to one pad.
![tin pad](21_smd_diode_tin.jpg)

Then ensuring the component is in the correct orientation, tack one pin in place.
![tack one end](22_smd_diode_tack.jpg)

Then solder the reminaing pin in place.
![solder final pin](23_smd_diode_solder.jpg)

Finish soldering all four diodes, and you'll have a board that looks like the below. (You can pick and choose through hole vs surface mount depending on how much of a challenge you are seeking.)
![all diodes done](26_diodes_done.jpg)

### Microcontroller

The microcontroller is the brains of any keyboard, with it scanning for key presses, figuring out what key was pressed, then sending the relavent keypress up to the computer all in a fraction of a second. A RP2040 based board, Sea-Picro, was chosen for this project as it can be programmed in python without installing a toolchain and has good supply even during the chip shortage.

We first need to solder the pin headers to the microcontroller, and can use the PCB to keep the pins aligned as shown below. The pin header is one pin shorter than the IO on Sea-Picro, leave the empty pin at the USB connector end as shown in red. Solder the pins at the end of each header.
![pin headers](27_solder_headers.png)

With the headers tacked in place, confirm the pins are square to the microcontroller. If they are not, heat up one of the solder joints, and gently push the connector into alignment. Make sure you don't touch the pin you are heating up otherwise you'll burn yourself! 
![checking pins square](29_sp_check_square.jpg)

Once the pins are square solder all of the pins. (sorry for the blurry photo)
![solder all pins](30_solder_headers.png)

With all the pins soldered on Sea-Picro, flip the board upside down and tack two opposing corners in place on the PCB.
![tack bottom pins](31_solder_headers_bottom.png)

If Sea-Picro isn't sitting fush to the PCB, heat up a pin and adjust as nessessary.
![align pins](31_5_aligning_pins.png)

With the microcontroller sitting flush to the PCB, solder the remaining pins. (forgot to photograph this step)

With all the pins soldered, snip off the legs so they don't stick out.
![trim headers](32_sp_snip_underneath.jpg)

### Switches

Switches are argueably the most important part of a keyboard, as without them you wouldn't be able to type anything! They come in a variety of options with different force profiles, but regardless of what switch you pick the install process is the same.

First, grab a switch and place it in the position you want. Rememeber we are fitting a rotary encoder as well so consider where you want that to live as it's much taller than a switch. In this case, I'm installing switches in 1,2,3, and an encoder in 0.
![place switch](35_insert_switch.jpg)

With the switch pressed into place, flip the board over and solder the pins in. Repeat for the other two switches.
![solder switch](36_solder_switch.png)

### Encoders

In addition to the encoders switch that shorts two pins when pressed, the encoder has two additional outputs that go high / low as the knob is turned, sending the direction of rotation to the microcontroller. They are a great way to control continuous values such as volume or opacity.

The first step is to snip both mounting legs off the encoder with the side cutters.
![snip legs](38_snip_leg.jpg)

With the legs removed, insert the encoder into the PCB and tack opposing pins in place. Don't solder all the pins yet.
![solder two pins](40_tack_pins.jpg)

With the pins tacked into place, ensure the encoder is sitting flush / square on the board, and adjust as nessessary. When square, solder the remaining pins.
![check square](40_5_check_square.jpg)

With all of the encoder pins soldered, install the keycaps and knob, and celebrate finishing the soldering of your new keyboard!
![elec done](41_final_product.jpg)

## Mechanical Assembly

With the electronics done, it's time to assemble the case. Check you have the below before continuing.

- 1 x Acrylic base
- 4 x M2 standoffs
- 8 x M2 bolts
- 4 x Bumpons

![mech parts](42_mech_required.jpg)

Start by removing the protective paper off the acrylic base.
![remove paper](43_peel.jpg)

Grab a screw and standoff, and screw into one of the holes in the acrylic.
![install standoff](44_thread_standoff.jpg)

Repeat for all four corners.
![all corners](45_all_installed.jpg)

Using a 1.5mm allen key, screw the PCB to the standoffs with the remaining screws.
![top screw install](46_top_screws.jpg)

Finally, add the bumpons to four corners of the acrylic.
![add bumpons](47_add_feed.jpg)

Now it's time to sit back and enjoy all of your hard work, as you've successfully assembled your new keyboard and can begin programming it.
![assembled unit](48_final_product.jpg)

## Software Configuration