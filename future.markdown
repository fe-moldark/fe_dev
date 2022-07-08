---
layout: default
title: Future
permalink: /future
---

# Future of this project

I'd recommend reading through the "History" tab first, otherwise this next part will not make much sense. 
<br>
Now, I have yet to completely solve the uncharacteristcally high CPU usage (although I may have narrowed down why that is), I was able to try out the game at slow speeds on the 3.5" screen on my wooden console. And it didn't quite seem right. That is great for playing old GBA-style games who's screens are designed to be that small, but it didnt't work with my game. This is even with me considering reorganizing / reducing the number of tiles to make the game fit onto a smaller screen, adjusting all the text size, etc etc. So I tried it on a 7" display that I've previously used to display a constant stream of the International Space Station (fun project), and quite honestly I loved it. Not only does everything look "fullsize", or just a natural size for the graphics, but everything from the text being readable to how I think the game should look felt right. 
<br>
To counter the issues I've seen using different Linux distributions and installing pygame there I have had thoughts of using a) Windows IoT on the Pi or b) using an old Windows 10 tablet (since they run a FULL version of Windows, not just the Windows IoT Core version. That will only be if all else fails since I want a light-weight OS.
<br>
Outside the scope of converting everything to work on Linux and getting pygame to work there, that means I will have to design an entirely new case for the 7" screen. And so taking inspiration from the Steam Deck and the Switch, I've designed the following:
<br>
<img src="/assets/console1.png" alt="">
<br>
The top image is how the console will look in a perfect world. Below that is a to-scale sketch of how all the parts will fit together. As you can see there are a LOT of parts to this, more than I used for my last console. It includes a 10,000mAh battery, as well as powerboost board and a power switch that attaches on to it. There's a basic class D MAX98306 audio amplifier that will have speakers on both sides of the console. (I am also using a slide potentiometer for volume control). I took apart one of my old USB joysticks and will be using the board, but rewired, to buttons on the e.g. PiGrrl Zero Gamepad. This also me to have more freedom in design while still conviently keeping the USB aspect which is good for looping through events in pygame. Other things I will be including are a power indidcator LED and a fan for cooling. Here's a more spacious rendition of how this will all (sort of) fit together.
<br>
<img src="/assets/console2.png" alt="">
<br>
There are a lot of parts here that will need very small and precise forms in order for this to all fit together. That's why I've decided to go the route of a 3D printer. There's gonna be a very steep learning curve, I'm aware, but I think this is the best route. It also doesn't hurt that I've always wanted a 3D printer because who hasn't wanted one? I will begin designing the as soon as I've taken care of the CPU issue.
<br>
I'm aware this project would be so much simpler to do with a Steam Deck, especially knowing that they can run full versions of Windows and have much better processors than I would get even with a Pi4. This way would takes away from the spirit of the project, however, the goal after is to make a game and then play said game on a console of my making.
<br>
