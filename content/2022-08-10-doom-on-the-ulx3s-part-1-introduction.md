+++
# Best practices from https://www.opengraph.xyz/: Keep title under 60 characters.
#        |----------------------------------------------------------|
title = "DOOM on the ULX3S Part 1: Introduction"

# Best practices from https://www.opengraph.xyz/: Keep description between 155 - 160 characters.
#              |---------------------------------------------------------------------------------------------------------------------------------------------------------|----|
description = "This is the first post in a series on running DOOM on the ULX3S FPGA using FOSS tools. This post outlines the goals and background of the project."

# Two formats are allowed: YYYY-MM-DD (2012-10-02) and RFC3339 (2002-10-02T15:00:00Z).
date = 2022-08-10
#updated = 2022-08-10

draft = false
in_search_index = true

[taxonomies]
    tags = ["fpga", "linux", "embedded", "riscv"]

# template = 
# weight = 
# slug = 
# path = 
# aliases = 
[extra]
    series = ["ulx3s-doom"]
+++

{{ figure(src="/cactus-doom.jpg",
          alt="A frame of DOOM carved into a cactus paddle"
          style="width: 100%;",
          position="center"
          caption_position="left",
          caption="A cactus can technically run DOOM, albeit with a pretty lousy frame rate (from Reddit)",
          caption_style="font-weight: bold; font-style: italic;") }}

In the embedded systems world, it's a right of passage for hackers to get a piece of hardware [to run DOOM](https://www.reddit.com/r/itrunsdoom/). I was recently rummaging around my box of development boards and I rediscovered my awesome [ULX3S](https://radiona.org/ulx3s/) which would be an awesome candidate for me to learn how to port DOOM. Not only is it a powerful dev board based around the [Lattice ECP5 FPGA](https://www.latticesemi.com/en/Products/FPGAandCPLD/ECP5), but thanks to the amazing work of a huge community of people, it also has a [fully open-source toolchain](https://github.com/YosysHQ/oss-cad-suite-build) and a huge ecosystem of compatible gateware. Time to meet our DOOM.

<!-- more -->

## FPGAs Are Pretty Neat (Especially This One)

If you aren't already familiar, one of my favorite ways of explaining the difference between a [processor](https://en.wikipedia.org/wiki/Processor_(computing)) and a [field-programmable gate array](https://en.wikipedia.org/wiki/Field-programmable_gate_array) is this:

> A processor executes code - it is provided instructions which tell it what to _do_. An FPGA implements digital logic - it is provided a circuit description which tells it what to _become_.

This is a profound philosophical distinction. This means that we can use a hardware description language (HDL) like [Verilog](https://en.wikipedia.org/wiki/Verilog) or [Amaranth](https://amaranth-lang.org/docs/amaranth/latest/) to describe a processor, a communication bus, or any other digital circuit and the FPGA will reconfigure itself to function as that circuit.

So not only are FPGAs powerful by themselves, they can be made even more powerful with additional hardware. In addition to the ECP5, the ULX3S in this project also sports:
* 32MB SDRAM
* HDMI port (called GPDI or General-Purpose Differential Interface for licensing reasons)
* Audio jack
* Buttons, switches, & LEDs
* A bunch of GPIO
* FLASH memory
* A whole ESP32 module for Bluetooth and WiFi
* [Lots more](https://radiona.org/ulx3s/#features)

There are several other [DOOM-on-FPGA](https://www.youtube.com/watch?v=3ZBAZ5QoCAk) projects out in the wild, even one [that implements the game in gateware (no CPU)](https://twitter.com/sylefeb/status/1258808333265514497?s=20), and another that uses a [custom processor instruction set architecture](https://github.com/mbitsnbites/mc1-doom). My goal with this was to learn how to get all the way from the logic gates all the way to running applications in Linux only using open source tools. That's `FPGA -> SoC -> Bootloader -> OS -> DOOM` all with FOSS tooling. Maybe one day I'll even run it on [open-source silicon](https://skywater-pdk.readthedocs.io/en/main/).

## Planning to Plan

I'm breaking the project up into a few milestones to make sure that I have the tools set up correctly and that I can tweak things at the various layers without everything breaking. This is important because each piece relies on the pieces below it to function. The plan is thus:

1. FPGA
    1. Accumulate resources like datasheets, manuals, tutorials, and similar projects to serve as reference materials
    2. Download and install the FPGA toolchain
    3. Flash a pre-built bitstream of the "Hello World" Blinky project to verify that my computer can communicate with the ULX3S
    4. Clone the Blinky project and run the synthesis, placing, and routing tools verify that HDL-to-bitstream generation works
    5. Modify the speed or pattern of the blinking LED in the source code and re-upload to verify basic modifications work
2. System-on-a-Chip
	1. Research SoC options for running Linux on an FPGA
	2. Download and flash pre-built SoC bitstream
	3. Clone design files, build bitstream, and flash to FPGA
	4. Explore source code and make a small modification to the design before building and uploading again
3. Binary interface, bootloader, root FS, & OS
	1. Download and transfer via serial port pre-built SBI, root filesystem, and Linux system with included bootloader. Verify Linux is running.
	2. Clone source projects for each of the above. Build the items, and transfer them to the FPGA
	3. Explore source code and make a small modification to the design before building and uploading again. Also speed up the transfer process since the default method is very slow.
4. Graphics on Linux
	1. Investigate the ways to support graphics in embedded Linux and the ULX3S
	2. Choose a solution and try to find pre-built binaries to test with
	3. Clone necessary projects and build the graphics stack necessary to run Doom
6. DOOM
	1. Get a WAD file
	2. Clone Chocolate DOOM
	3. Build it natively and/or cross-compile it
	4. Play DOOM