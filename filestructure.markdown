---
layout: default
title: How the File Structure Works
permalink: /filestructure/
---
# The File Structure

This part is a bit more complicated, and it's just because of the million different moving parts. Everything needed for this game to work is stored in a single main folder, and breaks down into various subfolders with images or information stored as text or excel files. This ranges from the default settings, to load folders and files, to units' characteristics, a chapter's structure, etc.

## Basic File Structure for a Single Level:
<img src="/assets/allmaps level.png" alt="">
<br>
The level is split into 4 parts - introduction conversation, prior to battle conversation, the actual gameplay, and the end conversation. The conversations naturally build up the plot and characters. The ALLYSTART folder houses information on where your allies begin the chapter at (customizable later on), and the ENEMYSTART folder contains detailed information on each enemy - everything from their location, level, class, weaponary, move status, grouping, faction, and more. The last two folders contain information on how enemies or neutral parties can be recruited to your cause and what chests can be opened (and their loot), as well the houses that can be visited. Those last couple of things are broken down on my features page.

The WINCONDITIONS I explain in my video on the map maker page, but I also go over that in one of the "code" subpages if you wan to look there.
<br>
<br>

## Enemy Saves
Since I brought up the different attributes of the enemies save folder, here is how it looks:
<img src="/assets/enemy load for new map.png" alt="">
<br>
As mentioned the various lines will define the character when they are first loaded into the chapter based off all the different attributes I mentioned above. The ally folder is remarkably similar, the only difference really is that they have a "death quote", i.e. if they die in battle they'll give some sort of farewall or sarcastic comment before they die. The enemy file also contains their "groupings", or which enemies they will move with if others in their group are activated. You don't want the enemy to try and lone wolf anything after all, that would be too easy.
<br>
<br>

## Chapter Saves and Suspend Points
One of the important, and initially very frustrating, parts of this game is the ability to save the game and reload right to where you left off. After all, no one wants to be forced to finish out an entire chapter just because they'll lose progress.  This image details the map save settings for a suspend point:
<img src="/assets/suspend savemap folder.png" alt="">
<br>
This lists what map features have already been interacted with, for example doors opened or villages visited. It's also worth noting that in the main suspend point folder it lists other information as well, including what characters have already died at that point, which have moved, health lost, etc.
That is largely detailed in the "EXTRA" folder, as seen below:
<img src="/assets/suspend info.png" alt="">
<br>
It saves some of the information I just alluded to, but also the turn number and money left (if some was spent at an armory for example). A chapter save has the exact same information a suspend save does, however the suspend file contains information that changes within a file.
<br>
<br>

## Weapon Files and Weapon Proficiency
Every weapon that belongs to a player is saved in their specific folder, and saves as the following (left image):
<img src="/assets/weapon save and wpn proficiency.png" alt="">
There are a total of 5 slots for weapons or gear per person. The example file on the left details a weapon's name and the bottom two numbers are uses left out of the maximum uses. The WPN_PRO (weapon proficieny) file dictates a character's ability to use weapons based off the required skill. Essentially, higher uses in a certain weapon class = higher skill, starting out at the bottom from E, to D, C, B, A, S (Special). Those 8 rows of 0s is an individual with no experience in any weaponary (swords, lances, arrows, magic, etc etc). The convoy saves items in the exact same way as the first text file - item name, followed by the uses left out of max uses. The max uses needs to be there for when I will add the weapon restore staves - think "Hammerne" from Shadow Dragon. When it comes time to actually use those weapons in the game, it's attributes have already been pulled by finding the weapon (based on its name) in a large spreadsheet. This will list it's damage, hit percentage, weapon class, weight, etc. [This page details how that works.](/code/loading_from_spreadsheets) These attributes will affect whether or not you, or the enemy, hit their target and if so, how much damage will be dealt after accounting for the opponent's defense. The information that stays with the weapon throughout chapters are its uses, eventually the weapon will "break" with enough uses, and yes I made a quick animation / screen for that.

