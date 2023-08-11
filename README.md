# Swirl
A Split keyboard with a thumb encoder on either side heavily inspired by the [helix](https://github.com/MakotoKurauchi/helix)

![image](https://github.com/vmorganp/swirl/assets/31448722/9350e84f-a610-44ec-b03f-c2fa4a79058a)

# ToDo
- diconnect the 2 pairs of inner pins on the trrs jack. both being ground causes a short circuit and requires modification of the TRRS jack at this time
    - I'm pretty sure there's something i2c related with this that you're *supposed* to do, but I don't actually understand that.
- Get the button part of the encoder in the appropriate col/row rather than being it's own direct connect key which is poorly supported in qmk


# Build Guide
## Ingredients
- 2x PCBs (Upload the zip from [here](./v0/ergogen_output/gerber.zip) to https://jlcpcb.com/ (the minimum order quantity is 5, maybe get six and share with a couple friends?)
- 2x Pro-micro or pro-micro-compatible microcontrollers (I like the elite pi from [here](https://www.littlekeyboards.com/products/elite-pi))
- 70x 1N4148 surface mounted diodes (SMD) like [these](https://www.diykeyboards.com/parts/product/p1n4148-smd-diodes-10pcs) (you actually only need 64, but they're almost always sold in 10s)
- 70x kailh choc v1 keyswitches of your choice like [these](https://www.littlekeyboards.com/collections/keyboard-switches/products/kailh-choc-low-profile-switches) (you actually only need 64, but they're almost always sold in 10s)
- 70x kailh choc v1 key caps of your choice like [these](https://www.littlekeyboards.com/collections/keycaps/products/mbk-choc-low-profile-keycaps?variant=39466488660035) (you actually only need 64, but they're almost always sold in 10s)
- 2x 3.5mm trrs headphone jack like [these](https://www.diykeyboards.com/parts/product/pj320a)
- 2x If you don't use the elite pi or have a will to do paperclip-resets, get some reset switches like [these](https://www.diykeyboards.com/parts/electronics/product/p3-5-x-6mm-vertical-tactile-microswitch)
- 2x EVQWGD001 roller encoder like [these](https://www.amazon.com/Encoder-Wheel-Switch-6-pin-EVQWGD001/dp/B0995GCFSX/ref=sr_1_2?keywords=EVQWGD001&sr=8-2) (please don't buy these on amazon, try ebay or something because these are wildly overpriced, but this link should be more stable than an ebay listing)
- Soldering tools
- Optionally, all of the hotswap stuff for your controllers and switches

## Hardware Steps
1. Bridge the microcontroller connections depending on your controller's orientation
    If you want the smooth side up, solder the bridges on the bottom, if you want the components (and the reset button on an eliete-pi) facing up, solder the bridges that face up
1. Solder SMDs (Ensure that the line on the SMD is on the same side of the connection as the line printed on the PCB)
1. Solder microcontroller
1. Solder TRRS connector
1. Solder key switches
1. Solder roller encoder

## Software Steps
Prerequisites
- Have qmk installed and setup, try the docs [here](https://docs.qmk.fm/#/newbs_getting_started) if you don't already have that setup

1. clone my qmk fork (maybe we get this merged into upstream at some point??)
`git clone git@github.com:vmorganp/qmk_firmware.git`

1. Compile and flash the firmware. (The default firmware is NOT good and I highly recommend creating your own)
    - Assuming you're using an elite-pi, compile the firmware using:
        1. qmk compile -kb swirl -km default -e CONVERT_TO=elite_pi`
        1. Drag and drop the compiled <filename>.uf2 file onto the pi

    - Otherwise:
        1. Run `qmk flash -kb swirl -km default`
        1. press the reset button/bridge the reset contact
        1. let it run

1. enjoy!

# Credits
@mrzealot and the other maintainers of ergogen

@ceoloide for having ergogen v4 footprints over in https://github.com/ceoloide/corney-island

@superfola on discord for helping me find me the reversible encoder footprint

@benvallack for informing me in a digestible way that this whole thing is actually doable

@imstubtw (i think) for the tutorial at https://flatfootfox.com/ergogen-part4-footprints-cases/

@aejay for the "swirl" text graphic [here](./graphics/swirl_text.svg)
