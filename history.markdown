---
layout: default
title: History
permalink: /history/
---

# History of the Game / Development

This game has gone through multiple overhauls, mainly when I realized a certain code structure I had made no sense since I had programmed it when I was younger. Here's a throw back to how the game first appeared in roughly 2015 / 2016:

<img src="/assets/oldVersionScreenshot.png" alt="">

Since then, I have added a hundred other features and abilities, heavily updated the graphics, and the code itself has exponentially grown and evolved as a result. This is what it looks like now:
<br>
<br>
## Screenshots
<img src="/assets/current_map.png" alt="">
<img src="/assets/chapter config.png" alt="">
<img src="/assets/trade chapter config.png" alt="">
<img src="/assets/armory.png" alt="">
<br>
<br>
## Where this project is going
Clearly based off this site I love retro games and that doesn't stop at just recreating one. I've also made my own console out of wood as you can see below, which normally runs Retropie:
<img src="/assets/retropie_front.png" alt="">
<img src="/assets/retropie_back.png" alt="">
<br>
The reason why I bring this up is because of what I am currently working on. 

Formerly, I always ran and worked on the game on my laptop running Windows, until it occurred to me - how cool would it be to be able to play my own game that I’ve programmed on a console that I‘ve built? Since then I have been (attempting) to migrate all functions of the game into a Linux distribution (the default Raspberry Pi OS) to be able to play it on there. Everything from trying to get outdated modules installed, changing the load structure to the linux file system and not my Windows PC, some audio files no longer want to load for some reason, etc.

This will also take some heavy modifications to the appearance - everything from the size of the text to how many tiles fit on the screen will have to be adjusted. I am going from a large laptop screen to an actual „console“ sized screen at just 480x320 resolution. It will take work. The other issue is now trying to use Python v2.7 on that, as when I tried updating the script to v3.x some modules no longer worked correctly nor did some of the sounds load in correctly.

So, to get the game working on linux (the Raspbian Desktop) I created a similar layout to the wood console it will end up on:

<img src="/assets/desktop_enviro.png" alt="">
<img src="/assets/custom_gamepad.png" alt="">
<br>
I quickly built the red gamepad that can plug into the Pi 3 and similarly takes the input from the GPIO pins with python. I formerly used a USB joystick on my Windows PC to play this game, but now I've got to remap all of the buttons. The main reason I built the red control stick is because it allows me an easier environment to work with than the 3.5" screen on the actual console.


The last part of this game that has changed includes the storyline. For a long time I was set on a classic FE-based plot, I hadn't planned out the actual dialogue but just the general direction each of the 25 chapters would take. About a year back, however, I revamped the entire plot since I felt it played too much into the FE genre, and it just felt overused. Now, it has a much darker plot that will hopefully leave the player unsure of whether or not they are even rooting for the main character. Formerly, the main character was always the hero and savior of the game - think Ike, Marth, Roy, Ephraim, etc. The intent now is to flip that idea as the game progresses. It certainly makes for a more interesting plot and avoids the clichés of past games.

<br>
<br>
**UPDATE**

So, I got all the buttons remapped to the raspberry pi after writing a new function that can read the input, how long the button has been pressed, etc. Python does support libraries for these kinds of things, however what I was trying to do has caused many people before me issues before I found out, and I found myself in the same boat. After it was working on my Desktop Pi, I threw the SD card into the console (also a Pi3 B+) and was able to run it. Unfortunately, it was extraordinarily slow. This was made on my laptop initially with 16GB RAM, 2.4GHz 6 core processor, etc which isn't a lot today but speed has never been an issue. Contrastly, it is much more than the 1GB RAM on the Pi and its slower processor. Using resource monitor from my laptop the program shouldn't be using any more than 100MB of RAM and enough CPU to spare for just this one program, so not sure where the bottleneck is. 
 <br>
 - Update again - 
So I ssh'd into the pi while it was running the game and ran htop, as it turns out the CPU was maxing out anywhere where from high 60s% to 104%. This isn't a super demanding script (imo), so after some research the problem lies either with a) the pygame.mixer() function (the audio), b) calling all pygame.init() functions when first starting out instead of only explictly calling the ones needed, c) for some reason installing Pygame via pip and not directly installing it (why I couldn't begin to understand...), or d) neglecting a time.sleep(x) function - which shouldn't be necessary since the game has a clock rate, even though it is continually running in the main while loop. So a lot of theories from stackoverflow to work through, hopefully I get it resolved.
<br>
Cheers.
