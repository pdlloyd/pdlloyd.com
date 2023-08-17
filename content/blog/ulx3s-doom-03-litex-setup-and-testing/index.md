+++
# Best practices from https://www.opengraph.xyz/: Keep title under 60 characters.
#        |----------------------------------------------------------|
title = "DOOM on the ULX3S Part 3: LiteX Setup and Testing"

# Best practices from https://www.opengraph.xyz/: Keep description between 155 - 160 characters.
#              |---------------------------------------------------------------------------------------------------------------------------------------------------------|----|
description = "This is the second post in a series on running DOOM on the ULX3S FPGA using FOSS tools. It outlines the toolchain setup for the RISCV-based SoC using LiteX."

# Two formats are allowed: YYYY-MM-DD (2012-10-02) and RFC3339 (2002-10-02T15:00:00Z).
date = 2022-08-12
#updated = 2022-08-12

draft = true
in_search_index = true

#[taxonomies]
#    tags = ["fpga", "linux", "embedded", "riscv"]

# template = 
# weight = 
# slug = 
# path = 
# aliases = 
#[extra]
#    series = ["ulx3s-doom"]
+++

THIS IS A DRAFT

<!-- more -->

set up litex
https://gojimmypi.github.io/risc-v-on-ulx3s-with-litex/

set up linux-litex
https://github.com/litex-hub/linux-on-litex-vexriscv

fix sbt
https://github.com/sbt/sbt/issues/6558
```
⦗OSS CAD Suite⦘ [user@mariner linux-on-litex-vexriscv]$ ./make.py --board=ulx3s --device=LFE5U-85F --build
INFO:ECP5PLL:Creating ECP5PLL.
INFO:ECP5PLL:Registering Single Ended ClkIn of 25.00MHz.
INFO:ECP5PLL:Creating ClkOut0 sys of 50.00MHz (+-10000.00ppm).
INFO:ECP5PLL:Creating ClkOut1 sys_ps of 50.00MHz (+-10000.00ppm).
INFO:ECP5PLL:Creating ECP5PLL.
INFO:ECP5PLL:Registering Single Ended ClkIn of 25.00MHz.
INFO:ECP5PLL:Creating ClkOut0 hdmi of 25.00MHz (+-0.00ppm).
INFO:ECP5PLL:Creating ClkOut1 hdmi5x of 125.00MHz (+-0.00ppm).
INFO:SoC:        __   _ __      _  __  
INFO:SoC:       / /  (_) /____ | |/_/  
INFO:SoC:      / /__/ / __/ -_)>  <    
INFO:SoC:     /____/_/\__/\__/_/|_|  
INFO:SoC:  Build your hardware, easily!
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Creating SoC... (2022-07-28 23:43:17)
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:FPGA device : LFE5U-85F-6BG381C.
INFO:SoC:System clock: 50.000MHz.
INFO:SoCBusHandler:Creating Bus Handler...
INFO:SoCBusHandler:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoCBusHandler:Adding reserved Bus Regions...
INFO:SoCBusHandler:Bus Handler created.
INFO:SoCCSRHandler:Creating CSR Handler...
INFO:SoCCSRHandler:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoCCSRHandler:Adding reserved CSRs...
INFO:SoCCSRHandler:CSR Handler created.
INFO:SoCIRQHandler:Creating IRQ Handler...
INFO:SoCIRQHandler:IRQ Handler (up to 32 Locations).
INFO:SoCIRQHandler:Adding reserved IRQs...
INFO:SoCIRQHandler:IRQ Handler created.
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Initial SoC:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoC:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoC:IRQ Handler (up to 32 Locations).
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Controller ctrl added.
INFO:SoC:CPU vexriscv_smp added.
INFO:SoC:CPU vexriscv_smp adding IO Region 0 at 0x80000000 (Size: 0x80000000).
INFO:SoCBusHandler:io0 Region added at Origin: 0x80000000, Size: 0x80000000, Mode: RW, Cached: False Linker: False.
INFO:SoC:CPU vexriscv_smp overriding sram mapping from 0x01000000 to 0x10000000.
INFO:SoC:CPU vexriscv_smp setting reset address to 0x00000000.
INFO:SoC:CPU vexriscv_smp adding Bus Master(s).
INFO:SoCBusHandler:cpu_bus0 added as Bus Master.
INFO:SoC:CPU vexriscv_smp adding Interrupt(s).
INFO:SoC:CPU vexriscv_smp adding SoC components.
INFO:SoCCSRHandler:uart CSR added at Location 2.
INFO:SoCCSRHandler:timer0 CSR added at Location 3.
INFO:SoCIRQHandler:uart IRQ added at Location 0.
INFO:SoCIRQHandler:timer0 IRQ added at Location 1.
INFO:SoCBusHandler:opensbi Region added at Origin: 0x40f00000, Size: 0x00080000, Mode: RW, Cached: True Linker: True.
INFO:SoCBusHandler:plic Region added at Origin: 0xf0c00000, Size: 0x00400000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:plic added as Bus Slave.
INFO:SoCBusHandler:clint Region added at Origin: 0xf0010000, Size: 0x00010000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:clint added as Bus Slave.
INFO:SoCBusHandler:rom Region added at Origin: 0x00000000, Size: 0x00010000, Mode: R, Cached: True Linker: False.
INFO:SoCBusHandler:rom added as Bus Slave.
INFO:SoC:RAM rom added Origin: 0x00000000, Size: 0x00010000, Mode: R, Cached: True Linker: False.
INFO:SoCRegion:Region size rounded internally from 0x00001800 to 0x00002000.
INFO:SoCBusHandler:sram Region added at Origin: 0x10000000, Size: 0x00001800, Mode: RW, Cached: True Linker: False.
INFO:SoCBusHandler:sram added as Bus Slave.
INFO:SoC:RAM sram added Origin: 0x10000000, Size: 0x00001800, Mode: RW, Cached: True Linker: False.
INFO:SoCIRQHandler:uart IRQ added at Location 0.
INFO:SoCIRQHandler:timer0 IRQ added at Location 1.
INFO:SoCBusHandler:main_ram Region added at Origin: 0x40000000, Size: 0x02000000, Mode: RW, Cached: True Linker: False.
INFO:SoCBusHandler:main_ram added as Bus Slave.
INFO:SoCBusHandler:sdblock2mem added as Bus Master.
INFO:SoCBusHandler:sdmem2block added as Bus Master.
INFO:SoCIRQHandler:sdirq IRQ allocated at Location 2.
INFO:SoC:CSR Bridge csr added.
INFO:SoCBusHandler:csr Region added at Origin: 0xf0000000, Size: 0x00010000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:csr added as Bus Slave.
INFO:SoCCSRHandler:csr added as CSR Master.
INFO:SoCBusHandler:Interconnect: InterconnectShared (3 <-> 6).
INFO:SoCCSRHandler:ctrl CSR allocated at Location 0.
INFO:SoCCSRHandler:identifier_mem CSR allocated at Location 1.
INFO:SoCCSRHandler:leds CSR allocated at Location 4.
INFO:SoCCSRHandler:sdblock2mem CSR allocated at Location 5.
INFO:SoCCSRHandler:sdcore CSR allocated at Location 6.
INFO:SoCCSRHandler:sdirq CSR allocated at Location 7.
INFO:SoCCSRHandler:sdmem2block CSR allocated at Location 8.
INFO:SoCCSRHandler:sdphy CSR allocated at Location 9.
INFO:SoCCSRHandler:sdram CSR allocated at Location 10.
INFO:SoCCSRHandler:video_framebuffer CSR allocated at Location 11.
INFO:SoCCSRHandler:video_framebuffer_vtg CSR allocated at Location 12.
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Finalized SoC:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:32-bit wishbone Bus, 4.0GiB Address Space.
IO Regions: (1)
io0                 : Origin: 0x80000000, Size: 0x80000000, Mode: RW, Cached: False Linker: False
Bus Regions: (7)
rom                 : Origin: 0x00000000, Size: 0x00010000, Mode: R, Cached: True Linker: False
sram                : Origin: 0x10000000, Size: 0x00001800, Mode: RW, Cached: True Linker: False
main_ram            : Origin: 0x40000000, Size: 0x02000000, Mode: RW, Cached: True Linker: False
opensbi             : Origin: 0x40f00000, Size: 0x00080000, Mode: RW, Cached: True Linker: True
csr                 : Origin: 0xf0000000, Size: 0x00010000, Mode: RW, Cached: False Linker: False
clint               : Origin: 0xf0010000, Size: 0x00010000, Mode: RW, Cached: False Linker: False
plic                : Origin: 0xf0c00000, Size: 0x00400000, Mode: RW, Cached: False Linker: False
Bus Masters: (3)
- cpu_bus0
- sdblock2mem
- sdmem2block
Bus Slaves: (6)
- plic
- clint
- rom
- sram
- main_ram
- csr
INFO:SoC:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
CSR Locations: (13)
- ctrl                  : 0
- identifier_mem        : 1
- uart                  : 2
- timer0                : 3
- leds                  : 4
- sdblock2mem           : 5
- sdcore                : 6
- sdirq                 : 7
- sdmem2block           : 8
- sdphy                 : 9
- sdram                 : 10
- video_framebuffer     : 11
- video_framebuffer_vtg : 12
INFO:SoC:IRQ Handler (up to 32 Locations).
IRQ Locations: (3)
- uart   : 0
- timer0 : 1
- sdirq  : 2
INFO:SoC:--------------------------------------------------------------------------------
INFO:ECP5PLL:Config:
clki_div   : 1
clkfb      : 2
clko0_freq : 50.00MHz
clko0_div  : 8
clko0_phase: 0.00°
clko1_freq : 50.00MHz
clko1_div  : 8
clko1_phase: 90.00°
clko2_div  : 1
vco        : 400.00MHz
clkfb_div  : 16
INFO:ECP5PLL:Config:
clki_div   : 1
clkfb      : 2
clko0_freq : 25.00MHz
clko0_div  : 20
clko0_phase: 0.00°
clko1_freq : 125.00MHz
clko1_div  : 4
clko1_phase: 0.00°
clko2_div  : 1
vco        : 500.00MHz
clkfb_div  : 20
VexRiscv cluster : VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ood_Wm
Generating cluster netlist
java.lang.UnsupportedOperationException: The Security Manager is deprecated and will be removed in a future release
	at java.base/java.lang.System.setSecurityManager(System.java:416)
	at sbt.TrapExit$.installManager(TrapExit.scala:54)
	at sbt.StandardMain$.runManaged(Main.scala:187)
	at sbt.xMain$.$anonfun$run$8(Main.scala:102)
	at scala.util.DynamicVariable.withValue(DynamicVariable.scala:62)
	at scala.Console$.withIn(Console.scala:230)
	at sbt.internal.util.Terminal$.withIn(Terminal.scala:560)
	at sbt.internal.util.Terminal$.$anonfun$withStreams$1(Terminal.scala:350)
	at scala.util.DynamicVariable.withValue(DynamicVariable.scala:62)
	at scala.Console$.withOut(Console.scala:167)
	at sbt.internal.util.Terminal$.$anonfun$withOut$2(Terminal.scala:550)
	at scala.util.DynamicVariable.withValue(DynamicVariable.scala:62)
	at scala.Console$.withErr(Console.scala:196)
	at sbt.internal.util.Terminal$.withOut(Terminal.scala:550)
	at sbt.internal.util.Terminal$.withStreams(Terminal.scala:350)
	at sbt.xMain$.run(Main.scala:86)
	at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:104)
	at java.base/java.lang.reflect.Method.invoke(Method.java:577)
	at sbt.internal.XMainConfiguration.run(XMainConfiguration.scala:83)
	at sbt.xMain.run(Main.scala:46)
	at xsbt.boot.Launch$.$anonfun$run$1(Launch.scala:149)
	at xsbt.boot.Launch$.withContextLoader(Launch.scala:176)
	at xsbt.boot.Launch$.run(Launch.scala:149)
	at xsbt.boot.Launch$.$anonfun$apply$1(Launch.scala:44)
	at xsbt.boot.Launch$.launch(Launch.scala:159)
	at xsbt.boot.Launch$.apply(Launch.scala:44)
	at xsbt.boot.Launch$.apply(Launch.scala:21)
	at xsbt.boot.Boot$.runImpl(Boot.scala:78)
	at xsbt.boot.Boot$.run(Boot.scala:73)
	at xsbt.boot.Boot$.main(Boot.scala:21)
	at xsbt.boot.Boot.main(Boot.scala)
[error] [launcher] error during sbt launcher: java.lang.UnsupportedOperationException: The Security Manager is deprecated and will be removed in a future release
Traceback (most recent call last):
  File "./make.py", line 885, in <module>
    main()
  File "./make.py", line 858, in main
    builder.build(run=args.build, build_name=board_name)
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/litex/litex/soc/integration/builder.py", line 322, in build
    self.soc.finalize()
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/litex/litex/soc/integration/soc.py", line 1266, in finalize
    Module.finalize(self)
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/migen/migen/fhdl/module.py", line 156, in finalize
    subfragments = self._collect_submodules()
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/migen/migen/fhdl/module.py", line 149, in _collect_submodules
    r.append((name, submodule.get_fragment()))
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/migen/migen/fhdl/module.py", line 102, in get_fragment
    self.finalize()
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/migen/migen/fhdl/module.py", line 157, in finalize
    self.do_finalize(*args, **kwargs)
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/litex/litex/soc/cores/cpu/vexriscv_smp/core.py", line 484, in do_finalize
    self.add_sources(self.platform)
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/litex/litex/soc/cores/cpu/vexriscv_smp/core.py", line 355, in add_sources
    self.generate_netlist()
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/litex/litex/soc/cores/cpu/vexriscv_smp/core.py", line 263, in generate_netlist
    raise OSError('Failed to run sbt')
OSError: Failed to run sbt

```

