+++
# Best practices from https://www.opengraph.xyz/: Keep title under 60 characters.
#        |----------------------------------------------------------|
title = "DOOM on the ULX3S Part 2: FPGA Setup and Testing"

# Best practices from https://www.opengraph.xyz/: Keep description between 155 - 160 characters.
#              |---------------------------------------------------------------------------------------------------------------------------------------------------------|----|
description = "This is the second post in a series on running DOOM on the ULX3S FPGA using FOSS tools. It outlines the setup for the FPGA using the Yosys OSS CAD Suite."

# Two formats are allowed: YYYY-MM-DD (2012-10-02) and RFC3339 (2002-10-02T15:00:00Z).
date = 2022-08-11
#updated = 2022-08-11

draft = true
in_search_index = true

#[taxonomies]
#    tags = ["fpga", "linux", "embedded", "riscv"]
    #categories = ["tech"]
    #series = ["ulx3s-doom"]

# template = 
# weight = 
# slug = 
# path = 
# aliases = 
[extra]
#    series = ["ulx3s-doom"]
+++

> “Begin at the beginning," the King said, very gravely, "and go on till you come to the end: then stop.”
>
> --<cite>Lewis Carroll, _Alice in Wonderland_</cite>

The first item in our hit parade of DOOM is making sure we can work with the "code" described by the hardware description languages used on the ULX3S FPGA. This involves the following processes:

<!-- more -->

## FPGA Build Process

### Synthesis

