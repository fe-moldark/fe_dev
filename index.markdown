---
layout: default
title: Welcome
#permalink: /welcome/
---

<html lang="{{ site.lang | default: "en-US" }}">
  <head>
	  
    <!-- Global site tag (gtag.js) - Google Analytics -->
    <script async src="https://www.googletagmanager.com/gtag/js?id=G-BCMY82GELL"></script>
    <script>
      window.dataLayer = window.dataLayer || [];
      function gtag(){dataLayer.push(arguments);}
      gtag('js', new Date());

      gtag('config', 'G-BCMY82GELL');
    </script>
  </head>
</html>

Welcome to FE Moldark, a website dedicated to documenting the complete recreation of the Fire Emblem game - everything from the graphics, a custom storyline and the various functions involved. FE Moldark is written entirely in Python v2.7, an old version of Python, yes, however this project began over 7 years ago and has been periodically worked on since. The code is completely original and throughout this site (and my youtube channel) I go into how different parts of it work.

The code currently stands at 15,000 lines, a challenge to keep up with for sure. For those familiar with the Fire Emblem series this is because I am attempting to incorporate functions from every aspect of the game; opening doors and chests, healing and warping staffs, including a convoy screen and adjustable map before going into battle, trading items, armory and vendors, recruitable units, there are a million different aspects already involved and a million more to go. One major accomplishment is the loading screen, sounds simple, I know. Now you are able to not just load a chapter and play with those units, but successively update into save files as well as the ability to save mid-game (think the "suspend" option for those familiar).

On a fundemental level, the tilemap is already setup in a grid, and the map is loaded into multiple arrays to display on the screen and to control / limit player movement. That would be the core of what the games works off of, the rest of this site will go into more details about how the rest of it comes together. There is no graphics team, programming and design team, gameplay and story departments, etc. It’s basically just me tackling them all as best I can on my own, which while it allows me to implement exactly what I want into the game, it also takes a good deal more time.

Feel free to browse around - I have already made and am working on multiple pages to showcase the various functions and features of the game, as well as some snippets of code where I break down how they work.

Enjoy.