Gotta downgrade to java-17
https://wiki.archlinux.org/title/Java#Switching_between_JVM

fix 
```
⦗OSS CAD Suite⦘ [user@mariner linux-on-litex-vexriscv]$ ./make.py --board=ulx3s --device=LFE5U-85F --build
INFO:ECP5PLL:Creating ECP5PLL.
INFO:ECP5PLL:Registering Single Ended ClkIn of 25.00MHz.
INFO:ECP5PLL:Creating ClkOut0 sys of 50.00MHz (+-10000.00ppm).
INFO:ECP5PLL:Creating ClkOut1 sys_ps of 50.00MHz (+-10000.00ppm).
INFO:ECP5PLL:Creating ECP5PLL.
INFO:ECP5PLL:Registering Single Ended ClkIn of 25.00MHz.
INFO:ECP5PLL:Creating ClkOut0 hdmi of 25.00MHz (+-0.00ppm).
INFO:ECP5PLL:Creating ClkOut1 hdmi5x of 125.00MHz (+-0.00ppm).
INFO:SoC:        __   _ __      _  __  
INFO:SoC:       / /  (_) /____ | |/_/  
INFO:SoC:      / /__/ / __/ -_)>  <    
INFO:SoC:     /____/_/\__/\__/_/|_|  
INFO:SoC:  Build your hardware, easily!
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Creating SoC... (2022-07-29 00:12:05)
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:FPGA device : LFE5U-85F-6BG381C.
INFO:SoC:System clock: 50.000MHz.
INFO:SoCBusHandler:Creating Bus Handler...
INFO:SoCBusHandler:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoCBusHandler:Adding reserved Bus Regions...
INFO:SoCBusHandler:Bus Handler created.
INFO:SoCCSRHandler:Creating CSR Handler...
INFO:SoCCSRHandler:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoCCSRHandler:Adding reserved CSRs...
INFO:SoCCSRHandler:CSR Handler created.
INFO:SoCIRQHandler:Creating IRQ Handler...
INFO:SoCIRQHandler:IRQ Handler (up to 32 Locations).
INFO:SoCIRQHandler:Adding reserved IRQs...
INFO:SoCIRQHandler:IRQ Handler created.
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Initial SoC:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:32-bit wishbone Bus, 4.0GiB Address Space.
INFO:SoC:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
INFO:SoC:IRQ Handler (up to 32 Locations).
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Controller ctrl added.
INFO:SoC:CPU vexriscv_smp added.
INFO:SoC:CPU vexriscv_smp adding IO Region 0 at 0x80000000 (Size: 0x80000000).
INFO:SoCBusHandler:io0 Region added at Origin: 0x80000000, Size: 0x80000000, Mode: RW, Cached: False Linker: False.
INFO:SoC:CPU vexriscv_smp overriding sram mapping from 0x01000000 to 0x10000000.
INFO:SoC:CPU vexriscv_smp setting reset address to 0x00000000.
INFO:SoC:CPU vexriscv_smp adding Bus Master(s).
INFO:SoCBusHandler:cpu_bus0 added as Bus Master.
INFO:SoC:CPU vexriscv_smp adding Interrupt(s).
INFO:SoC:CPU vexriscv_smp adding SoC components.
INFO:SoCCSRHandler:uart CSR added at Location 2.
INFO:SoCCSRHandler:timer0 CSR added at Location 3.
INFO:SoCIRQHandler:uart IRQ added at Location 0.
INFO:SoCIRQHandler:timer0 IRQ added at Location 1.
INFO:SoCBusHandler:opensbi Region added at Origin: 0x40f00000, Size: 0x00080000, Mode: RW, Cached: True Linker: True.
INFO:SoCBusHandler:plic Region added at Origin: 0xf0c00000, Size: 0x00400000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:plic added as Bus Slave.
INFO:SoCBusHandler:clint Region added at Origin: 0xf0010000, Size: 0x00010000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:clint added as Bus Slave.
INFO:SoCBusHandler:rom Region added at Origin: 0x00000000, Size: 0x00010000, Mode: R, Cached: True Linker: False.
INFO:SoCBusHandler:rom added as Bus Slave.
INFO:SoC:RAM rom added Origin: 0x00000000, Size: 0x00010000, Mode: R, Cached: True Linker: False.
INFO:SoCRegion:Region size rounded internally from 0x00001800 to 0x00002000.
INFO:SoCBusHandler:sram Region added at Origin: 0x10000000, Size: 0x00001800, Mode: RW, Cached: True Linker: False.
INFO:SoCBusHandler:sram added as Bus Slave.
INFO:SoC:RAM sram added Origin: 0x10000000, Size: 0x00001800, Mode: RW, Cached: True Linker: False.
INFO:SoCIRQHandler:uart IRQ added at Location 0.
INFO:SoCIRQHandler:timer0 IRQ added at Location 1.
INFO:SoCBusHandler:main_ram Region added at Origin: 0x40000000, Size: 0x02000000, Mode: RW, Cached: True Linker: False.
INFO:SoCBusHandler:main_ram added as Bus Slave.
INFO:SoCBusHandler:sdblock2mem added as Bus Master.
INFO:SoCBusHandler:sdmem2block added as Bus Master.
INFO:SoCIRQHandler:sdirq IRQ allocated at Location 2.
INFO:SoC:CSR Bridge csr added.
INFO:SoCBusHandler:csr Region added at Origin: 0xf0000000, Size: 0x00010000, Mode: RW, Cached: False Linker: False.
INFO:SoCBusHandler:csr added as Bus Slave.
INFO:SoCCSRHandler:csr added as CSR Master.
INFO:SoCBusHandler:Interconnect: InterconnectShared (3 <-> 6).
INFO:SoCCSRHandler:ctrl CSR allocated at Location 0.
INFO:SoCCSRHandler:identifier_mem CSR allocated at Location 1.
INFO:SoCCSRHandler:leds CSR allocated at Location 4.
INFO:SoCCSRHandler:sdblock2mem CSR allocated at Location 5.
INFO:SoCCSRHandler:sdcore CSR allocated at Location 6.
INFO:SoCCSRHandler:sdirq CSR allocated at Location 7.
INFO:SoCCSRHandler:sdmem2block CSR allocated at Location 8.
INFO:SoCCSRHandler:sdphy CSR allocated at Location 9.
INFO:SoCCSRHandler:sdram CSR allocated at Location 10.
INFO:SoCCSRHandler:video_framebuffer CSR allocated at Location 11.
INFO:SoCCSRHandler:video_framebuffer_vtg CSR allocated at Location 12.
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:Finalized SoC:
INFO:SoC:--------------------------------------------------------------------------------
INFO:SoC:32-bit wishbone Bus, 4.0GiB Address Space.
IO Regions: (1)
io0                 : Origin: 0x80000000, Size: 0x80000000, Mode: RW, Cached: False Linker: False
Bus Regions: (7)
rom                 : Origin: 0x00000000, Size: 0x00010000, Mode: R, Cached: True Linker: False
sram                : Origin: 0x10000000, Size: 0x00001800, Mode: RW, Cached: True Linker: False
main_ram            : Origin: 0x40000000, Size: 0x02000000, Mode: RW, Cached: True Linker: False
opensbi             : Origin: 0x40f00000, Size: 0x00080000, Mode: RW, Cached: True Linker: True
csr                 : Origin: 0xf0000000, Size: 0x00010000, Mode: RW, Cached: False Linker: False
clint               : Origin: 0xf0010000, Size: 0x00010000, Mode: RW, Cached: False Linker: False
plic                : Origin: 0xf0c00000, Size: 0x00400000, Mode: RW, Cached: False Linker: False
Bus Masters: (3)
- cpu_bus0
- sdblock2mem
- sdmem2block
Bus Slaves: (6)
- plic
- clint
- rom
- sram
- main_ram
- csr
INFO:SoC:32-bit CSR Bus, 32-bit Aligned, 16.0KiB Address Space, 2048B Paging, big Ordering (Up to 32 Locations).
CSR Locations: (13)
- ctrl                  : 0
- identifier_mem        : 1
- uart                  : 2
- timer0                : 3
- leds                  : 4
- sdblock2mem           : 5
- sdcore                : 6
- sdirq                 : 7
- sdmem2block           : 8
- sdphy                 : 9
- sdram                 : 10
- video_framebuffer     : 11
- video_framebuffer_vtg : 12
INFO:SoC:IRQ Handler (up to 32 Locations).
IRQ Locations: (3)
- uart   : 0
- timer0 : 1
- sdirq  : 2
INFO:SoC:--------------------------------------------------------------------------------
INFO:ECP5PLL:Config:
clki_div   : 1
clkfb      : 2
clko0_freq : 50.00MHz
clko0_div  : 8
clko0_phase: 0.00°
clko1_freq : 50.00MHz
clko1_div  : 8
clko1_phase: 90.00°
clko2_div  : 1
vco        : 400.00MHz
clkfb_div  : 16
INFO:ECP5PLL:Config:
clki_div   : 1
clkfb      : 2
clko0_freq : 25.00MHz
clko0_div  : 20
clko0_phase: 0.00°
clko1_freq : 125.00MHz
clko1_div  : 4
clko1_phase: 0.00°
clko2_div  : 1
vco        : 500.00MHz
clkfb_div  : 20
VexRiscv cluster : VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ood_Wm
Generating cluster netlist
copying runtime jar...
WARNING: A terminally deprecated method in java.lang.System has been called
WARNING: System::setSecurityManager has been called by sbt.TrapExit$ (file:/home/user/.sbt/boot/scala-2.12.12/org.scala-sbt/sbt/1.4.7/run_2.12-1.4.7.jar)
WARNING: Please consider reporting this to the maintainers of sbt.TrapExit$
WARNING: System::setSecurityManager will be removed in a future release
[info] welcome to sbt 1.4.7 (N/A Java 17.0.3)
[info] loading settings for project vexriscv-build from plugins.sbt ...
[info] loading project definition from /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv/project
[info] Updating 
https://repo.scala-sbt.org/scalasbt/sbt-plugin-releases/com.eed3si9n/sbt-assembly/scala_2.12/sbt_1.0/0.14.10/ivys/ivy.xml
  100.0% [##########] 1.7 KiB (2.0 KiB / s)
https://repo1.maven.org/maven2/org/pantsbuild/jarjar/1.7.2/jarjar-1.7.2.pom
  100.0% [##########] 2.1 KiB (62.4 KiB / s)
https://repo1.maven.org/maven2/org/scalactic/scalactic_2.12/3.0.8/scalactic_2.12-3.0.8.pom
  100.0% [##########] 2.2 KiB (29.5 KiB / s)
https://repo1.maven.org/maven2/org/apache/ant/ant/1.9.9/ant-1.9.9.pom
  100.0% [##########] 9.4 KiB (284.8 KiB / s)
https://repo1.maven.org/maven2/org/apache/maven/maven-plugin-api/3.3.9/maven-plugin-api-3.3.9.pom
  100.0% [##########] 2.6 KiB (77.2 KiB / s)
https://repo1.maven.org/maven2/org/ow2/asm/asm/7.0/asm-7.0.pom
  100.0% [##########] 2.9 KiB (39.8 KiB / s)
https://repo1.maven.org/maven2/org/ow2/asm/asm-commons/7.0/asm-commons-7.0.pom
  100.0% [##########] 3.6 KiB (38.4 KiB / s)
https://repo1.maven.org/maven2/org/apache/ant/ant-parent/1.9.9/ant-parent-1.9.9.pom
  100.0% [##########] 5.5 KiB (147.9 KiB / s)
https://repo1.maven.org/maven2/org/apache/maven/maven/3.3.9/maven-3.3.9.pom
  100.0% [##########] 23.4 KiB (615.0 KiB / s)
https://repo1.maven.org/maven2/org/ow2/ow2/1.5/ow2-1.5.pom
  100.0% [##########] 11.0 KiB (288.6 KiB / s)
https://repo1.maven.org/maven2/org/apache/maven/maven-parent/27/maven-parent-27.pom
  100.0% [##########] 39.8 KiB (903.5 KiB / s)
https://repo1.maven.org/maven2/org/apache/apache/17/apache-17.pom
  100.0% [##########] 15.7 KiB (540.7 KiB / s)
https://repo1.maven.org/maven2/org/apache/ant/ant-launcher/1.9.9/ant-launcher-1.9.9.pom
  100.0% [##########] 2.3 KiB (95.0 KiB / s)
https://repo1.maven.org/maven2/org/eclipse/sisu/org.eclipse.sisu.plexus/0.3.2/org.eclipse.sisu.plexus-0.3.2.pom
  100.0% [##########] 4.1 KiB (162.9 KiB / s)
https://repo1.maven.org/maven2/org/ow2/asm/asm-tree/7.0/asm-tree-7.0.pom
  100.0% [##########] 3.0 KiB (122.0 KiB / s)
https://repo1.maven.org/maven2/org/apache/maven/maven-artifact/3.3.9/maven-artifact-3.3.9.pom
  100.0% [##########] 2.1 KiB (46.3 KiB / s)
https://repo1.maven.org/maven2/org/apache/maven/maven-model/3.3.9/maven-model-3.3.9.pom
  100.0% [##########] 3.9 KiB (46.3 KiB / s)
https://repo1.maven.org/maven2/org/ow2/asm/asm-analysis/7.0/asm-analysis-7.0.pom
  100.0% [##########] 3.1 KiB (29.9 KiB / s)
https://repo1.maven.org/maven2/org/eclipse/sisu/sisu-plexus/0.3.2/sisu-plexus-0.3.2.pom
  100.0% [##########] 13.4 KiB (326.9 KiB / s)
https://repo1.maven.org/maven2/org/apache/commons/commons-lang3/3.4/commons-lang3-3.4.pom
  100.0% [##########] 21.7 KiB (618.9 KiB / s)
https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-classworlds/2.5.2/plexus-classworlds-2.5.2.pom
  100.0% [##########] 7.1 KiB (198.2 KiB / s)
https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-component-annotations/1.5.5/plexus-component-annotations-1.5.5.pom
  100.0% [##########] 815B (22.1 KiB / s)
https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/3.0.22/plexus-utils-3.0.22.pom
  100.0% [##########] 3.7 KiB (106.9 KiB / s)
https://repo1.maven.org/maven2/org/eclipse/sisu/org.eclipse.sisu.inject/0.3.2/org.eclipse.sisu.inject-0.3.2.pom
  100.0% [##########] 2.6 KiB (71.2 KiB / s)
https://repo1.maven.org/maven2/javax/enterprise/cdi-api/1.0/cdi-api-1.0.pom
  100.0% [##########] 1.4 KiB (19.7 KiB / s)
https://repo1.maven.org/maven2/org/eclipse/sisu/sisu-inject/0.3.2/sisu-inject-0.3.2.pom
  100.0% [##########] 14.1 KiB (469.0 KiB / s)
https://repo1.maven.org/maven2/org/apache/commons/commons-parent/37/commons-parent-37.pom
  100.0% [##########] 61.6 KiB (1.2 MiB / s)
https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-containers/1.5.5/plexus-containers-1.5.5.pom
  100.0% [##########] 4.1 KiB (84.5 KiB / s)
https://repo1.maven.org/maven2/org/codehaus/plexus/plexus/3.3.1/plexus-3.3.1.pom
  100.0% [##########] 20.0 KiB (391.5 KiB / s)
https://repo1.maven.org/maven2/org/jboss/weld/weld-api-parent/1.0/weld-api-parent-1.0.pom
  100.0% [##########] 2.3 KiB (45.1 KiB / s)
https://repo1.maven.org/maven2/org/apache/apache/16/apache-16.pom
  100.0% [##########] 15.0 KiB (406.4 KiB / s)
https://repo1.maven.org/maven2/org/codehaus/plexus/plexus/2.0.7/plexus-2.0.7.pom
  100.0% [##########] 16.9 KiB (444.5 KiB / s)
https://repo1.maven.org/maven2/org/jboss/weld/weld-api-bom/1.0/weld-api-bom-1.0.pom
  100.0% [##########] 7.7 KiB (203.2 KiB / s)
https://repo1.maven.org/maven2/org/sonatype/spice/spice-parent/17/spice-parent-17.pom
  100.0% [##########] 6.6 KiB (173.7 KiB / s)
https://repo1.maven.org/maven2/org/jboss/weld/weld-parent/6/weld-parent-6.pom
  100.0% [##########] 20.2 KiB (481.1 KiB / s)
https://repo1.maven.org/maven2/org/sonatype/forge/forge-parent/10/forge-parent-10.pom
  100.0% [##########] 13.2 KiB (308.0 KiB / s)
[info] Resolved  dependencies
[info] Updating 
https://repo1.maven.org/maven2/org/fusesource/jansi/jansi/1.12/jansi-1.12.pom
  100.0% [##########] 3.6 KiB (120.8 KiB / s)
[info] Resolved  dependencies
[info] Fetching artifacts of 
https://repo1.maven.org/maven2/javax/annotation/jsr250-api/1.0/jsr250-api-1.0.jar
  100.0% [##########] 5.7 KiB (154.3 KiB / s)
https://repo1.maven.org/maven2/org/ow2/asm/asm-commons/7.0/asm-commons-7.0.jar
  100.0% [##########] 78.0 KiB (2.1 MiB / s)
https://repo1.maven.org/maven2/org/ow2/asm/asm-tree/7.0/asm-tree-7.0.jar
  100.0% [##########] 49.2 KiB (1.3 MiB / s)
https://repo1.maven.org/maven2/org/apache/maven/maven-plugin-api/3.3.9/maven-plugin-api-3.3.9.jar
  100.0% [##########] 46.4 KiB (1.0 MiB / s)
https://repo1.maven.org/maven2/org/eclipse/sisu/org.eclipse.sisu.inject/0.3.2/org.eclipse.sisu.inject-0.3.2.jar
  100.0% [##########] 368.8 KiB (4.7 MiB / s)
https://repo1.maven.org/maven2/org/ow2/asm/asm-analysis/7.0/asm-analysis-7.0.jar
  100.0% [##########] 32.5 KiB (739.5 KiB / s)
https://repo1.maven.org/maven2/javax/enterprise/cdi-api/1.0/cdi-api-1.0.jar
  100.0% [##########] 43.9 KiB (1.3 MiB / s)
https://repo1.maven.org/maven2/org/apache/commons/commons-lang3/3.4/commons-lang3-3.4.jar
  100.0% [##########] 424.5 KiB (7.4 MiB / s)
https://repo1.maven.org/maven2/org/apache/maven/maven-artifact/3.3.9/maven-artifact-3.3.9.jar
  100.0% [##########] 53.7 KiB (1.0 MiB / s)
https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-classworlds/2.5.2/plexus-classworlds-2.5.2.jar
  100.0% [##########] 51.4 KiB (443.5 KiB / s)
https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-utils/3.0.22/plexus-utils-3.0.22.jar
  100.0% [##########] 239.2 KiB (2.5 MiB / s)
https://repo1.maven.org/maven2/javax/inject/javax.inject/1/javax.inject-1.jar
  100.0% [##########] 2.4 KiB (55.4 KiB / s)
https://repo1.maven.org/maven2/org/eclipse/sisu/org.eclipse.sisu.plexus/0.3.2/org.eclipse.sisu.plexus-0.3.2.jar
  100.0% [##########] 200.6 KiB (4.7 MiB / s)
https://repo1.maven.org/maven2/org/codehaus/plexus/plexus-component-annotations/1.5.5/plexus-component-annotations-1.5.5.jar
  100.0% [##########] 4.1 KiB (80.6 KiB / s)
https://repo1.maven.org/maven2/org/ow2/asm/asm/7.0/asm-7.0.jar
  100.0% [##########] 111.0 KiB (1.4 MiB / s)
https://repo1.maven.org/maven2/org/pantsbuild/jarjar/1.7.2/jarjar-1.7.2.jar
  100.0% [##########] 122.3 KiB (3.7 MiB / s)
https://repo1.maven.org/maven2/org/apache/ant/ant-launcher/1.9.9/ant-launcher-1.9.9.jar
  100.0% [##########] 18.0 KiB (399.2 KiB / s)
https://repo1.maven.org/maven2/org/apache/maven/maven-model/3.3.9/maven-model-3.3.9.jar
  100.0% [##########] 160.1 KiB (2.0 MiB / s)
https://repo1.maven.org/maven2/org/fusesource/jansi/jansi/1.12/jansi-1.12.jar
  100.0% [##########] 148.2 KiB (1.4 MiB / s)
https://repo1.maven.org/maven2/org/scalactic/scalactic_2.12/3.0.8/scalactic_2.12-3.0.8.jar
  100.0% [##########] 705.2 KiB (1.8 MiB / s)
https://repo1.maven.org/maven2/org/apache/ant/ant/1.9.9/ant-1.9.9.jar
  100.0% [##########] 2.0 MiB (4.5 MiB / s)
[info] Fetched artifacts of 
[info] loading settings for project root from build.sbt ...
[info] loading settings for project spinalhdl-build from plugin.sbt ...
[info] loading project definition from /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/project
[info] Updating 
https://repo1.maven.org/maven2/org/scalameta/sbt-scalafmt_2.12_1.0/2.4.3/sbt-scalafmt-2.4.3.pom
  100.0% [##########] 2.5 KiB (27.3 KiB / s)
https://repo1.maven.org/maven2/org/xerial/sbt/sbt-sonatype_2.12_1.0/2.3/sbt-sonatype-2.3.pom
  100.0% [##########] 2.3 KiB (24.3 KiB / s)
https://repo.scala-sbt.org/scalasbt/sbt-plugin-releases/com.jsuereth/sbt-pgp/scala_2.12/sbt_1.0/1.1.0/ivys/ivy.xml
  100.0% [##########] 1.6 KiB (10.2 KiB / s)
https://repo.scala-sbt.org/scalasbt/sbt-plugin-releases/com.eed3si9n/sbt-unidoc/scala_2.12/sbt_1.0/0.4.1/ivys/ivy.xml
  100.0% [##########] 1.5 KiB (4.2 KiB / s)
https://repo1.maven.org/maven2/org/apache/httpcomponents/httpclient/4.2.6/httpclient-4.2.6.pom
  100.0% [##########] 5.4 KiB (186.4 KiB / s)
https://repo1.maven.org/maven2/com/eed3si9n/gigahorse-okhttp_2.12/0.3.0/gigahorse-okhttp_2.12-0.3.0.pom
  100.0% [##########] 2.1 KiB (41.2 KiB / s)
https://repo1.maven.org/maven2/org/scalameta/scalafmt-dynamic_2.12/2.7.5/scalafmt-dynamic_2.12-2.7.5.pom
  100.0% [##########] 2.7 KiB (54.8 KiB / s)
https://repo.scala-sbt.org/scalasbt/sbt-plugin-releases/com.jsuereth/pgp-library_2.12/1.1.0/ivys/ivy.xml
  100.0% [##########] 1.8 KiB (11.7 KiB / s)
https://repo1.maven.org/maven2/org/apache/httpcomponents/httpcomponents-client/4.2.6/httpcomponents-client-4.2.6.pom
  100.0% [##########] 12.3 KiB (207.6 KiB / s)
https://repo1.maven.org/maven2/org/apache/httpcomponents/project/7/project-7.pom
  100.0% [##########] 26.6 KiB (886.8 KiB / s)
https://repo1.maven.org/maven2/org/apache/apache/13/apache-13.pom
  100.0% [##########] 13.6 KiB (368.8 KiB / s)
https://repo1.maven.org/maven2/com/squareup/okhttp3/okhttp/3.7.0/okhttp-3.7.0.pom
  100.0% [##########] 1.5 KiB (42.9 KiB / s)
https://repo1.maven.org/maven2/com/typesafe/config/1.4.0/config-1.4.0.pom
  100.0% [##########] 2.2 KiB (62.2 KiB / s)
https://repo1.maven.org/maven2/commons-codec/commons-codec/1.6/commons-codec-1.6.pom
  100.0% [##########] 10.9 KiB (311.3 KiB / s)
https://repo1.maven.org/maven2/commons-logging/commons-logging/1.1.1/commons-logging-1.1.1.pom
  100.0% [##########] 17.9 KiB (527.5 KiB / s)
https://repo1.maven.org/maven2/org/apache/httpcomponents/httpcore/4.2.5/httpcore-4.2.5.pom
  100.0% [##########] 4.8 KiB (86.5 KiB / s)
https://repo1.maven.org/maven2/com/eed3si9n/gigahorse-core_2.12/0.3.0/gigahorse-core_2.12-0.3.0.pom
  100.0% [##########] 2.2 KiB (54.4 KiB / s)
https://repo1.maven.org/maven2/io/get-coursier/interface/0.0.17/interface-0.0.17.pom
  100.0% [##########] 1.6 KiB (40.9 KiB / s)
https://repo1.maven.org/maven2/org/bouncycastle/bcpg-jdk15on/1.51/bcpg-jdk15on-1.51.pom
  100.0% [##########] 1.6 KiB (36.2 KiB / s)
https://repo1.maven.org/maven2/org/scala-lang/modules/scala-parser-combinators_2.12/1.0.5/scala-parser-combinators_2.12-1.0.5.pom
  100.0% [##########] 2.1 KiB (29.7 KiB / s)
https://repo1.maven.org/maven2/org/scalameta/scalafmt-interfaces/2.7.5/scalafmt-interfaces-2.7.5.pom
  100.0% [##########] 2.1 KiB (56.0 KiB / s)
https://repo1.maven.org/maven2/org/apache/httpcomponents/httpcomponents-core/4.2.5/httpcomponents-core-4.2.5.pom
  100.0% [##########] 9.1 KiB (304.1 KiB / s)
https://repo1.maven.org/maven2/org/apache/commons/commons-parent/22/commons-parent-22.pom
  100.0% [##########] 40.9 KiB (818.7 KiB / s)
https://repo1.maven.org/maven2/org/apache/commons/commons-parent/5/commons-parent-5.pom
  100.0% [##########] 15.7 KiB (348.1 KiB / s)
https://repo1.maven.org/maven2/org/apache/apache/9/apache-9.pom
  100.0% [##########] 14.8 KiB (435.4 KiB / s)
https://repo1.maven.org/maven2/org/apache/apache/4/apache-4.pom
  100.0% [##########] 4.4 KiB (99.8 KiB / s)
https://repo1.maven.org/maven2/com/typesafe/ssl-config-core_2.12/0.2.2/ssl-config-core_2.12-0.2.2.pom
  100.0% [##########] 1.9 KiB (60.6 KiB / s)
https://repo1.maven.org/maven2/org/bouncycastle/bcprov-jdk15on/1.51/bcprov-jdk15on-1.51.pom
  100.0% [##########] 1.1 KiB (35.3 KiB / s)
https://repo1.maven.org/maven2/org/reactivestreams/reactive-streams/1.0.0/reactive-streams-1.0.0.pom
  100.0% [##########] 1.1 KiB (35.4 KiB / s)
https://repo1.maven.org/maven2/com/squareup/okio/okio/1.12.0/okio-1.12.0.pom
  100.0% [##########] 1.4 KiB (27.8 KiB / s)
https://repo1.maven.org/maven2/com/squareup/okio/okio-parent/1.12.0/okio-parent-1.12.0.pom
  100.0% [##########] 3.7 KiB (105.7 KiB / s)
[info] Resolved  dependencies
[info] Fetching artifacts of 
https://repo1.maven.org/maven2/org/slf4j/slf4j-api/1.7.25/slf4j-api-1.7.25.jar
  100.0% [##########] 40.2 KiB (1.0 MiB / s)
https://repo1.maven.org/maven2/org/scalameta/scalafmt-dynamic_2.12/2.7.5/scalafmt-dynamic_2.12-2.7.5.jar
  100.0% [##########] 113.2 KiB (1.1 MiB / s)
https://repo1.maven.org/maven2/com/squareup/okhttp3/okhttp/3.7.0/okhttp-3.7.0.jar
  100.0% [##########] 385.7 KiB (4.7 MiB / s)
https://repo1.maven.org/maven2/commons-logging/commons-logging/1.1.1/commons-logging-1.1.1.jar
  100.0% [##########] 59.3 KiB (1.4 MiB / s)
https://repo1.maven.org/maven2/org/apache/httpcomponents/httpcore/4.2.5/httpcore-4.2.5.jar
  100.0% [##########] 222.4 KiB (1.6 MiB / s)
https://repo1.maven.org/maven2/org/reactivestreams/reactive-streams/1.0.0/reactive-streams-1.0.0.jar
  100.0% [##########] 2.0 KiB (76.7 KiB / s)
https://repo1.maven.org/maven2/org/xerial/sbt/sbt-sonatype_2.12_1.0/2.3/sbt-sonatype-2.3.jar
  100.0% [##########] 80.4 KiB (512.0 KiB / s)
https://repo1.maven.org/maven2/commons-codec/commons-codec/1.6/commons-codec-1.6.jar
  100.0% [##########] 227.3 KiB (1.2 MiB / s)
https://repo1.maven.org/maven2/org/scala-lang/modules/scala-parser-combinators_2.12/1.0.5/scala-parser-combinators_2.12-1.0.5.jar
  100.0% [##########] 205.1 KiB (2.9 MiB / s)
https://repo1.maven.org/maven2/com/typesafe/ssl-config-core_2.12/0.2.2/ssl-config-core_2.12-0.2.2.jar
  100.0% [##########] 237.8 KiB (3.9 MiB / s)
https://repo1.maven.org/maven2/org/apache/httpcomponents/httpclient/4.2.6/httpclient-4.2.6.jar
  100.0% [##########] 425.4 KiB (4.2 MiB / s)
https://repo1.maven.org/maven2/com/squareup/okio/okio/1.12.0/okio-1.12.0.jar
  100.0% [##########] 79.2 KiB (2.6 MiB / s)
https://repo1.maven.org/maven2/org/bouncycastle/bcpg-jdk15on/1.51/bcpg-jdk15on-1.51.jar
  100.0% [##########] 249.7 KiB (1.7 MiB / s)
https://repo1.maven.org/maven2/org/scalameta/sbt-scalafmt_2.12_1.0/2.4.3/sbt-scalafmt-2.4.3.jar
  100.0% [##########] 39.6 KiB (748.1 KiB / s)
https://repo1.maven.org/maven2/org/scalameta/scalafmt-interfaces/2.7.5/scalafmt-interfaces-2.7.5.jar
  100.0% [##########] 4.3 KiB (101.4 KiB / s)
https://repo1.maven.org/maven2/com/eed3si9n/gigahorse-okhttp_2.12/0.3.0/gigahorse-okhttp_2.12-0.3.0.jar
  100.0% [##########] 39.3 KiB (510.7 KiB / s)
https://repo1.maven.org/maven2/com/typesafe/config/1.4.0/config-1.4.0.jar
  100.0% [##########] 287.3 KiB (1.1 MiB / s)
https://repo1.maven.org/maven2/com/eed3si9n/gigahorse-core_2.12/0.3.0/gigahorse-core_2.12-0.3.0.jar
  100.0% [##########] 163.1 KiB (1.6 MiB / s)
https://repo.scala-sbt.org/scalasbt/sbt-plugin-releases/com.jsuereth/pgp-library_2.12/1.1.0/jars/pgp-library_2.12.jar
  100.0% [##########] 183.7 KiB (326.8 KiB / s)
https://repo.scala-sbt.org/scalasbt/sbt-plugin-releases/com.jsuereth/sbt-pgp/scala_2.12/sbt_1.0/1.1.0/jars/sbt-pgp.jar
  100.0% [##########] 194.9 KiB (531.2 KiB / s)
https://repo.scala-sbt.org/scalasbt/sbt-plugin-releases/com.eed3si9n/sbt-unidoc/scala_2.12/sbt_1.0/0.4.1/jars/sbt-unidoc.jar
  100.0% [##########] 44.2 KiB (74.0 KiB / s)
https://repo1.maven.org/maven2/org/bouncycastle/bcprov-jdk15on/1.51/bcprov-jdk15on-1.51.jar
  100.0% [##########] 2.7 MiB (2.8 MiB / s)
https://repo1.maven.org/maven2/io/get-coursier/interface/0.0.17/interface-0.0.17.jar
  100.0% [##########] 3.0 MiB (1.5 MiB / s)
[info] Fetched artifacts of 
[info] compiling 1 Scala source to /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/project/target/scala-2.12/sbt-1.0/classes ...
https://repo1.maven.org/maven2/org/scala-sbt/util-interface/1.4.0/util-interface-1.4.0.jar
  100.0% [##########] 2.6 KiB (131.9 KiB / s)
[info] Non-compiled module 'compiler-bridge_2.12' for Scala 2.12.12. Compiling...
[info]   Compilation completed in 9.035s.
[info] loading settings for project all from build.sbt ...
[info] set current project to VexRiscv (in build file:/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv/)
[warn] there are 9 keys that are not used by any other settings/tasks:
[warn]  
[warn] * all / test / baseDirectory
[warn]   +- /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/build.sbt:13
[warn] * core / test / baseDirectory
[warn]   +- /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/build.sbt:13
[warn] * debugger / test / baseDirectory
[warn]   +- /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/build.sbt:13
[warn] * demo / test / baseDirectory
[warn]   +- /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/build.sbt:13
[warn] * idslpayload / test / baseDirectory
[warn]   +- /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/build.sbt:13
[warn] * idslplugin / test / baseDirectory
[warn]   +- /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/build.sbt:13
[warn] * lib / test / baseDirectory
[warn]   +- /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/build.sbt:13
[warn] * sim / test / baseDirectory
[warn]   +- /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/build.sbt:13
[warn] * tester / test / baseDirectory
[warn]   +- /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/build.sbt:13
[warn]  
[warn] note: a setting might still be used by a command; to exclude a key from this `lintUnused` check
[warn] either append it to `Global / excludeLintKeys` or call .withRank(KeyRanks.Invisible) on the key
[info] Updating 
[info] Resolved  dependencies
[info] Updating 
https://repo1.maven.org/maven2/org/scala-lang/scala-compiler/2.11.12/scala-compiler-2.11.12.pom
  100.0% [##########] 2.3 KiB (60.9 KiB / s)
https://repo1.maven.org/maven2/jline/jline/2.14.3/jline-2.14.3.pom
  100.0% [##########] 19.4 KiB (236.9 KiB / s)
https://repo1.maven.org/maven2/org/scala-lang/modules/scala-parser-combinators_2.11/1.0.4/scala-parser-combinators_2.11-1.0.4.pom
  100.0% [##########] 2.1 KiB (25.7 KiB / s)
https://repo1.maven.org/maven2/org/scala-lang/modules/scala-xml_2.11/1.2.0/scala-xml_2.11-1.2.0.pom
  100.0% [##########] 2.7 KiB (22.2 KiB / s)
[info] Resolved  dependencies
[info] Fetching artifacts of 
https://repo1.maven.org/maven2/org/scala-lang/modules/scala-parser-combinators_2.11/1.0.4/scala-parser-combinators_2.11-1.0.4.jar
  100.0% [##########] 413.8 KiB (2.8 MiB / s)
https://repo1.maven.org/maven2/jline/jline/2.14.3/jline-2.14.3.jar
  100.0% [##########] 262.2 KiB (1.4 MiB / s)
https://repo1.maven.org/maven2/org/scala-lang/modules/scala-xml_2.11/1.2.0/scala-xml_2.11-1.2.0.jar
  100.0% [##########] 663.3 KiB (2.3 MiB / s)
https://repo1.maven.org/maven2/org/scala-lang/scala-reflect/2.11.12/scala-reflect-2.11.12.jar
  100.0% [##########] 4.4 MiB (1.8 MiB / s)
https://repo1.maven.org/maven2/org/scala-lang/scala-compiler/2.11.12/scala-compiler-2.11.12.jar
  100.0% [##########] 14.9 MiB (4.5 MiB / s)
https://repo1.maven.org/maven2/org/scala-lang/scala-library/2.11.12/scala-library-2.11.12.jar
  100.0% [##########] 5.5 MiB (1.5 MiB / s)
[info] Fetched artifacts of 
[info] Updating 
https://repo1.maven.org/maven2/commons-io/commons-io/2.4/commons-io-2.4.pom
  100.0% [##########] 9.9 KiB (283.6 KiB / s)
https://repo1.maven.org/maven2/org/slf4j/slf4j-simple/1.7.25/slf4j-simple-1.7.25.pom
  100.0% [##########] 1015B (28.3 KiB / s)
https://repo1.maven.org/maven2/com/github/oshi/oshi-core/5.2.0/oshi-core-5.2.0.pom
  100.0% [##########] 3.6 KiB (37.7 KiB / s)
https://repo1.maven.org/maven2/net/openhft/affinity/3.21ea1.1/affinity-3.21ea1.1.pom
  100.0% [##########] 8.2 KiB (70.9 KiB / s)
https://repo1.maven.org/maven2/com/github/oshi/oshi-parent/5.2.0/oshi-parent-5.2.0.pom
  100.0% [##########] 35.0 KiB (1.1 MiB / s)
https://repo1.maven.org/maven2/net/openhft/java-parent-pom/1.1.23/java-parent-pom-1.1.23.pom
  100.0% [##########] 4.7 KiB (151.8 KiB / s)
https://repo1.maven.org/maven2/org/apache/commons/commons-parent/25/commons-parent-25.pom
  100.0% [##########] 47.2 KiB (924.9 KiB / s)
https://repo1.maven.org/maven2/net/openhft/root-parent-pom/1.2.3/root-parent-pom-1.2.3.pom
  100.0% [##########] 12.9 KiB (322.2 KiB / s)
https://repo1.maven.org/maven2/net/openhft/third-party-bom/3.19.4/third-party-bom-3.19.4.pom
  100.0% [##########] 19.9 KiB (349.2 KiB / s)
https://repo1.maven.org/maven2/org/jetbrains/annotations/19.0.0/annotations-19.0.0.pom
  100.0% [##########] 1.3 KiB (38.9 KiB / s)
[info] Resolved  dependencies
[info] Fetching artifacts of 
https://repo1.maven.org/maven2/org/jetbrains/annotations/19.0.0/annotations-19.0.0.jar
  100.0% [##########] 24.2 KiB (654.0 KiB / s)
https://repo1.maven.org/maven2/org/slf4j/slf4j-simple/1.7.25/slf4j-simple-1.7.25.jar
  100.0% [##########] 14.9 KiB (402.7 KiB / s)
https://repo1.maven.org/maven2/commons-io/commons-io/2.4/commons-io-2.4.jar
  100.0% [##########] 180.8 KiB (1.8 MiB / s)
https://repo1.maven.org/maven2/net/openhft/affinity/3.21ea1.1/affinity-3.21ea1.1.jar
  100.0% [##########] 81.1 KiB (693.2 KiB / s)
[info] Fetched artifacts of 
[info] Updating 
https://repo1.maven.org/maven2/com/github/scopt/scopt_2.11/3.7.1/scopt_2.11-3.7.1.pom
  100.0% [##########] 2.1 KiB (36.3 KiB / s)
https://repo1.maven.org/maven2/com/lihaoyi/sourcecode_2.11/0.2.7/sourcecode_2.11-0.2.7.pom
  100.0% [##########] 1.5 KiB (15.7 KiB / s)
[info] Resolved  dependencies
[info] Fetching artifacts of 
https://repo1.maven.org/maven2/com/github/scopt/scopt_2.11/3.7.1/scopt_2.11-3.7.1.jar
  100.0% [##########] 151.6 KiB (2.5 MiB / s)
[info] Fetched artifacts of 
[info] Updating 
https://repo1.maven.org/maven2/org/scalatest/scalatest_2.11/3.2.5/scalatest_2.11-3.2.5.pom
  100.0% [##########] 4.6 KiB (123.2 KiB / s)
https://repo1.maven.org/maven2/org/yaml/snakeyaml/1.8/snakeyaml-1.8.pom
  100.0% [##########] 13.2 KiB (355.7 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-refspec_2.11/3.2.5/scalatest-refspec_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (91.8 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-funspec_2.11/3.2.5/scalatest-funspec_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (51.9 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-wordspec_2.11/3.2.5/scalatest-wordspec_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (85.4 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-diagrams_2.11/3.2.5/scalatest-diagrams_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (91.9 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-freespec_2.11/3.2.5/scalatest-freespec_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (59.8 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-funsuite_2.11/3.2.5/scalatest-funsuite_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (36.2 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-matchers-core_2.11/3.2.5/scalatest-matchers-core_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (28.0 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-mustmatchers_2.11/3.2.5/scalatest-mustmatchers_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (109.6 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-core_2.11/3.2.5/scalatest-core_2.11-3.2.5.pom
  100.0% [##########] 3.8 KiB (35.5 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-featurespec_2.11/3.2.5/scalatest-featurespec_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (22.6 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-propspec_2.11/3.2.5/scalatest-propspec_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (30.6 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-shouldmatchers_2.11/3.2.5/scalatest-shouldmatchers_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (25.2 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-flatspec_2.11/3.2.5/scalatest-flatspec_2.11-3.2.5.pom
  100.0% [##########] 2.4 KiB (23.9 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-compatible/3.2.5/scalatest-compatible-3.2.5.pom
  100.0% [##########] 1.6 KiB (59.8 KiB / s)
https://repo1.maven.org/maven2/org/slf4j/slf4j-api/1.7.30/slf4j-api-1.7.30.pom
  100.0% [##########] 3.7 KiB (138.7 KiB / s)
https://repo1.maven.org/maven2/org/scalactic/scalactic_2.11/3.2.5/scalactic_2.11-3.2.5.pom
  100.0% [##########] 2.2 KiB (46.5 KiB / s)
https://repo1.maven.org/maven2/org/slf4j/slf4j-parent/1.7.30/slf4j-parent-1.7.30.pom
  100.0% [##########] 13.5 KiB (421.3 KiB / s)
[info] Resolved  dependencies
[info] Updating 
[info] Resolved  dependencies
[info] Fetching artifacts of 
https://repo1.maven.org/maven2/org/scalatest/scalatest-compatible/3.2.5/scalatest-compatible-3.2.5.jar
  100.0% [##########] 1.4 KiB (36.3 KiB / s)
https://repo1.maven.org/maven2/org/slf4j/slf4j-api/1.7.30/slf4j-api-1.7.30.jar
  100.0% [##########] 40.5 KiB (1.0 MiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest_2.11/3.2.5/scalatest_2.11-3.2.5.jar
  100.0% [##########] 718B (20.6 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-propspec_2.11/3.2.5/scalatest-propspec_2.11-3.2.5.jar
  100.0% [##########] 47.4 KiB (398.1 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-featurespec_2.11/3.2.5/scalatest-featurespec_2.11-3.2.5.jar
  100.0% [##########] 119.0 KiB (862.4 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-funsuite_2.11/3.2.5/scalatest-funsuite_2.11-3.2.5.jar
  100.0% [##########] 90.9 KiB (783.2 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-freespec_2.11/3.2.5/scalatest-freespec_2.11-3.2.5.jar
  100.0% [##########] 158.7 KiB (2.8 MiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-wordspec_2.11/3.2.5/scalatest-wordspec_2.11-3.2.5.jar
  100.0% [##########] 222.3 KiB (1.2 MiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-funspec_2.11/3.2.5/scalatest-funspec_2.11-3.2.5.jar
  100.0% [##########] 155.4 KiB (1008.9 KiB / s)
https://repo1.maven.org/maven2/org/scala-lang/modules/scala-xml_2.11/1.0.5/scala-xml_2.11-1.0.5.jar
  100.0% [##########] 655.4 KiB (2.6 MiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-diagrams_2.11/3.2.5/scalatest-diagrams_2.11-3.2.5.jar
  100.0% [##########] 25.4 KiB (445.9 KiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-core_2.11/3.2.5/scalatest-core_2.11-3.2.5.jar
  100.0% [##########] 4.8 MiB (16.4 MiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-matchers-core_2.11/3.2.5/scalatest-matchers-core_2.11-3.2.5.jar
  100.0% [##########] 2.3 MiB (8.5 MiB / s)
https://repo1.maven.org/maven2/org/scalactic/scalactic_2.11/3.2.5/scalactic_2.11-3.2.5.jar
  100.0% [##########] 1.6 MiB (3.3 MiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-refspec_2.11/3.2.5/scalatest-refspec_2.11-3.2.5.jar
  100.0% [##########] 43.4 KiB (884.9 KiB / s)
https://repo1.maven.org/maven2/org/yaml/snakeyaml/1.8/snakeyaml-1.8.jar
  100.0% [##########] 251.7 KiB (1.4 MiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-flatspec_2.11/3.2.5/scalatest-flatspec_2.11-3.2.5.jar
  100.0% [##########] 220.5 KiB (2.0 MiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-shouldmatchers_2.11/3.2.5/scalatest-shouldmatchers_2.11-3.2.5.jar
  100.0% [##########] 930.1 KiB (2.1 MiB / s)
https://repo1.maven.org/maven2/org/scalatest/scalatest-mustmatchers_2.11/3.2.5/scalatest-mustmatchers_2.11-3.2.5.jar
  100.0% [##########] 922.6 KiB (2.1 MiB / s)
[info] Fetched artifacts of 
[warn] There may be incompatibilities among your library dependencies; run 'evicted' to see detailed eviction warnings.
[info] compiling 2 Scala sources to /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/idslpayload/target/scala-2.11/classes ...
[info] compiling 13 Scala sources and 10 Java sources to /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/sim/target/scala-2.11/classes ...
https://repo1.maven.org/maven2/org/scala-sbt/compiler-bridge_2.11/1.4.4/compiler-bridge_2.11-1.4.4.pom
  100.0% [##########] 2.7 KiB (75.9 KiB / s)
[info] Non-compiled module 'compiler-bridge_2.11' for Scala 2.11.12. Compiling...
[info]   Compilation completed in 8.71s.
[warn] there were two deprecation warnings; re-run with -deprecation for details
[warn] one warning found
[info] compiling 2 Scala sources to /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/idslplugin/target/scala-2.11/classes ...
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/sim/src/main/scala/spinal/sim/VerilatorBackend.scala:463:20: match may not be exhaustive.
[warn] It would fail on the following inputs: DEFAULT, FSDB, FST_SPACE, FST_SPEED, GHW, LXT, LXT2, LXT2_SPACE, LXT2_SPEED, LXT_SPACE, LXT_SPEED, VCDGZ, VPD, WDB, WaveFormat()
[warn]     val waveArgs = format match {
[warn]                    ^
[warn] there were 5 deprecation warnings; re-run with -deprecation for details
[warn] one warning found
[warn] there was one deprecation warning; re-run with -deprecation for details
[warn] two warnings found
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/sim/src/main/java/spinal/sim/DynamicCompiler.java: DynamicCompiler.java uses or overrides a deprecated API.
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/sim/src/main/java/spinal/sim/DynamicCompiler.java: Recompile with -Xlint:deprecation for details.
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/sim/src/main/java/spinal/sim/DynamicCompiler.java: DynamicCompiler.java uses unchecked or unsafe operations.
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/sim/src/main/java/spinal/sim/DynamicCompiler.java: Recompile with -Xlint:unchecked for details.
[info] compiling 63 Scala sources and 1 Java source to /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/target/scala-2.11/classes ...
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/Bits.scala:30:22: a pure expression does nothing in statement position; you may be omitting necessary parentheses
[warn]   def Bits(u: Unit = null) = new Bits()
[warn]                      ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/SInt.scala:30:22: a pure expression does nothing in statement position; you may be omitting necessary parentheses
[warn]   def SInt(u: Unit = null) = new SInt()
[warn]                      ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/Trait.scala:45:22: a pure expression does nothing in statement position; you may be omitting necessary parentheses
[warn]   def Bool(u: Unit = null) = applyIt(spinal.core.Bool())
[warn]                      ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/Trait.scala:46:31: a pure expression does nothing in statement position; you may be omitting necessary parentheses
[warn]   override def Bits(u: Unit = null) = applyIt(super.Bits())
[warn]                               ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/Trait.scala:47:31: a pure expression does nothing in statement position; you may be omitting necessary parentheses
[warn]   override def UInt(u: Unit = null) = applyIt(super.UInt())
[warn]                               ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/Trait.scala:48:31: a pure expression does nothing in statement position; you may be omitting necessary parentheses
[warn]   override def SInt(u: Unit = null) = applyIt(super.SInt())
[warn]                               ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/UInt.scala:32:22: a pure expression does nothing in statement position; you may be omitting necessary parentheses
[warn]   def UInt(u: Unit = null) = new UInt()
[warn]                      ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/internals/Phase.scala:2433:25: non-variable type argument spinal.core.SpinalEnum in type pattern spinal.core.SpinalEnumCraft[spinal.core.SpinalEnum] is unchecked since it is eliminated by erasure
[warn]                 case d: SpinalEnumCraft[SpinalEnum] => d.init(d.spinalEnum.elements(0))
[warn]                         ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/AFix.scala:230:5: match may not be exhaustive.
[warn] It would fail on the following input: SCRAP
[warn]     roundType match {
[warn]     ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/SInt.scala:389:5: match may not be exhaustive.
[warn] It would fail on the following input: SCRAP
[warn]     roundType match{
[warn]     ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/core/src/main/scala/spinal/core/UInt.scala:268:5: match may not be exhaustive.
[warn] It would fail on the following input: SCRAP
[warn]     roundType match{
[warn]     ^
[warn] there were 5 deprecation warnings; re-run with -deprecation for details
[warn] there was one feature warning; re-run with -feature for details
[warn] 13 warnings found
[info] compiling 347 Scala sources to /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/target/scala-2.11/classes ...
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/bus/regif/BusIfAdapter/WishboneBusInterface.scala:5:30: imported `BusIf' is permanently hidden by definition of trait BusIf in package regif
[warn] import spinal.lib.bus.regif.{BusIf, ClassName}
[warn]                              ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/bus/regif/BusIfAdapter/WishboneBusInterface.scala:5:37: imported `ClassName' is permanently hidden by definition of object ClassName in package regif
[warn] import spinal.lib.bus.regif.{BusIf, ClassName}
[warn]                                     ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/generator/Generator.scala:100:7: a pure expression does nothing in statement position; you may be omitting necessary parentheses
[warn]       p
[warn]       ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/Stream.scala:154:5: match may not be exhaustive.
[warn] It would fail on the following inputs: (false, true, true), (true, false, true), (true, true, true)
[warn]     (m2s, s2m, halfRate) match {
[warn]     ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/bus/regif/RegInst.scala:622:7: Exhaustivity analysis reached max recursion depth, not all missing cases are reported.
[warn] (Please try with scalac -Ypatmat-exhaust-depth 40 or -Ypatmat-exhaust-depth off.)
[warn]       accType match {
[warn]       ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/bus/regif/RegInst.scala:641:7: Exhaustivity analysis reached max recursion depth, not all missing cases are reported.
[warn] (Please try with scalac -Ypatmat-exhaust-depth 40 or -Ypatmat-exhaust-depth off.)
[warn]       accType match {
[warn]       ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/dsptool/FixData.scala:30:26: match may not be exhaustive.
[warn] It would fail on the following input: SCRAP
[warn]       val rounded = this.roundType match {
[warn]                          ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/pipeline/Pipeline.scala:158:22: match may not be exhaustive
[warn] It would fail on the following input: Some((x: Any forSome x not in Pipeline.this.ConnectionModel))
[warn]       stageDriver.get(stage) match {
[warn]                      ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/system/dma/sg/MemoryCore.scala:112:7: match may not be exhaustive.
[warn] It would fail on the following input: (true, true)
[warn]       (p.writes(self).absolutePriority, p.writes(other).absolutePriority) match {
[warn]       ^
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/system/dma/sg/MemoryCore.scala:198:7: match may not be exhaustive.
[warn] It would fail on the following input: (true, true)
[warn]       (p.reads(self).absolutePriority, p.reads(other).absolutePriority) match {
[warn]       ^
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/bus/regif/BusIfAdapter/Axi4BusInterface.scala:1:1: 
[info] Found names but no class, trait or object is defined in the compilation unit.
[info] The incremental compiler cannot record the dependency information in such case.
[info] Some errors like unused import referring to a non-existent class might not be reported.
[info]     
[info] package spinal.lib.bus.regif
[info] ^
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/com/usb/sim/HostAgent.scala:1:1: 
[info] Found names but no class, trait or object is defined in the compilation unit.
[info] The incremental compiler cannot record the dependency information in such case.
[info] Some errors like unused import referring to a non-existent class might not be reported.
[info]     
[info] package spinal.lib.com.usb.sim
[info] ^
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/bus/regif/BusIfAdapter/Axi4BusInterface.scala:1:1: 
[info] Found top level imports but no class, trait or object is defined in the compilation unit.
[info] The incremental compiler cannot record the dependency information in such case.
[info] Some errors like unused import referring to a non-existent class might not be reported.
[info]     
[info] package spinal.lib.bus.regif
[info] ^
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/SpinalHDL/lib/src/main/scala/spinal/lib/com/usb/sim/HostAgent.scala:1:1: 
[info] Found top level imports but no class, trait or object is defined in the compilation unit.
[info] The incremental compiler cannot record the dependency information in such case.
[info] Some errors like unused import referring to a non-existent class might not be reported.
[info]     
[info] package spinal.lib.com.usb.sim
[info] ^
[warn] there were 68 deprecation warnings; re-run with -deprecation for details
[warn] there were 5 feature warnings; re-run with -feature for details
[warn] 12 warnings found
[info] compiling 91 Scala sources to /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv/target/scala-2.11/classes ...
[warn] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv/src/main/scala/vexriscv/VexRiscv.scala:36:17: match may not be exhaustive.
[warn] It would fail on the following input: None
[warn]     plugins.find(_.getClass == clazz) match {
[warn]                 ^
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv/src/main/scala/vexriscv/demo/smp/VexRiscvSmpLitexMpCluster.scala:1:1: 
[info] Found names but no class, trait or object is defined in the compilation unit.
[info] The incremental compiler cannot record the dependency information in such case.
[info] Some errors like unused import referring to a non-existent class might not be reported.
[info]     
[info] package vexriscv.demo.smp
[info] ^
[info] /home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog/ext/VexRiscv/src/main/scala/vexriscv/demo/smp/VexRiscvSmpLitexMpCluster.scala:1:1: 
[info] Found top level imports but no class, trait or object is defined in the compilation unit.
[info] The incremental compiler cannot record the dependency information in such case.
[info] Some errors like unused import referring to a non-existent class might not be reported.
[info]     
[info] package vexriscv.demo.smp
[info] ^
[warn] there were 40 deprecation warnings; re-run with -deprecation for details
[warn] there were two feature warnings; re-run with -feature for details
[warn] three warnings found
[info] running (fork) vexriscv.demo.smp.VexRiscvLitexSmpClusterCmdGen --cpu-count=1 --ibus-width=32 --dbus-width=32 --dcache-size=4096 --icache-size=4096 --dcache-ways=1 --icache-ways=1 --litedram-width=16 --aes-instruction=False --out-of-order-decoder=True --wishbone-memory=True --fpu=False --cpu-per-fpu=4 --rvc=False --netlist-name=VexRiscvLitexSmpCluster_Cc1_Iw32Is4096Iy1_Dw32Ds4096Dy1_ITs4DTs4_Ood_Wm --netlist-directory=/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/pythondata-cpu-vexriscv-smp/pythondata_cpu_vexriscv_smp/verilog --dtlb-size=4 --itlb-size=4
[info] [Runtime] SpinalHDL v1.7.1-SNAPSHOT    git head : b8bb31bec8321cf20da2f0cc2db0da9baad1249d
[info] [Runtime] JVM max memory : 3940.0MiB
[info] [Runtime] Current date : 2022.07.29 00:15:33
[info] [Progress] at 0.000 : Elaborate components
[info] [Progress] at 1.515 : Checks and transforms
[info] [Progress] at 2.026 : Generate Verilog
[info] [Warning] toplevel/cores_0_cpu_logic_cpu/RegFilePlugin_regFile : Mem[32 bits].readAsync can only be write first into Verilog
[info] [Warning] toplevel/cores_0_cpu_logic_cpu/RegFilePlugin_regFile : Mem[32 bits].readAsync can only be write first into Verilog
[info] [Warning] 298 signals were pruned. You can call printPruned on the backend report to get more informations.
[info] [Done] at 2.471
[success] Total time: 175 s (02:55), completed Jul 29, 2022, 12:15:35 AM
Python path configuration:
  PYTHONHOME = '/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite'
  PYTHONPATH = (not set)
  program name = '/usr/bin/python'
  isolated = 0
  environment = 1
  user site = 0
  import site = 1
  sys._base_executable = '/usr/bin/python'
  sys.base_prefix = '/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite'
  sys.base_exec_prefix = '/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite'
  sys.platlibdir = 'lib'
  sys.executable = '/usr/bin/python'
  sys.prefix = '/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite'
  sys.exec_prefix = '/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite'
  sys.path = [
    '/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/lib/python310.zip',
    '/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/lib/python3.10',
    '/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/lib/python3.10/lib-dynload',
  ]
Fatal Python error: init_fs_encoding: failed to get the Python codec of the filesystem encoding
Python runtime state: core initialized
ModuleNotFoundError: No module named 'encodings'

Current thread 0x00007fbd1ebbd740 (most recent call first):
  <no Python frame>
Traceback (most recent call last):
  File "./make.py", line 885, in <module>
    main()
  File "./make.py", line 858, in main
    builder.build(run=args.build, build_name=board_name)
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/litex/litex/soc/integration/builder.py", line 342, in build
    self._check_meson()
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/litex/litex/soc/integration/builder.py", line 259, in _check_meson
    meson_version = subprocess.check_output(["meson", "-v"]).decode("utf-8").split(".")
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/lib/python3.8/subprocess.py", line 411, in check_output
    return run(*popenargs, stdout=PIPE, timeout=timeout, check=True,
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/lib/python3.8/subprocess.py", line 512, in run
    raise CalledProcessError(retcode, process.args,
subprocess.CalledProcessError: Command '['meson', '-v']' returned non-zero exit status 1.
```