The HDL typically describes a digital circuit at an abstraction level called the RTL, or [register transfer level](https://semiengineering.com/knowledge_centers/eda-design/definitions/register-transfer-level/). This describes the functional behavior of a design, but doesn't generally communicate how that design is implemented on a particular FPGA. The synthesizer takes the RTL and translates it into a netlist. The netlist is a model of the FPGA's internal cells and primitives like [flip-flops](https://en.wikipedia.org/wiki/Flip-flop_(electronics)), [RAM](https://en.wikipedia.org/wiki/Random-access_memory) and [lookup tables (LUTs)](https://en.wikipedia.org/wiki/Lookup_table). We'll be using [Yosys](https://github.com/YosysHQ/yosys) in this project.

<a href="https://www.plantuml.com/plantuml/uml/LP5FJuGm4CNl_HIJFUbXyGjio1wCyR3n8Dx900CqwHyo7OXe_EuEJQnwWBxc_JfzBxqcGPRLE-De5908RATPOB1ClTWOZEcH1pXTklhrxGPDNBadUBAE4jmzFzxkBmzTVG9CmEAw-0wV1c1K6qvzN8CGjnknTN6gjepfhX1Zykqs3wxINpPrBUQAB6rQR41t84q6qX8AG3Atw94no5mjU_RHi_aovWYFONAKWpUx4fJi1t59c_Q_rLv8d4sIUnKaaFmlvFTsq35JgDJwGOxhj1ESptKUgXMArhH5e_zbz3jqFcwk58RZ0Opv1W00">
{{ image(src="plantuml-synthesis.png", alt="The synthesizer reads RTL source files as input and produces a netlist file.", position="center", style="border-radius: 8px;") }}
</a>

### Formal Verification (Optional)

[Formal verification](https://en.wikipedia.org/wiki/Formal_verification) is a subdiscipline of FPGA design which uses a solver program to mathematically prove the correctness of a particular design. I don't know how to do formal verification yet, and so will be skipping this step, but I know that it can be very useful. One use case is detecting obscure, unintended edge-cases that could break the design or introduce security vulnerabilities, but may be hard to detect or reproduce with simulation alone.

<a href="https://testbench4u.com/2017/05/29/formal-verification-questions/">
{{ image(src="formal-verification.png", alt="The synthesizer reads RTL source files as input and produces a netlist file.", position="center", style="border-radius: 8px;") }}
</a>

### Simulation (Optional)
Simulation allows you to inject "fake" input signals into a design using something called a testbench, and run the hardware in a simulated environment to see how the internal signals behave. This is extremely helpful in debugging since you can "see inside" the design and perform the `write -> build -> test` loop way faster and with more insight than if you worked exclusively with real hardware. I'm skipping this step in this tutorial, however, since we'll be using designs that are presumably pre-tested and already work.

### Placing & Routing
Since digital circuits take up real physical space inside an FPGA or [ASIC](https://en.wikipedia.org/wiki/Application-specific_integrated_circuit), P&R tools take the netlist file from the synthesizer and determines if/how all the components of the design can be arranged inside the physical device. Onced placed, the tools then determine the most efficient way to route data and power to each of the components, and connect signals to the metal pins on the IC package. Assuming everything fit and nothing broke, the router produces a bitstream file to load to the FPGA. We'll be using [Nextpnr](https://github.com/YosysHQ/nextpnr) in this project.

### Bitstream Loading
Once a bitstream file is produced, it needs to be loaded onto the physical hardware. The loader will read the bitstream and transfer it into the configuration memory of the FPGA which can be either the internal SRAM of the FPGA or a SPI FLASH chip on the dev board. The ECP5 has an FTDI  care of the interfacing with the dev board 

With that background out of the way, let's get to it and set up the [Yosys OSS CAD Suite](https://github.com/YosysHQ/oss-cad-suite-build).

## RTFM (Resources That Facilitate Miracles)
Reading and writing documentation is mission critical to the success of any moderately complex project. Here are a few resources that make understanding and debugging these tools much more pleasant:
- [The Official ULX3S Repository](https://github.com/emard/ulx3s)
- [The Official ULX3S Manual](https://github.com/emard/ulx3s/blob/master/doc/MANUAL.md)
- [prjtrellis - the ECP5 bitstream reverse engineering project](https://github.com/YosysHQ/prjtrellis)
- [Lattice ECP5 Documentation](https://www.latticesemi.com/en/Products/FPGAandCPLD/ECP5#_11D625E1D2C7406C96A5312C93FF0CBD)
- [Yosys OSS CAD Suite Repository](https://github.com/YosysHQ/oss-cad-suite-build)
- [A post by gojimmypi from a few years ago describing a similar project](https://gojimmypi.github.io/risc-v-on-ulx3s-with-litex/) 

## Yosys OSS CAD Suite

The first step in getting anything working on a dev board is to set up the toolchain. For FPGAs, this means:
* RTL Synthesizer for the Verilog HDL
* Optional formal verification tools
* Placing and routing
* Bitstream loader
* Simulator

Thankfully, there are now fully open options for everything and the 

 takes care of it all. Find the latest release of the tools [here](https://github.com/YosysHQ/oss-cad-suite-build/releases/latest) and download the appropriate package for your system. We'll be using a 64-bit Linux machine and so the following commands will be based on that platform. If you like ridiculous Bash one-liners, this one uses `curl`, `jq`, and `grep` to download the latest `linux-x64` build (based loosely on [this](https://smarterco.de/download-latest-version-from-github-with-curl/)): 

```bash
curl -L -o oss-cad-suite-linux-x64-latest.tgz \
"$(curl -s https://api.github.com/repos/YosysHQ/oss-cad-suite-build/releases/latest \
| jq .assets[].browser_download_url \
| grep linux-x64 \
| cut -d '"' -f 2)"
```

Extract the file: 
```bash
tar -zxvf oss-cad-suite-linux-x64-latest.tgz
```

And finally, set up the environment:
```bash
export PATH="<extracted_location>/oss-cad-suite/bin:$PATH"
```
or
```bash
source <extracted_location>/oss-cad-suite/environment
```

See the OSS CAD Suite [README](https://github.com/YosysHQ/oss-cad-suite-build#installation) for more info.

### Blinky
```bash
git clone https://github.com/ulx3s/blink.git
cd blink
fujprog blink_85f.bit
```
Video of it going really fast:

<video width="100%" controls muted>
  <source src="/ulx3s-blink-fast.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>


slow it down. Edit blinky.v line 30 and change 
```SystemVerilog
o_led[5:0] <= ctr[23:18];
```
to 
```SystemVerilog
o_led[5:0] <= ctr[28:23];
```

video of it going really slow:

<video width="100%" controls muted>
  <source src="/ulx3s-blink-slow.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>