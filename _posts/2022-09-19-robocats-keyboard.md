---
title: Robcats Keyboard Workshop Assembly Instructions
date: 2022-09-19 00:00:00 -10
categories: []
tags: []
img_path: /assets/2022-08-28-intro-keyboard/
---

## Introduction 

The goal of today's workshop is to provide an introduction to soldering and programming through building a small mechanical keyboard. By the end of the workshop you should have a keyboard consisting off three keys and a rotary encoder that you can program to perform any task you can imagine. This could span from a simple volume knob, to dedicated copy / paste keys, or even typing the entire bee movie script with one keypress.

![finished product](48_final_product.jpg)

## Soldering
 
### Required Parts

We will be using the below components during today's workshop, and will be handed out as you get to each step.

- 1 x Sea-Picro (1)
- 1 x PCB (2)
- 2 x 12 pin headers (3)
- 4 x Diodes (through hole (4) or surface mount (5))
- 3 x Keyswitches (6) and keycaps (7)
- 1 x Rotary encoder (8) and knob (9)

The LEDs (10) will be pre soldered, and the reset switch (11) is not required.

![required parts](0_parts_required_robocats.jpg)

You will also require the following tools.

- Soldering iron
- Solder
- Tweezers
- Flush cut side cutters

### Soldering Tips

The most important thing to remember with soldering is that the solder flows to wherever is hot. As such it's important to heat up the components you are trying to solder before feeding solder into the joint. A rough rule of thumb is to hold your iron against the components for a second before feeding solder **into the component being soldered, not the iron**. This will ensure the solder sticks to the parts you are trying to attach to the circuit board, and not just pool up on the iron.

Here is a short video showing how to solder, with the first 15 seconds demoing the above instructions.
{% include youtube_embed.html id="BsF9A7xBRP0" %}

### Diodes

On a normal keyboard, diodes are used to prevent an effect known as "ghosting", where the microcontroller thinks more keys are pressed than actually are when specific key combinations are pressed. You will see diodes in two different package types, a glass tube with leads (through hole) and a black rectangle with small pads (surface mount). If you've never soldered before I'd suggest using the through hole diodes, however if you are after a challenge the surface mount option is also available.

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

Finally, trim the leads using the flush cut side cutters. Please point the side cutters towards the desk when cutting so the leads don't go flying around the room.
![trim leads](19_trim_legs.jpg)

### Surface Mount Diodes

Like through hole diodes, surface mount diodes are directional and won't work if installed backwards. They have a horizontal line on one end of the package which lines up with the line on the PCB. This can sometimes be hard to see, but shining light from the side of the package will help reveal the marking.
![diode marking](20_smd_diode_align.jpg)

As we have done previously, add solder to one pad.
![tin pad](21_smd_diode_tin.jpg)

Then ensuring the component is in the correct orientation, tack one pin in place.
![tack one end](22_smd_diode_tack.jpg)

Then solder the remaining pin in place.
![solder final pin](23_smd_diode_solder.jpg)

Finish soldering all four diodes, and you'll have a board that looks like the below. (You can pick and choose through hole vs surface mount depending on how much of a challenge you are seeking.)
![all diodes done](26_diodes_done.jpg)

### Microcontroller

The microcontroller is the brains of any keyboard, with it scanning for key presses, figuring out what key was pressed, then sending the relavent keypress up to the computer all in a fraction of a second. A RP2040 based board, Sea-Picro, was chosen for this project as it can be programmed in python without installing a toolchain and has good supply even during the chip shortage.

We first need to solder the pin headers to the microcontroller, and can use the PCB to keep the pins aligned as shown below. The pin header is one pin shorter than the IO on Sea-Picro, please leave the empty pin at the USB connector end as shown in red. Solder the pins at the end of each header.
![pin headers](27_solder_headers.png)

With the headers tacked in place, confirm the pins are square to the microcontroller. If they are not, heat up one of the solder joints, and gently push the connector into alignment. Make sure you don't touch the pin you are heating up otherwise you'll burn yourself! 
![checking pins square](29_sp_check_square.jpg)

Once the pins are square solder all of the pins. (sorry for the blurry photo)
![solder all pins](30_solder_headers.png)