https://stackoverflow.com/questions/65184937/fatal-python-error-init-fs-encoding-failed-to-get-the-python-codec-of-the-file

comment out set pythonhome in ./oss-cad-suite/py3bin/python3.8

./make.py --board=ulx3s --device=LFE5U-85F --build

fujprog ulx3s.bit works but ./make.py --board=ulx3s --device=LFE5U-85F --load doesn't. Looks like it uses ujprog and fails with the error
```
ULX2S / ULX3S JTAG programmer v 3.0.92 (built Jul  6 2021 13:46:09)
Cannot find JTAG cable.
Traceback (most recent call last):
  File "./make.py", line 885, in <module>
    main()
  File "./make.py", line 874, in main
    board.load(filename=builder.get_bitstream_filename(mode="sram"))
  File "./make.py", line 33, in load
    prog.load_bitstream(filename)
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/litex/litex/build/lattice/programmer.py", line 160, in load_bitstream
    self.call(["ujprog", bitstream_file])
  File "/home/user/work/jacana/projects/ulx3s-doom/oss-cad-suite/litex/litex/litex/build/generic_programmer.py", line 101, in call
    raise OSError(msg)
OSError: Error occured during UJProg's call, please check:
- UJProg installation.
- Access permissions.
- Hardware and cable.
- Bitstream presence.
```
ujproj on its own with a .bit file fails the same way. instead of using ujprog, change `oss-cad-suite/litex/litex-boards/litex_boards/platforms/radiona_ulx3s.py`

