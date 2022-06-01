---
layout: default
title: How the Arrows work on the Move Map
permalink: /code/arrows
--- 


# How the Arrows work on the Move Map:

For some visual context's sake, here is how the arrows appear in-game:

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZOz9ITXQrGg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>
This function is actually separate from the move map itself (which is also a page in "Code"), however it does draw from the free_space_list that is generated from a function involved with the move map, called show_map().
<br>
<br>
Besides being a nice visual for the player, it is also important as it dictates how your unit will move since there may be more than one path to a certain location. This matters when there are unseen traps laid out the ground, or when fog of war is activated for the level at which point a unit's move path becomes much more important.
<br>
<br>
If you go from a tile not in the free_space_list (blue squares) to one suddenly back in the free_space_list, it will perform a quick calculation to find the shortest path there. Similarly if you move to another tile that is still with the free_space_list but more than your unit's maximum move, it will recalculate a route for you (since this means they can get there, but not by your current route). If you just move the arrow to a new tile, within the free_space_list and under the maximum moves for that unit, it will simply append that next move location to the runPath.
<br>
<br>
To clarify one thing on the code below, when you first select a unit the initial runPath is simply their location. The rest of the code speaks for itself if you can follow python.

```python
def arrows(runPath,newSpot,free_space_list):#runPath
    try:
        lastSpot=runPath[-1]
    except IndexError:
        runPath=[(MoveWho.y,MoveWho.x)]
        lastSpot=runPath[-1]
        
    neighbors=[(lastSpot[0]+1,lastSpot[1]),(lastSpot[0],lastSpot[1]+1),(lastSpot[0]-1,lastSpot[1]),(lastSpot[0],lastSpot[1]-1)]

    if newSpot in runPath:#go back on list
        while newSpot in runPath:
            runPath=runPath[:-1]
        runPath.append((newSpot[0],newSpot[1]))
    elif newSpot == (MoveWho.y,MoveWho.x):#if back at "home base", reset runPath
        runPath=[(MoveWho.y,MoveWho.x)]
    elif newSpot in free_space_list:
        if len(runPath)<=(MoveWho.move) and newSpot in neighbors:
            runPath.append((newSpot[0],newSpot[1]))
        else:#means in a spot in my free_space_list, but cant reach by current path, so use pathfinding program here
            useGrid=flyingOrGround(MoveWho)

            matrix = []
            for row in range(mapHeight):
                new_row = []
                for column in range(mapWidth):
                    if useGrid[row][column] == 0:
                        new_row.append(1)
                    else:
                       new_row.append(0)
                matrix.append(new_row)
                
            for enemy in enemy_sprites_no_edit:
                matrix[enemy.y][enemy.x]=0
                
            y1 = mov_y+array_addy
            x1 = mov_x+array_addx
            matrix[MoveWho.y][MoveWho.x] = 1

            grid_pathfind = Grid(matrix=matrix)
            start = grid_pathfind.node(MoveWho.x,MoveWho.y)
            end = grid_pathfind.node(x1,y1)
            
            finder = AStarFinder(diagonal_movement=DiagonalMovement.never)
            path, runs = finder.find_path(start, end, grid_pathfind)

            runPath=[]
            for item in path:
                runPath.append((item[1],item[0]))
    arrows.runPath=runPath
 
```
<br>
When blitting the arrows themselves it uses the following tiles:
<img src="/assets/arrows_img.png" alt="">
<br>
Each is oriented their own way - connect east to west, turns north to east, etc.

When it comes time to blit the arrows themselves it has to go through a seperate function. It goes through each location in the runPath and relates each pos to the previous and next spot to create the arrow map you saw in the above video. Full code:

```python
def showArrows():
    if ShowMap is True:
        iis=0
        if displayTrade is False and displayInventory is False:
            for run in runPath:
                if iis != 0 and iis < len(runPath)-1:
                    thisSpot=(run[1]-array_addx,run[0]-array_addy)#as x,y

                    if runPath[iis-1][1] > runPath[iis][1]:
                        if runPath[iis+1][1] < runPath[iis][1]:
                            thisArrow=arrowleftright
                        elif runPath[iis+1][0] > runPath[iis][0]:
                            thisArrow=arrowbottomright
                        elif runPath[iis+1][0] < runPath[iis][0]:
                            thisArrow=arrowtopright  
                    elif runPath[iis-1][1] < runPath[iis][1]:
                        if runPath[iis+1][1] > runPath[iis][1]:
                            thisArrow=arrowleftright
                        elif runPath[iis+1][0] > runPath[iis][0]:
                            thisArrow=arrowbottomleft
                        elif runPath[iis+1][0] < runPath[iis][0]:
                            thisArrow=arrowtopleft
                    elif runPath[iis-1][0] < runPath[iis][0]:
                        if runPath[iis+1][1] < runPath[iis][1]:
                            thisArrow=arrowtopleft
                        elif runPath[iis+1][1] > runPath[iis][1]:
                            thisArrow=arrowtopright
                        elif runPath[iis+1][0] > runPath[iis][0]:
                            thisArrow=arrowtopbottom
                    elif runPath[iis-1][0] > runPath[iis][0]:
                        if runPath[iis+1][1] < runPath[iis][1]:
                            thisArrow=arrowbottomleft
                        elif runPath[iis+1][1] > runPath[iis][1]:
                            thisArrow=arrowbottomright
                        elif runPath[iis+1][0] < runPath[iis][0]:
                            thisArrow=arrowtopbottom

                    screen.blit(thisArrow,(thisSpot[0]*tilesize,thisSpot[1]*tilesize))

                if iis == len(runPath)-1 and iis != 0:
                    
                    thisSpot=(run[1]-array_addx,run[0]-array_addy)#as x,y
                    
                    if runPath[iis-1][1] > runPath[iis][1]:
                        thisArrow=arrowtipw
                    elif runPath[iis-1][1] < runPath[iis][1]:
                        thisArrow=arrowtipe
                    elif runPath[iis-1][0] < runPath[iis][0]:
                        thisArrow=arrowtips
                    elif runPath[iis-1][0] > runPath[iis][0]:
                        thisArrow=arrowtipn
                    screen.blit(thisArrow,(thisSpot[0]*tilesize,thisSpot[1]*tilesize))
                iis+=1
```