With all the pins soldered on Sea-Picro, ensure it's placed on the same side as the diodes with the USB connector facing towards the edge of PCB as per the above photo. 

**Please ask a mentor to confirm the orientation is correct, as if it's incorrect your board will not work!**

With Sea-Picro oriented correctly, flip the board upside down and tack two opposing corners in place on the PCB.
![tack bottom pins](31_solder_headers_bottom.png)

If Sea-Picro isn't sitting flush to the PCB, heat up a pin and adjust as necessary.
![align pins](31_5_aligning_pins.png)

With the microcontroller sitting flush to the PCB, solder the remaining pins. (forgot to photograph this step)

With all the pins soldered, snip off the legs so they don't stick out. Please take care so the pins don't go flying around the room.
![trim headers](32_sp_snip_underneath.jpg)

### Switches

Switches are arguably the most important part of a keyboard, as without them you wouldn't be able to type anything! They come in a variety of options with different force profiles, but regardless of what switch you pick the install process is the same.

First, grab a switch and place it in the position you want. Remember we are fitting a rotary encoder as well so consider where you want that to live as it's much taller than a switch. In this case, I'm installing switches in 1,2,3, and an encoder in 0.
![place switch](35_insert_switch.jpg)

With the switch pressed into place, flip the board over and solder the pins in. Repeat for the other two switches.
![solder switch](36_solder_switch.png)

### Encoders

In addition to the push button/switch in the encoder that shorts two pins when pressed, the encoder has two additional outputs that go high / low as the knob is turned, sending the direction of rotation to the microcontroller. As such you can turn the encoder for as many revolutions as you'd like, so they are a great way to control continuous values such as volume or opacity.

The first step is to snip both mounting legs off the encoder with the side cutters.
![snip legs](38_snip_leg.jpg)

With the legs removed, insert the encoder into the PCB and tack opposing pins in place. Don't solder all the pins yet.
![solder two pins](40_tack_pins.jpg)

With the pins tacked into place, ensure the encoder is sitting flush / square on the board, and adjust as necessary. When square, solder the remaining pins.
![check square](40_5_check_square.jpg)

With all of the encoder pins soldered, install the keycaps and knob, and celebrate finishing the soldering of your new keyboard!
![elec done](41_final_product.jpg)

## Firmware Configuration

Out of the box, Sea-Picro (and the RP2040 microcontroller within) has no idea what it's purpose in life is, so we need to configure it to not only be a keyboard, but one which works with our custom made PCB, and your custom keycodes. To do this, we will be using [KMK](http://kmkfw.io/docs/Getting_Started/), a [CircuitPython](https://www.adafruit.com/circuitpython) based keyboard firmware framework, due to it's ease of programming - all you need to do it edit a text file and when you save the code it will run.

