---
layout: posts
title: Game Off 2018 Update (2/2)
date: 2018-11-26
---

It's only been a few days since the last update, but I've decided to go ahead and comment on the overall status of this project
and where I see it heading.

Since my last update I've added a basic attack mechanic (the ability to 'consume' souls, because demons), basic enemy collision,
as well as health and soul tracking. My awesome wife [Corivana](https://github.com/corivana) also had a helping hand in putting together 
some additional enemy and environment sprites in preparation for what would be the final push to completion. 

![](https://chadramsey.github.io/assets/images/2018/akuma_damage_soul.gif){: .center-image }
*"A basic attack mechanic that allows the player to 'consume' souls"*

Then in the days following it slowly dawned on me that the PICO-8 was not the platform best suited for this project - what was initally endearing about its limitations became 
a hindrance to the spirit of what we were trying to create, and rather than submit what would feel like an 'incomplete' project I've decided to make other plans for it instead.

This isn't an attack on the PICO-8 as a platform - I still contest that its a fantastic tool for prototyping and even developing full-fledged
experiences - but instead a realization that the 'mini-venture' we set out to create would simply take longer than the time allotted to get in a suitable state in time for the Game Off,
and that we would really need to dig into the memory managment aspects of the PICO-8 in order to achieve the results we wanted to see. Currently the world map is incapable of spanning more than 1 transition in any direction, and given that sprite and map data share the same space in memory, creating the 
environment spites we wanted to implement also became a challenge. Even with the support of an additional developer/artist, seeing this project to a state I 
could be proud of didn't seem attainable. 

Ultimately my ambitions were bigger than my limitations, and I learned that along the way - something to keep in mind for the next game jam: keep it simple.

Having said that I am happy with the overall mechanics that are in place - and this *is* all in the spirit of open source - so I've decided to go ahead and make the
source code for this project publically available in it's current state for anyone interested to expand upon or pull from. The only condition is that any future 
iterations of the project remain open source and that sprites are not copied for use in other projects outside of this one.

The project source can be found [here](https://github.com/chadramsey/pico8-akuma) and I also have intentions on uploading the cartridge to lexaloffle later
this week for easy access. I'll update this post once that's done.

I'm pleased with what I have been able to learn regarding the PICO-8 over the course of the past three weeks, and I've had a blast getting up to 
speed with how one might approach the creation of their own top-down adventure using the PICO-8. 

Perhaps we'll get the opportunity to see this vision through more completely in the future, with an expanded color palette and fewer limitations, 
but in the mean time this has served as a great prototype of what may come.

Update: You can preview the cartridge uploaded to lexaloffle below:
<iframe src="https://www.lexaloffle.com/bbs/widget.php?pid=akuma-2" allowfullscreen width="621" height="513" style="border:none; overflow:hidden"></iframe>