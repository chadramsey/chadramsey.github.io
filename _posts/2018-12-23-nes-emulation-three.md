---
layout: posts
title: A Journey in NES Emulation - Part 2
date: 2018-12-23
---

With the [last post](https://chadramsey.github.io/nes-emulation-two/) covering a brief overview of the project as a whole, I want to start discussing some of the more detailed subject matter surrounding the NES, starting with the CPU. 

The NES CPU is based on the widly used [6502 microprocessor](https://en.wikipedia.org/wiki/MOS_Technology_6502) (as seen in the Apple II and Commodore 64), manufactured by Ricoh as the 2A03 and 2A07 microprocessor to accomodate for NTSC and PAL television systems, respectfully. What are NTSC and PAL? These two formats exist because analog television systems around the globe hold different standards for color encoding and refresh rate based on their region - at the time, many western countries used NTSC while most eastern countries adhered PAL. 

In order for the NES to accommodate for these differing standards, two variations of the CPU had to be manufactured, but aside from these modifications the processors are otherwise identical. The CPU runs at a 1.79 MHz on the NTSC variant, and 1.66 MHz on the PAL variant, and houses 2KB of internal RAM. In addition, the CPU also handles processing for audio and controller I/O - all within the same chip.

So how does the CPU start working with our games?

The CPU is in charge of translating compiled assemby code into actionable instructions based on the 6502's [instruction set](http://obelisk.me.uk/6502/reference.html). Once a ROM is loaded, the emulator initializes the program by determining the 'starting point', called the reset vector. Once the reset vector is determined the CPU reads in and processes the subsequent instructions which make up the mechanics of the game. One of the most laborious tasks in coming up with an emulator is transforming these instructions (also referred to as 'opcodes' in their compiled, byte-represented form) into their respective software-based implementations. The 6502 contains instructions for up to 256 unique opcodes, but of these 256 opcodes only 151 are offically supported.

A string of opcode translations might look something like this:

```
78d8 a900 8d00 20a2 (opcodes produced from compiled source code)

78 -> SEI - Set Interrupt Disable (2 cycles)
d8 -> CLD - Clear Decimal Mode (2 cycles)

a9 -> LDA - Load Accumulator (2 cycles)
00 -> BRK - Force Interrupt (7 cycles)

d8 -> CLD - Clear Decimal Mode (2 cycles)
00 -> BRK - Force Interrupt (7 cycles)

20 -> JSR - Jump to Subroutine (6 cycles)
a2 -> LDX - Load X Register (2 cycles)
```

And so on - a standard ROM contains thousands of opcode sequences.

You'll notice that 'cycles' are called out in this example as well. Keeping track of CPU cycle counts becomes directly relevant during synchronization with the PPU. which I plan on discussing in a future post. For now it's worth calling out that the PPU operates at 3 times the frquency of the CPU, so managing the timing between the two becomes crucial.

Since we're on the subject of discussing how the CPU operates, I want to also address on some of the core components of the CPU memory map. While the CPU on the NES only utilizes 2KB of RAM, it turns out the 6502 can actually reference up to 64KB of memory. 

So what is going on with the rest of that space? The remaining address space is used for PPU, APU, and I/O registers, as well as cartridge space for handling program ROM/RAM and mappers. Even then, segments of CPU and PPU address space are mirrored on the NES, presumably to save on the cost it would have otherwise taken to physically account for the unused address space outside of what was designated. A visual representation of how this address space is allocated would look something like this (credit to [NintendoAge](http://nintendoage.com/forum/messageview.cfm?catid=22&threadid=4291)):

![](https://chadramsey.github.io/assets/images/2018/nes-emu-three.png){: .center-image }
*"A visual representation of NES CPU address space."*

A well documented breakdown of how this address space is mapped can be found at the [nesdev Wiki](https://wiki.nesdev.com/w/index.php/CPU_memory_map). 

There are a mind boggling number details surrounding the CPU, and this post only scratches the surface regarding some of the basics. Fortunally, [the nesdev Wiki](https://wiki.nesdev.com/w/index.php/CPU#Sections) covers all of this information in painstaking detail.

Next up I plan on discussing how the CPU and PPU work together to display graphics to the screen.

kNES can be found [on my GitHub page](https://github.com/chadramsey/knes). 
This emulator is very much still in its infancy and published primarily to 
get the ball rolling on documentation and community support.