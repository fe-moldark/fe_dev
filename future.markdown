---
layout: default
title: Future
permalink: /future
---

# Future of this project

I'd recommend reading through the "History" tab first, otherwise this next part will not make much sense. 
<br>
<br>
Now, I have yet to completely solve the uncharacteristically high CPU usage (although I may have narrowed down why that is), I was able to try out the game at slow speeds on the 3.5" screen on my wooden console. And it didn't quite seem right. That is great for playing old GBA-style games who's screens are designed to be that small, but it didn't work with my game. This is even with me considering reorganizing / reducing the number of tiles to make the game fit onto a smaller screen, adjusting all the text size, etc etc. So I tried it on a 7" display that I've previously used to display a constant stream of the International Space Station (fun project), and quite honestly I loved it. Not only does everything look "full size", or just a natural size for the graphics, but everything from the text being readable to how I think the game should play felt right. 
<br>
<br>
To counter the issues I've seen using different Linux distributions and installing pygame there I have had thoughts of using a) Windows IoT on the Pi or b) using an old Windows 10 tablet (since they run a FULL version of Windows, not just the Windows IoT Core version. That will only be if all else fails since I want a light-weight OS.
<br>
<br>
Outside the scope of converting everything to work on Linux and getting pygame to work there, that means I will have to design an entirely new case for the 7" screen. And so taking inspiration from the Steam Deck and the Switch, I've designed the following:
<br>
<br>
<img src="/assets/console1.jpg" alt="">
<br>
<br>
The top image is how the console will look in a perfect world. Below that is a to-scale sketch of how all the parts will fit together. As you can see there are a LOT of parts to this, more than I used for my last console. All together the project would cost >$150, however thankfully I already have 95% of these things laying around from past projects. It includes a 10,000mAh battery, as well as powerboost board and a power switch that attaches on to it. There's a basic class D audio amplifier that will connect to speakers on both sides of the console, and I am using a slide potentiometer for volume control. I took apart one of my old USB joysticks and will be using the board, but rewired, to buttons on the e.g. PiGrrl Zero Gamepads. This allows me to have more freedom in design while still conveniently keeping the USB aspect which is good for looping through events in pygame. Other things I will be including are a low-power indicator LED and a fan on the back for cooling. Here's a more spacious rendition of how this will all (sort of) fit together.
<br>
<br>
<img src="/assets/console2.jpg" alt="">
<br>
<br>
There are a lot of parts here that will need very small and precise forms in order for this to all fit together, and that's why I've decided to go the route of a 3D printer. There's gonna be a very steep learning curve, trust me I'm aware, but I think this is the best route. It also doesn't hurt that I've always wanted a 3D printer because who hasn't wanted one? I will begin designing the case as soon as I've taken care of the CPU issue.
<br>
<br>
I'm aware this project would be so much simpler to do with a Steam Deck, especially knowing that they can run full versions of Windows and that it has much better processors than I would get even with the new versions of the Pi. This way would take away from the spirit of the project, however, the goal after all is to make a game and then play said game on a console of my making. So, that's where things stand right now. Cheers.
<br>
