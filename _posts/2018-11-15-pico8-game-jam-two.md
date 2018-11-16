---
layout: posts
title: Game Off 2018 Update (1/2)
date: 2018-11-15
---

Wow, I can't believe it's already been over two weeks since the Game Off kicked off. This year's theme is 'Hybrid'.

I have been sinking a lot of time into learning the mechanics of the PICO-8 and crafting new game elements
on the daily (shameless inspiration included). What I've come up with so far is called 'Akuma', a top-down
adventure staring a stoic human/demon hybrid set out to collect items, fight off baddies and claim...victory? 
If I'm being totally honest, I'm working out the details as I go - but isn't that the point of a code jam?

![](https://chadramsey.github.io/assets/images/2018/akuma_title_screen.gif)

After kicking around some ideas about how I wanted the look and feel of this title to be, given the limited color palette
and 'token' count (the number of variable names, operators, etc.) of the PICO-8, I settled on something that felt a little
more 'lively' than a simple 8-bit title. Since some of my favorite and most memorable gaming experiences came out of the 16-bit era, I knew
I could look there to draw inspiration from some of my favorite titles. Understanding this would ultimately
limit me in terms of sprite count (and force me to get really creative with the PICO-8's modest 16-color palette), I still felt like
I could complete something that was worth while and expressive.

So what do we have so far? I've been working on getting a few primary mechanics in place that would make way for handling the creative
elements during the latter half of the month. These machanics were also important to me for establishing the 'look and feel' of the game.

![](https://chadramsey.github.io/assets/images/2018/akuma_key_grab_screen.gif)

*"Queue the 'I found some awesome game-progressing loot' clip."*

As with all games, establishing a system to handle screen and collision events was a must. I've also worked in a dialog system that makes rendering 
event-based dialog pretty seamless. The scene elements (i.e., the flowers in this case), enemies, and player all operate on their own time cycles and are managed 
independently each frame. Currently picking up this key and promping the dialog will hault all player and enemy movement until dismissed. All sprites have been
hand drawn and I still continue to make tweaks to them regularly (I get lost in this process longer than I'd like to admit). To bring things home in the 
'look and feel' department, I decided to work in a screen transistion mechanic once the player reaches the bounds of a given map area - much like you'd 
see in many 16-bit era games.

![](https://chadramsey.github.io/assets/images/2018/akuma_transition_screen.gif)

All of this so far exists as a test bed for the remainder of the game. I plan on taking a hard shift into creating a meaningful environment and putting all
this to good use in the next couple weeks.

There's still much work to be done and I'm tweaking and creating as I go, but I have to say I'm having a good time along the way. If nothing else I can
say that I'm very impressed with the PICO-8 and its capability. It's a perfect tool for mocking up a simple game or other small applications and would
recommend it for anyone looking to gain an appreciation of game development.

I'll pop back in with a final write up towards the end of the project; in the mean time I'll be hammering down as much as I can before month's end.