```python
8:   from litex.build.lattice.programmer import FUJProg
204: return FUJProg()
```
and `oss-cad-suite/litex/litex/litex/build/lattice/programmer.py` to use `fujprog`
```python
154: # fujprog -------------------------------------------------------------------------------------------
155: 
156: class FUJProg(GenericProgrammer):
157:     needs_bitreverse = False
158: 
159:     def load_bitstream(self, bitstream_file):
160:         self.call(["fujprog", bitstream_file])
```

video of it working:
<video width="100%" controls muted>
  <source src="/ulx3s-linux-litex-leds.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>



to use lite_term, the UDEV rule described here was important
https://github.com/emard/ulx3s/blob/master/doc/MANUAL.md#programming-over-usb-port-us1

I didn't feel like building the full set of images with buildroot, etc, and so used the files at https://github.com/litex-hub/linux-on-litex-vexriscv/issues/164 

put them in the images directory

```
⦗OSS CAD Suite⦘ [user@mariner linux-on-litex-vexriscv]$ litex_term --images=images/boot.json /dev/ttyUSB0


litex> reboot�
        __   _ __      _  __
       / /  (_) /____ | |/_/
      / /__/ / __/ -_)>  <
     /____/_/\__/\__/_/|_|
   Build your hardware, easily!

 (c) Copyright 2012-2022 Enjoy-Digital
 (c) Copyright 2007-2015 M-Labs

 BIOS CRC passed (d34972b9)

 LiteX git sha1: 7789e187

--=============== SoC ==================--
CPU:		VexRiscv SMP-LINUX @ 50MHz
BUS:		WISHBONE 32-bit @ 4GiB
CSR:		32-bit data
ROM:		64KiB
SRAM:		6KiB
L2:		2KiB
SDRAM:		32768KiB 16-bit @ 50MT/s (CL-2 CWL-2)

--========== Initialization ============--
Initializing SDRAM @0x40000000...
Switching SDRAM to software control.
Switching SDRAM to hardware control.
Memtest at 0x40000000 (2.0MiB)...
  Write: 0x40000000-0x40200000 2.0MiB     
   Read: 0x40000000-0x40200000 2.0MiB     
Memtest OK
Memspeed at 0x40000000 (Sequential, 2.0MiB)...
  Write speed: 15.6MiB/s
   Read speed: 20.1MiB/s

--============== Boot ==================--
Booting from serial...
Press Q or ESC to abort boot completely.
sL5DdSMmkekro
[LITEX-TERM] Received firmware download request from the device.
[LITEX-TERM] Uploading images/Image to 0x40000000 (7531468 bytes)...
[LITEX-TERM] Upload calibration... (inter-frame: 10.00us, length: 64)
[LITEX-TERM] Upload complete (9.9KB/s).
[LITEX-TERM] Uploading images/rv32.dtb to 0x40ef0000 (2930 bytes)...
[LITEX-TERM] Upload calibration... (inter-frame: 10.00us, length: 64)
[LITEX-TERM] Upload complete (9.8KB/s).
[LITEX-TERM] Uploading images/rootfs.cpio to 0x41000000 (3781632 bytes)...
[LITEX-TERM] Upload calibration... (inter-frame: 10.00us, length: 64)
[LITEX-TERM] Upload complete (9.9KB/s).
[LITEX-TERM] Uploading images/opensbi.bin to 0x40f00000 (53640 bytes)...
[LITEX-TERM] Upload calibration... (inter-frame: 10.00us, length: 64)
[LITEX-TERM] Upload complete (9.9KB/s).
[LITEX-TERM] Booting the device.
[LITEX-TERM] Done.
Executing booted program at 0x40f00000

--============= Liftoff! ===============--

OpenSBI v0.8-1-gecf7701
   ____                    _____ ____ _____
  / __ \                  / ____|  _ \_   _|
 | |  | |_ __   ___ _ __ | (___ | |_) || |
 | |  | | '_ \ / _ \ '_ \ \___ \|  _ < | |
 | |__| | |_) |  __/ | | |____) | |_) || |_
  \____/| .__/ \___|_| |_|_____/|____/_____|
        | |
        |_|

Platform Name       : LiteX / VexRiscv-SMP
Platform Features   : timer,mfdeleg
Platform HART Count : 8
Boot HART ID        : 0
Boot HART ISA       : rv32imas
BOOT HART Features  : time
BOOT HART PMP Count : 0
Firmware Base       : 0x40f00000
Firmware Size       : 124 KB
Runtime SBI Version : 0.2

MIDELEG : 0x00000222
MEDELEG : 0x0000b101
[    0.000000] Linux version 5.14.0 (florent@panda) (riscv32-buildroot-linux-gnu-gcc.br_real (Buildroot 2021.08-381-g279167ee8d) 10.3.0, GNU ld (GNU Binutils) 2.36.1) #1 SMP Tue Sep 21 12:57:31 CEST 2021
[    0.000000] earlycon: liteuart0 at I/O port 0x0 (options '')
[    0.000000] Malformed early option 'console'
[    0.000000] earlycon: liteuart0 at MMIO 0xf0001000 (options '')
[    0.000000] printk: bootconsole [liteuart0] enabled
[    0.000000] Zone ranges:
[    0.000000]   Normal   [mem 0x0000000040000000-0x0000000041ffffff]
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000040000000-0x0000000041ffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000040000000-0x0000000041ffffff]
[    0.000000] SBI specification v0.2 detected
[    0.000000] SBI implementation ID=0x1 Version=0x8
[    0.000000] SBI TIME extension detected
[    0.000000] SBI IPI extension detected
[    0.000000] SBI RFENCE extension detected
[    0.000000] SBI v0.2 HSM extension detected
[    0.000000] riscv: ISA extensions aimp
[    0.000000] riscv: ELF capabilities aim
[    0.000000] percpu: Embedded 8 pages/cpu s11340 r0 d21428 u32768
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 8128
[    0.000000] Kernel command line: console=liteuart earlycon=liteuart,0xf0001000 rootwait root=/dev/ram0
[    0.000000] Dentry cache hash table entries: 4096 (order: 2, 16384 bytes, linear)
[    0.000000] Inode-cache hash table entries: 2048 (order: 1, 8192 bytes, linear)
[    0.000000] Sorting __ex_table...
[    0.000000] mem auto-init: stack:off, heap alloc:off, heap free:off
[    0.000000] Memory: 14956K/32768K available (5685K kernel code, 572K rwdata, 883K rodata, 209K init, 221K bss, 17812K reserved, 0K cma-reserved)
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
[    0.000000] rcu: Hierarchical RCU implementation.
[    0.000000] rcu: 	RCU restricting CPUs from NR_CPUS=8 to nr_cpu_ids=1.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 25 jiffies.
[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=1
[    0.000000] NR_IRQS: 64, nr_irqs: 64, preallocated irqs: 0
[    0.000000] riscv-intc: 32 local interrupts mapped
[    0.000000] plic: interrupt-controller@f0c00000: mapped 32 interrupts with 1 handlers for 2 contexts.
[    0.000000] random: get_random_bytes called from start_kernel+0x4ac/0x63c with crng_init=0
[    0.000000] riscv_timer_init_dt: Registering clocksource cpuid [0] hartid [0]
[    0.000000] clocksource: riscv_clocksource: mask: 0xffffffffffffffff max_cycles: 0xb8812736b, max_idle_ns: 440795202655 ns
[    0.000162] sched_clock: 64 bits at 50MHz, resolution 20ns, wraps every 4398046511100ns
[    0.024140] Console: colour dummy device 80x25
[    0.038575] Calibrating delay loop (skipped), value calculated using timer frequency.. 100.00 BogoMIPS (lpj=200000)
[    0.066396] pid_max: default: 32768 minimum: 301
[    0.114869] Mount-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.132312] Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.446399] ASID allocator using 9 bits (512 entries)
[    0.488325] rcu: Hierarchical SRCU implementation.
[    0.583902] smp: Bringing up secondary CPUs ...
[    0.595885] smp: Brought up 1 node, 1 CPU
[    0.682166] devtmpfs: initialized
[    1.108964] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645041785100000 ns
[    1.132894] futex hash table entries: 256 (order: 2, 16384 bytes, linear)
[    1.254997] NET: Registered PF_NETLINK/PF_ROUTE protocol family
[    3.744310] pps_core: LinuxPPS API ver. 1 registered
[    3.756917] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    3.781130] PTP clock support registered
[    3.838163] FPGA manager framework
[    4.035745] clocksource: Switched to clocksource riscv_clocksource
[    4.164352] simple-framebuffer 40c00000.framebuffer: framebuffer at 0x40c00000, 0x12c000 bytes
[    4.191594] simple-framebuffer 40c00000.framebuffer: format=a8b8g8r8, mode=640x480x32, linelength=2560
[    5.024843] Console: switching to colour frame buffer device 80x30
[    5.720672] simple-framebuffer 40c00000.framebuffer: fb0: simplefb registered!
[    9.615600] NET: Registered PF_INET protocol family
[    9.664848] IP idents hash table entries: 2048 (order: 2, 16384 bytes, linear)
[    9.812095] tcp_listen_portaddr_hash hash table entries: 512 (order: 0, 6144 bytes, linear)
[    9.848766] TCP established hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    9.880634] TCP bind hash table entries: 1024 (order: 1, 8192 bytes, linear)
[    9.905006] TCP: Hash tables configured (established 1024 bind 1024)
[    9.956199] UDP hash table entries: 256 (order: 1, 8192 bytes, linear)
[    9.984478] UDP-Lite hash table entries: 256 (order: 1, 8192 bytes, linear)
[   10.576617] Unpacking initramfs...
[   11.268751] workingset: timestamp_bits=30 max_order=12 bucket_order=0
[   16.576440] io scheduler mq-deadline registered
[   16.596250] io scheduler kyber registered
[   25.180568] LiteX SoC Controller driver initialized
[   65.824964] Initramfs unpacking failed: broken padding
[   69.172328] Freeing initrd memory: 8192K
[   76.127972] f0001000.serial: ttyLXU0 at MMIO 0x0 (irq = 0, base_baud = 0) is a liteuart
[   76.160433] printk: console [liteuart0] enabled
[   76.160433] printk: console [liteuart0] enabled
[   76.187949] printk: bootconsole [liteuart0] disabled
[   76.187949] printk: bootconsole [liteuart0] disabled
[   76.753018] i2c_dev: i2c /dev entries driver
[   77.684039] NET: Registered PF_INET6 protocol family
[   78.044553] Segment Routing with IPv6
[   78.068321] In-situ OAM (IOAM) with IPv6
[   78.108003] sit: IPv6, IPv4 and MPLS over IPv4 tunneling driver
[   78.408265] NET: Registered PF_PACKET protocol family
[   78.647424] litex-mmc f0004800.mmc: Requested clk_freq=12500000: set to 12500000 via div=4
[   78.944954] litex-mmc f0004800.mmc: Requested clk_freq=0: set to 195312 via div=256
[   79.172152] litex-mmc f0004800.mmc: Requested clk_freq=12500000: set to 12500000 via div=4
[   79.344638] Freeing unused kernel image (initmem) memory: 204K
[   79.371727] Kernel memory protection not selected by kernel config.
[   79.396748] Run /init as init process
[   80.496093] Command (cmd 9) failed, status 2
[   81.511834] Command (cmd 9) failed, status 2
[   82.528248] Command (cmd 9) failed, status 2
[   83.543870] Command (cmd 9) failed, status 2
[   84.560780] Command (cmd 9) failed, status 2
[   85.576461] Command (cmd 9) failed, status 2
[   85.592483] mmc0: unrecognised CSD structure version 3
[   85.615706] mmc0: error -22 whilst initialising SD card
[   85.635985] litex-mmc f0004800.mmc: card claims to support voltages below defined range
[   85.664419] litex-mmc f0004800.mmc: Requested clk_freq=0: set to 195312 via div=256
[   93.164181] litex-mmc f0004800.mmc: Requested clk_freq=12500000: set to 12500000 via div=4
[   94.331681] Command (cmd 1) failed, status 2
[   94.348833] mmc0: error -110 whilst initialising MMC card
[   94.368720] litex-mmc f0004800.mmc: Requested clk_freq=0: set to 195312 via div=256
Starting syslogd: OK
Starting klogd: OK
Running sysctl: 
OK
Saving random seed: [  205.083851] random: dd: uninitialized urandom read (512 bytes read)
OK
Starting network: OK

Welcome to Buildroot
buildroot login: root
                   __   _
                  / /  (_)__  __ ____ __
                 / /__/ / _ \/ // /\ \ /
                /____/_/_//_/\_,_//_\_\
                      / _ \/ _ \
   __   _ __      _  _\___/_//_/         ___  _
  / /  (_) /____ | |/_/__| | / /____ __ / _ \(_)__ _____  __
 / /__/ / __/ -_)>  </___/ |/ / -_) \ // , _/ (_-</ __/ |/ /
/____/_/\__/\__/_/|_|____|___/\__/_\_\/_/|_/_/___/\__/|___/
                  / __/  |/  / _ \
                 _\ \/ /|_/ / ___/
                /___/_/  /_/_/
  32-bit RISC-V Linux running on LiteX / VexRiscv-SMP.

login[72]: root login on 'console'
root@buildroot:~# whoami
root

```

when generating the buildroot binaries, cd to a directory above linux-on-litex-vexriscv. then run
```bash
$ git clone http://github.com/buildroot/buildroot
$ cd buildroot
$ make BR2_EXTERNAL=../linux-on-litex-vexriscv/buildroot/ litex_vexriscv_defconfig
$ make
```

When installing a RISCV toolckain, don't install riscv64-unknown-elf-gcc and instead install riscv-none-embed-gcc