To make programming easier, please install [Mu](https://learn.adafruit.com/welcome-to-circuitpython/installing-mu-editor), which is the recommended editor for CircuitPython and has an inbuilt serial terminal which allows us to talk to your keyboard for debugging purposes.

Sea-Picro comes flashed with CircuitPython out of the box, but we need to load KMK and the `code.py` file with our keyboard configuration. The steps are below:

1. Download a [copy of KMK](https://github.com/KMKfw/kmk_firmware/archive/refs/heads/master.zip).
2. Unzip it and copy the KMK folder and the `boot.py` file at the root of the USB drive corresponding to your board (often appearing as CIRCUITPY).
3. Unplug and replug your device to force the `boot.py` changes to be implemented.
4. Using Mu, open the existing `code.py` file on the CIRCUITPY drive and replace it with the below code.

```python
# Sea-Picro pinout
import board

# KMK drivers
from kmk.kmk_keyboard import KMKKeyboard
from kmk.scanners.keypad import KeysScanner
from kmk.modules.encoder import EncoderHandler
from kmk.extensions.RGB import RGB, AnimationModes

# Different keycodes that can be sent
from kmk.keys import KC
from kmk.extensions.media_keys import MediaKeys
from kmk.handlers.sequences import send_string
from kmk.handlers.sequences import unicode_string_sequence
from kmk.handlers.sequences import simple_key_sequence

# Init keyboard
keyboard = KMKKeyboard()

# Mapping IO pin to position in matrix
# Comment lines in / out depending if you are using diodes or not
# keyboard.matrix = KeysScanner([board.D21, board.D23, board.D20, board.D22,]) # Without diodes
keyboard.matrix = KeysScanner([board.D29, board.D28, board.D27, board.D26,]) # With diodes

# Add encoders, RGB, and media key support to keyboard
encoder_handler = EncoderHandler()
rgb_ext = RGB(pixel_pin=board.D7, num_pixels=3, val_limit=255, val_default=64, animation_mode=AnimationModes.RAINBOW,)
media_keys = MediaKeys()
keyboard.modules = [encoder_handler, media_keys, rgb_ext]

# Configure encoder pins
# As the encoder can be placed in multiple spots we don't define which IO the
# push button is mapped to, and instead leave that for the switch matrix definition
encoder_handler.pins = ((board.D9, board.D8, None, False),)

# Examples of different keys that can be sent
# All valid keys: https://github.com/KMKfw/kmk_firmware/blob/master/docs/keycodes.md#keys-overview
# Strings: https://github.com/KMKfw/kmk_firmware/blob/master/docs/sequences.md#sending-strings
EG_STRING = send_string("According to all known laws of aviation, there is no way a bee should be able to fly. Its wings are too small to get its fat little body off the ground.")
# Unicode (requires config on your PC first) https://github.com/KMKfw/kmk_firmware/blob/master/docs/sequences.md#unicode
EG_UNICODE = unicode_string_sequence('(っ◔◡◔)っ ❤')
# Chains of key presses
EG_COPY = KC.LCTL(KC.C)
EG_PASTE = KC.LCTL(KC.V)

# This is where we control what keys are sent when a switch is pressed
keyboard.keymap = [
    [
        KC.MPLY, EG_STRING, EG_COPY, EG_PASTE
    ]
]

# Below configures what happens when the encoder is turned
encoder_handler.map = (((KC.VOLD, KC.VOLU, None),),)

# With everything configured, time to become a keyboard!
if __name__ == '__main__':
    keyboard.go()
```
Press the keys / turn the encoder on your keyboard and see if they all work. By default they will work as below.

- SW0 / Encoder: Media Play / Pause
- SW3: Prints the first line of the Bee movie script.
- SW2: Copy
- SW3: Paste
- Encoder Clockwise: Volume Up
- Encoder Anticlockwise: Volume Down

If you have issues, check the diodes are installed in the correct orientation and all pins are soldered. Just incase you have issues with the diodes, there is a "no diode" IO configuration on line 22 that can be commented in to check if the diodes are the issue or if it exists somewhere else.

Assuming everything is working, it's time to jump to [mechanical assembly](#mechanical-assembly) and attach the base before returning here to configure the keyboard to send whatever keycodes you want. Below are a few links to KMK documentation to help guide you.

- There's a [reference](https://github.com/KMKfw/kmk_firmware/blob/master/docs/keycodes.md#keys-overview) of the available keycodes.
- [International](https://github.com/KMKfw/kmk_firmware/blob/master/docs/international.md#international-keycodes) extension adds keys for non US layouts and [Media Keys](https://github.com/KMKfw/kmk_firmware/blob/master/docs/media_keys.md#media-keys) adds keys for ... media.

And to go even further:
- [Sequences](https://github.com/KMKfw/kmk_firmware/blob/master/docs/sequences.md#sequences) are used for sending multiple keystrokes in a single action.
- [Layers](https://github.com/KMKfw/kmk_firmware/blob/master/docs/layers.md#layers) can transform the whole way your keyboard is behaving with a single touch.
- [ModTap](https://github.com/KMKfw/kmk_firmware/blob/master/docs/modtap.md#modtap-keycodes) allow you to customize the way a key behaves whether it is tapped or hold, and [TapDance](https://github.com/KMKfw/kmk_firmware/blob/master/docs/tapdance.md#tap-dance) depending on the number of times it is pressed.
- [RGB](https://github.com/KMKfw/kmk_firmware/blob/master/docs/rgb.md#keycodes) allows you to control addressable LEDs.

If you make a change and notice your board is no longer working, there is a good chance there is a bug somewhere that is preventing the code from running. If this is the case, the onboard RGB LED will blink a [error code](https://learn.adafruit.com/welcome-to-circuitpython/troubleshooting#circuitpython-7-dot-0-0-and-later-2978455) that corresponds to the below.


- 1 GREEN blink: Code finished without error.
- 2 RED blinks: Code ended due to an exception. Check the serial console for details.
- 3 YELLOW blinks: CircuitPython is in safe mode. No user code was run. Check the serial console for safe mode reason.

## Mechanical Assembly

With the electronics done, it's time to assemble the case. Check you have the below before continuing.

- 1 x Acrylic base
- 4 x M2 standoffs
- 8 x M2 bolts
- 4 x Bumpons
- 1.5mm hex/allen key

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
![add bumpons](47_add_feet.jpg)

Now it's time to sit back and enjoy all of your hard work, as you've successfully assembled your new keyboard and can begin programming it.
![assembled unit](48_final_product.jpg)

## Programming Challenges

With all the above done, you should have a fully functioning keyboard whose function is only limited by your imagination (and the rules of physics). If there is time left in the workshop, please play around with the code and configure it's functionality to things you find interesting. 

If you'd like some ideas, give the below a go:

- Configure keys to change the colour of the RGB LEDs. [Hint](#hint-change-colour-rgb), [Answer](#answer-change-colour-rgb).
- Set the encoder to change the LED brightness when you turn it. [Hint](#hint-encoder-brightness-change), [Answer](#answer-encoder-brightness-change).
- Configure one key to press `CTRL + L`, another to type the RoboCats website URL, and a third to press enter, allowing you to visit the RoboCats website quickly (when pressed within a web browser). [Hint](#hint-visit-robocats-website), [Answer](#answer-visit-robocats-website).
- Combine the above into a single key press. [Hint](#hint-robocats-website-single-key), [Answer](#answer-robocats-website-single-key).
- Write a function that types `3`, waits a second, `2`, waits a second, `1`, waits a second, then types `Liftoff!`. [Hint](#hint-3-2-1-liftoff), [Answer](#answer-3-2-1-liftoff).
- Use a tool such as [TextKool](https://textkool.com/en/ascii-art-generator) to generate fancy `RoboCats` text and type it with one key press. [Hint](#hint-fancy-robocats-text), [Answer](#answer-fancy-robocats-text).
- Print the below ASCII art of Shrek to the Mu serial terminal with a single key press. [Hint](#hint-shrek-print), [Answer](#answer-shrek-print).
```
⢀⡴⠑⡄⠀⠀⠀⠀⠀⠀⠀⣀⣀⣤⣤⣤⣀⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠸⡇⠀⠿⡀⠀⠀⠀⣀⡴⢿⣿⣿⣿⣿⣿⣿⣿⣷⣦⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠑⢄⣠⠾⠁⣀⣄⡈⠙⣿⣿⣿⣿⣿⣿⣿⣿⣆⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢀⡀⠁⠀⠀⠈⠙⠛⠂⠈⣿⣿⣿⣿⣿⠿⡿⢿⣆⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⢀⡾⣁⣀⠀⠴⠂⠙⣗⡀⠀⢻⣿⣿⠭⢤⣴⣦⣤⣹⠀⠀⠀⢀⢴⣶⣆
⠀⠀⢀⣾⣿⣿⣿⣷⣮⣽⣾⣿⣥⣴⣿⣿⡿⢂⠔⢚⡿⢿⣿⣦⣴⣾⠁⠸⣼⡿
⠀⢀⡞⠁⠙⠻⠿⠟⠉⠀⠛⢹⣿⣿⣿⣿⣿⣌⢤⣼⣿⣾⣿⡟⠉⠀⠀⠀⠀⠀
⠀⣾⣷⣶⠇⠀⠀⣤⣄⣀⡀⠈⠻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⠀⠀⠀⠀⠀⠀
⠀⠉⠈⠉⠀⠀⢦⡈⢻⣿⣿⣿⣶⣶⣶⣶⣤⣽⡹⣿⣿⣿⣿⡇⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠉⠲⣽⡻⢿⣿⣿⣿⣿⣿⣿⣷⣜⣿⣿⣿⡇⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿⣿⣷⣶⣮⣭⣽⣿⣿⣿⣿⣿⣿⣿⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⣀⣀⣈⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠇⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠃⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠹⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⠟⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠉⠛⠻⠿⠿⠿⠿⠛⠉
```

## Hints

### Hint: Change Colour RGB

- Check out the [RGB Key Codes](https://github.com/KMKfw/kmk_firmware/blob/master/docs/rgb.md#keycodes).
- You'll need to put the board into plain mode, then use Hue to adjust the colour. This can be done by altering the keymap.

### Hint: Encoder Brightness Change

- This is very similar to the colour change problem above, except you want to change the brightness (Value) and map those keycodes to the encoder.

### Hint: Visit RoboCats Website

- In the example code we have this keycode `EG_COPY = KC.LCTL(KC.C)`, which presses `CTRL + C` to copy.
- Try modifying this to press `CTRL + L` instead, and update the name from `EG_COPY` to something more relevant.
- Then try modifying the `send_string` example to print the RoboCats URL `https://www.melbournerobocats.com/`.
- You might notice that after the URL is typed we need to press enter, so add that to your keymap as well.

### Hint: RoboCats Website Single Key

- We will use [Key Sequences](https://github.com/KMKfw/kmk_firmware/blob/master/docs/sequences.md#key-sequences) to press keys in sequence.
- Look at the example `simple_key_presses` at the above link and modify it to use the keycodes we made earlier.
- You'll need to define this sequence below the keycodes you want to use.


### Hint: 3 2 1 Liftoff!

- We can use the `simple_key_presses` per the previous challenge, but will need to add `KC.MACRO_SLEEP_MS(1000)` in between steps to delay by 1 second.
- To make the text appear on a new line each time, you can either use `KC.ENTER` as a keycode, or add a newline `\n` to the end of a string.

### Hint: Fancy RoboCats Text

- As we've seen in the previous challenge, we can use `send_string` in a sequence to print multiple lines of text.
- We need to ensure we only use a font that uses standard keycodes, for example the one I've generated below:
```
 _____   ____  ____   ____   _____       _______ _____ 
|  __ \ / __ \|  _ \ / __ \ / ____|   /\|__   __/ ____|
| |__) | |  | | |_) | |  | | |       /  \  | | | (___  
|  _  /| |  | |  _ <| |  | | |      / /\ \ | |  \___ \ 
| | \ \| |__| | |_) | |__| | |____ / ____ \| |  ____) |
|_|  \_\\____/|____/ \____/ \_____/_/    \_\_| |_____/ 
```
- If we copy and paste each line of the above text into a separate `send_string` command, we should be able to print the text one line at a time.
- We'll either need to add a newline `\n` or `KC.ENTER` at the end of each string to ensure it prints on multiple lines.

### Hint: Shrek Print

- This problem is a challenging one, as the picture of Shrek uses characters that you can't type on a keyboard, so we can't send keycodes as we've done above.
- We can however send it over the serial terminal to Mu, where we can then copy and paste it to a text editor on your PC.
- The KMK developers have this as an example, so scroll to the bottom of [this page](https://github.com/KMKfw/kmk_firmware/blob/master/docs/keys.md) and give it a go.
- You'll need to open the Mu serial terminal to see the work of art be printed out.

## Answers

### Answer: Change Colour RGB

- We will use the [RGB Key Codes](https://github.com/KMKfw/kmk_firmware/blob/master/docs/rgb.md#keycodes) to adjust the LEDs.
- Once we find the keycodes we want to use, we can update the keymap with the new codes.
- `KC.RGB_MODE_PLAIN` will be used to change the animation mode from rainbow to plain, as otherwise the Hue codes are not acted upon.
- KMK uses HSV (Hue, Saturation, Value) for colour control, and Hue is how we adjust colour. Add the `KC.HUI` (Hue Increase) and `KC.HUD` (Hue Decrease) keycodes into the keymap.
- With the keymap updated (see below), tap the `PLAIN` key, then you can use the `HUI` and `HUD` keys to adjust the colour.

```python
keyboard.keymap = [
    [
        KC.MPLY, KC.RGB_MODE_PLAIN, KC.RGB_HUI, KC.RGB_HUD
    ]
]

```

### Answer: Encoder Brightness Change

- As above, we will use the [RGB Key Codes](https://github.com/KMKfw/kmk_firmware/blob/master/docs/rgb.md#keycodes), but update the encoder keymap instead of the keyboard switch keymap.
- Value is the HSV equivalent of Brightness, so `KC.RGB_VAI` and `KC.RGB_VAD` are the keycodes we will use.
- Updating the encoder keymap with these for clockwise / anticlockwise as shown below should get us the desired result.
- If the value increases when you turn anticlockwise (and you want it to decrease), swap the location of the two keycodes.

```python
encoder_handler.map = (((KC.RGB_VAD, KC.RGB_VAI, None),),)
```

### Answer: Visit RoboCats Website

- We can modify the `EG_COPY = KC.LCTL(KC.C)` line to `URL = KC.LCTL(KC.L)`, which will move your cursor to the URL bar in your browser.
- Similarly, editing the string example `EG_STRING = send_string("According ...")` to `ROBO_URL = send_string("https://www.melbournerobocats.com/")` will type out the URL.
- We then need to add `KC.ENTER` to our keymap so we can press enter after typing out the URL.

```python
URL = KC.LCTL(KC.L)
ROBO_URL = send_string("https://www.melbournerobocats.com/")

# This is where we control what keys are sent when a switch is pressed
keyboard.keymap = [
    [
        KC.MPLY, URL, ROBO_URL, KC.ENTER
    ]
]
```

### Answer: RoboCats Website Single Key

- Using [Key Sequences](https://github.com/KMKfw/kmk_firmware/blob/master/docs/sequences.md#key-sequences) we can press the keys we defined in the last challenge all in one go.
- If we enter the keycodes we made in the previous challenge into the example linked above, it will look something like the below.
- Adding `ROBO_URL_SINGLE` to our keymap will then allow us to trigger this sequence.

```python
URL = KC.LCTL(KC.L)
ROBO_URL = send_string("https://www.melbournerobocats.com/")

ROBO_URL_SINGLE = simple_key_sequence(
    (
        URL,
        ROBO_URL,
        KC.ENTER,
    )
)

# This is where we control what keys are sent when a switch is pressed
keyboard.keymap = [
    [
        ROBO_URL_SINGLE, URL, ROBO_URL, KC.ENTER
    ]
]
```

### Answer: 3 2 1 Liftoff!

- We will use [Key Sequences](https://github.com/KMKfw/kmk_firmware/blob/master/docs/sequences.md#key-sequences) as we did in the previous challenge to solve this.
- You can either type `1 2 3` using the keycodes, or send them as a string, but will need to type `Liftoff!` as a string.
- We will press `KC.ENTER` after typing each key, and append a newline to the `Liftoff!` string.
- Between each step `KC.MACRO_SLEEP_MS(1000)` will be called to create a delay. The function accepts a time in milliseconds (thousandths of a second) so we will pass 1000 to get a one second delay.

```python
LIFTOFF = simple_key_sequence(
    (
        KC.N3,
        KC.ENTER,
        KC.MACRO_SLEEP_MS(1000),
        KC.N2,
        KC.ENTER,
        KC.MACRO_SLEEP_MS(1000),
        send_string("1\n"),
        KC.MACRO_SLEEP_MS(1000),
        send_string("LIFTOFF!\n"),
    )
)

# This is where we control what keys are sent when a switch is pressed
keyboard.keymap = [
    [
        LIFTOFF, URL, ROBO_URL, KC.ENTER
    ]
]
```

### Answer: Fancy RoboCats Text

- As explained in the hint, we will use multiple `send_string` functions to print each line of the text.
- We need to append a `\n` or `KC.ENTER` to the end of each line to ensure they print on a new line each time.
- One possible solution is shown below.

```python
FANCY_ROBO = simple_key_sequence(
    (
        send_string(" _____   ____  ____   ____   _____       _______ _____ \n"),
        send_string("|  __ \ / __ \|  _ \ / __ \ / ____|   /\|__   __/ ____|\n"),
        send_string("| |__) | |  | | |_) | |  | | |       /  \  | | | (___  \n"),
        send_string("|  _  /| |  | |  _ <| |  | | |      / /\ \ | |  \___ \ \n"),
        send_string("| | \ \| |__| | |_) | |__| | |____ / ____ \| |  ____) |\n"),
        send_string("|_|  \_\\____/|____/ \____/ \_____/_/    \_\_| |_____/ \n"),
    )
)

# This is where we control what keys are sent when a switch is pressed
keyboard.keymap = [
    [
        FANCY_ROBO, URL, ROBO_URL, KC.ENTER
    ]
]
```

### Answer: Shrek Print

- First, we copy and paste the example code from the [KMK example](https://github.com/KMKfw/kmk_firmware/blob/master/docs/keys.md) to our code. Place above the keymap.
- Looking at the code, we can see when we press `LALT` it will call the `shrek` function that prints the image.
- As such, if we add the `KC.LALT` keycode to our keymap, it should print Shrek whenever Left Alt is pressed.
- We then need to open Mu and go to the serial terminal to see the picture be printed.
- Once it's been printed, you can copy and paste it in whatever text editor / messaging platform you like.

```python
def shrek(*args, **kwargs):
    print('⢀⡴⠑⡄⠀⠀⠀⠀⠀⠀⠀⣀⣀⣤⣤⣤⣀⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀')
    print('⠸⡇⠀⠿⡀⠀⠀⠀⣀⡴⢿⣿⣿⣿⣿⣿⣿⣿⣷⣦⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀')
    print('⠀⠀⠀⠀⠑⢄⣠⠾⠁⣀⣄⡈⠙⣿⣿⣿⣿⣿⣿⣿⣿⣆⠀⠀⠀⠀⠀⠀⠀⠀')
    print('⠀⠀⠀⠀⢀⡀⠁⠀⠀⠈⠙⠛⠂⠈⣿⣿⣿⣿⣿⠿⡿⢿⣆⠀⠀⠀⠀⠀⠀⠀')
    print('⠀⠀⠀⢀⡾⣁⣀⠀⠴⠂⠙⣗⡀⠀⢻⣿⣿⠭⢤⣴⣦⣤⣹⠀⠀⠀⢀⢴⣶⣆')
    print('⠀⠀⢀⣾⣿⣿⣿⣷⣮⣽⣾⣿⣥⣴⣿⣿⡿⢂⠔⢚⡿⢿⣿⣦⣴⣾⠁⠸⣼⡿')
    print('⠀⢀⡞⠁⠙⠻⠿⠟⠉⠀⠛⢹⣿⣿⣿⣿⣿⣌⢤⣼⣿⣾⣿⡟⠉⠀⠀⠀⠀⠀')
    print('⠀⣾⣷⣶⠇⠀⠀⣤⣄⣀⡀⠈⠻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇⠀⠀⠀⠀⠀⠀')
    print('⠀⠉⠈⠉⠀⠀⢦⡈⢻⣿⣿⣿⣶⣶⣶⣶⣤⣽⡹⣿⣿⣿⣿⡇⠀⠀⠀⠀⠀⠀')
    print('⠀⠀⠀⠀⠀⠀⠀⠉⠲⣽⡻⢿⣿⣿⣿⣿⣿⣿⣷⣜⣿⣿⣿⡇⠀⠀⠀⠀⠀⠀')
    print('⠀⠀⠀⠀⠀⠀⠀⠀⢸⣿⣿⣷⣶⣮⣭⣽⣿⣿⣿⣿⣿⣿⣿⠀⠀⠀⠀⠀⠀⠀')
    print('⠀⠀⠀⠀⠀⠀⣀⣀⣈⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠇⠀⠀⠀⠀⠀⠀⠀')
    print('⠀⠀⠀⠀⠀⠀⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠃⠀⠀⠀⠀⠀⠀⠀⠀')
    print('⠀⠀⠀⠀⠀⠀⠀⠹⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⠟⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀')
    print('⠀⠀⠀⠀⠀⠀⠀⠀⠀⠉⠛⠻⠿⠿⠿⠿⠛⠉')

    return False # Returning True will follow thru the normal handlers sending the ALT key to the OS
KC.LALT.before_press_handler(shrek)

# This is where we control what keys are sent when a switch is pressed
keyboard.keymap = [
    [
        KC.LALT, KC.RGB_MODE_PLAIN, KC.RGB_HUI, KC.RGB_HUD
    ]
]
```