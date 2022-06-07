---
layout: default
title: Map Maker Page
permalink: /mapmaker/
---

# Map Maker

When I first started making a map for the game it was very simple and more or less used for testing functions and how the map affected movement, etc. Once I started creating multiple maps for different levels, however, it became apparent I needed an easier way to create maps which led to this side project.

This program is also written in Python v2.7 and uses Pygame as well, and is appropriately called "Map Maker". I'll get into the various features of the program here in a second, but if you want to see how it actually works in practice I've linked a video (associated with the same youtube account as this site) down below:
<iframe width="840" height="445" src="https://www.youtube.com/embed/watch?v=jkbnEvTVbpo&list=PLecUQNqdK8lSmqQErHC5WlEA_KyjvJHH8&index=8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br>
<br>

A more simple breakdown:

1) Select whatever level / map you are working on located on the right side. Hit the "print to txt file" when done to save that automatically to the appropriate file for the game located on my local system.
<br>
2) Options are either to edit / move around the map, or to edit the units for the chapter.
<br>
3) When editing the map and saving it, it saves in the following format:
<img src="/assets/how maps are saved.png" alt="">
<br>
To explain, each line represents a row, and each column within is seperated by the parantheses and comma. The part in quotations is the tile name located in the default python folder, and the number next to it represents at what rotation it is saved for that tile (in 90 degree increments naturally). When the chapter loads up in the game it loads each as its own pygame.image surface and rotates it accordingly before adding it to the overall array in play. From there your view of the map is dictated by how you move the cursor around the map, which is tracked by the actual blitted location - mov_x, mov_y, and how the map is shifted - array_addx, array_addy. I hope that makes sense.

Below is an image, or collage, of (I believe) all the tiles currently in use. All of them (except for the blue/green armor and mountain tile) were made by me solely using Gimp, here it is:
<img src="/assets/all tiles.png" alt="">
<br>
I covered most of the functions of the program in the above video, everything else ties more into the actual functionalities of the game itself and not this side project. That being said, I am proud of how this simple program turned out since it was able to automate a lot of the work I was doing manually and save time, including not just creating the map, but adding enemies and customizing them to the level.



If you want to see some actual (sped up) captures of me making custom maps / recreating maps from various FE games, I will include that below as well. These are mainly older captures and so you'll notice some features are not available as were seen in the first video on this page, but it still does a good job showcasing how it works:

<iframe width="840" height="473" src="https://www.youtube.com/embed/watch?v=kh88FvpEo6I&list=PLecUQNqdK8lSmqQErHC5WlEA_KyjvJHH8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Link to full playlist: [Map Maker Playlist](https://www.youtube.com/playlist?list=PLecUQNqdK8lSmqQErHC5WlEA_KyjvJHH8)

