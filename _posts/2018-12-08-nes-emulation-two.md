---
layout: posts
title: A Journey in NES Emulation - Part 1
date: 2018-12-08
---

Writing an NES emulator has been a long time interest of mine, primarily because the subject of software emulation is facinating. I've spend my fair share of time studying how games are developed (from both modern and retro prospectives), but emulation is a completely different beast - an exercise in computer architecture dealing entirely in low-level components including precise hardware specifications and assembly code. Even for something we consider 'basic' by today's standards, the NES classics we all know and love are nothing short of technical masterpieces.

![](https://chadramsey.github.io/assets/images/2018/nes-emu-one.png){: .center-image }

I should address a couple of things up front about this project: first, why Kotlin? Kotlin is a 'modern', statically typed language that runs on the JVM. As someone who works regularly with Java, I feel that it's quickly becoming the preferred language over Java for modern application development and I enjoy working with it (read more about Kotlin ![here](https://kotlinlang.org/). Writing for the JVM also means that the emulator can be run 'cross-platform', and since we're dealing with NES hardware, the performance trade off isn't a top concern.

Secondly, I haven't taken on this project without huge support from existing projects in the open source commuity, namely Andrew Hoffman's ![halfnes](https://github.com/andrew-hoffman/halfnes), which is an existing, largely comprehensive NES emulator written in Java. A lot of my current understanding of certain implementation details have come from this project, although I'm in the process of learning more and tweaking as I go. Once I feel the project is in a 'good enough' state, I plan on submitting it as an open source project on my personal Github (ideally by the time these posts are complete). Another absolutely necessary source of information for this project comes from the ![nesdev Wiki](https://wiki.nesdev.com/w/index.php/NES_reference_guide), which contains both hardware and software documentation for everything NES.

With that out of the way, I can start discussing the project itself. Right out of the gate, I was interested in how an emulator could take compiled assembly code and translate that to pixels on a screen. Even having spent some time working through the process, I'm still completely fascinated by the orchestration of it all. Simply put, the compiled source code is represented as nothing more than a series of HEX values - each value signaling a processor directive that, as a whole, make up the instruction set for a given title. I plan on discussing the details of this process more in depth in a later post.

![](https://chadramsey.github.io/assets/images/2018/nes-emu-two.png){: .center-image }
*"The first few lines of compiled source code for 'Metroid'."*

Since I'm working with the JVM, and hardware acceleration and other low level bindings aren't completely necessary to achieve acceptable emulation for the NES, I decided to forgo using a cross-platform library such as SDL and stick with a basic JFrame implementation for this project - at least as a first pass solution. This implementation renders a new 'frame' as a BufferedImage and displays the contents within the JFrame at (an ideal) 60 frames/second, although I've found that the timing isn't always perfect. I also plan on discussing how these frames are composed when I get around to discussing the PPU, or picture processing unit (effectively the 'graphics processor' of the NES).

With the basics covered, I want to address one more topic central to console emulation. How is it that the compiled source code addressed above makes its way into a digital file format suited for emulators from the cartridge it originated from? NES cartridge data can be 'ripped', or extracted using special hardware/software such as ![INLretro Dumper-Programmer (formerly named 'kazzo')](www.infiniteneslives.com/inlretro.php). This relatively inexpensive board will allow cartridge owners to back up their cartridges into the digital formats that emulators accept. 

This product also supports the ability to flash cartridges, allowing the ability to load your own ROMs onto a playable cartridge for the die-hard enthusiast who wants to see their creations running on actual NES hardware. For those interested in writing games for the NES, the ![nesdev Wiki](https://wiki.nesdev.com/w/index.php/NES_reference_guide) is a great starting point, as well as ![NES Programming guide hosted on NintendoAge](http://nintendoage.com/forum/messageview.cfm?catid=22&threadid=7155).

Next up I plan on diving into the CPU, and how the NES handles working with the compiled source code mentioned above. Stick around for Part 2.