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

THIS IS A DRAFT

<!-- more -->

## Things to Do
1. Accumulate resources like datasheets, manuals, tutorials, and similar projects to serve as reference materials
2. Download and install the FPGA toolchain
3. Flash a pre-built bitstream of the "Hello World" Blinky project to verify that my computer can communicate with the ULX3S
4. Clone the Blinky project and run the synthesis, placing, and routing tools verify that HDL-to-bitstream generation works
5. Modify the speed or pattern of the blinking LED in the source code and re-upload to verify basic modifications work

### RTFM (Resources That Feel Miraculous)
- https://github.com/emard/ulx3s
- https://github.com/emard/ulx3s/blob/master/doc/MANUAL.md

### Toolchain
The first step in getting anything working on a dev board is to set up the toolchain. For FPGAs, this means:
* RTL Synthesizer for the Verilog HDL
* Optional formal verification tools
* Placing and routing
* Bitstream loader
* Simulator

Thankfully, there are now fully open options for everything and the [Yosys OSS CAD Suite](https://github.com/YosysHQ/oss-cad-suite-build) takes care of it all. Find the latest release of the tools [here](https://github.com/YosysHQ/oss-cad-suite-build/releases/latest) and download the appropriate package for your system. We'll be using a 64-bit Linux machine and so the following commands will be based on that platform. If you like ridiculous Bash one-liners, this one uses `curl`, `jq`, and `grep` to download the latest `linux-x64` build (based loosely on [this](https://smarterco.de/download-latest-version-from-github-with-curl/)): 

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
```verilog
o_led[5:0] <= ctr[23:18];
```
to 
```verilog
o_led[5:0] <= ctr[28:23];
```

video of it going really slow:

<video width="100%" controls muted>
  <source src="/ulx3s-blink-slow.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>