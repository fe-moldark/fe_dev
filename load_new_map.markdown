---
layout: default
title: Loading a New Map
permalink: /code/load_new_map
--- 


# Loading a New Map:

This is obviously a very core function and one that takes a lot of work. Similar to what I explained on the "File Structure" page, there are so many different things that need to be loaded. Everything from loading weapons and items into objects, loading friendly and enemy units into sprites, the game map, basic settings, etc. And then when you get into the suspend saves you also have to deal with what doors and what chests at what locations have been opened, unit's new locations, their health, weapon uses, whether or not they have moved yet that turn, etc etc.
<br>
<br>
Suffice to say, it is quite a lot of code - over 1,100 lines of it to be precise. If you want to skim through the code yourself I wil link that file down below. It's actually one of the better documented parts of this program (for obvious reasons), so following it should not prove to be too difficult. Interesting fact, as this function is ~1,100 lines long it alone makes up over 7% of the entire code for the program. That's a lot for just one function, but thankfully it is only called whenever a new level is loaded, and it is quicker than you think.
<br>
<br>
Here is the file if you wish to download: 
[test to download file here][1]

[1]:{{http://127.0.0.1:4000/}}/_downloads/load_new_map.py
