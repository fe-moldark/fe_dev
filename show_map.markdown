---
layout: default
title: Creating the Move Map
permalink: /code/show_map
--- 


# Creating the move map:

When creating the move map for an individual unit there are more factors to consider than you might think. By default, the level loads in the map at the very beginning and a basic array that is further manipulated based off the unit during your turn.
<br>
<br>
Factors that influence the unit's movement include:
<br>
-default impassable tiles (think high mountain ranges)
<br>
-what type of unit, grounded or flying - ex. flying units can move over water
<br>
-enemies limit movement, you can't move through them or land on their location
<br>
-if fogOfWar is True, the above statement will need to change
<br>
-you need to allow the ability to move through ally spaces, but not able to land on their space
<br>
-ensuring any movement past the parameters of the map is dealt with proper error handling
<br>
<br>
This first snippet of code is the process used to create the free_space_list. It calls on the show_map function which I will go over after this explanation.
```python
free_space_list = []
second_new_player_list = []
third_new_player_list = []

#MoveWho=selected unit
y1 = MoveWho.y
x1 = MoveWho.x
move1 = MoveWho.move #what is their movement range, anything from 4-10 tiles
new_player_list = [(y1,x1)]#begin with starting location



show_map(new_player_list, second_new_player_list, MoveWho)#starts off with starting location and an empty list

for i in range((move1-1)):#number of iterations based off unit's movement
    show_map(second_new_player_list, third_new_player_list, MoveWho) #returns updates the third_new_player_list
    
    second_new_player_list = []
    
    for item in third_new_player_list:#dump discovered locations for next iteration. This quickly builds a unit's move map
        second_new_player_list.append(item)

#
for item in ally_sprites_no_edit: #if an ally occupies a free space, remove it. You can still pass through there, but cannot settle there
    if (item.y,item.x) in free_space_list:
        free_space_list.remove((item.y,item.x))

free_space_list.append((y1,x1))
```


This next part is the show_map function that is used to create the free_space_list and when actually showing the map, or blitting the map onto the screen. 

The screen has a set number of tiles for the width and height, and it adjusts your screen in response to movement of the arrow keys (soon to be actual buttons). In order for the window to adjust, I created the array_addx, array_addy variables that tell you how far off from (0,0) you are.
<br>

To better explain, a "normal" map would show tiles x from (0-17) mapwidth and y (0-11) mapheight, however most maps will easily exceed this size. So, if as you move around the map the screen shifts say 2 tile across and 1 down, your array_addx, array_addy would be (2,1). Now whenever there are any blitting actions or interactions with the game, those two variables are used with the default mov_x,mov_y (which are the cursor locations). The cursor locations are always consistent with their actual location (i.e. can and will exceed the 18x12 map display), when blitting that main cursor, however, you would actually end up subtracting the array_add values. Hopefully that makes sense, but I feel like it won't. Here's the function for all of that:



```python
def show_map(y, z,who):
    grid=flyingOrGround(who)#function for grid that limits players' movement
    #think a flying unit vs mounted, their maps are different

    pls_count_this=0
    if fogOfWar is False:
        for item in enemy_sprites_no_edit:
            grid[item.y][item.x] = 1 #make enemy units APPEAR as NOT blocked / occupied squares in array
            pls_count_this+=1
    else:#fog of war is true
        fogFreeList=[]
        lookRange=3#default for normal units
        for item in ally_sprites_no_edit:
            if item.clas.name=="Thief": #thieves get to see further
                lookRange=10

            if item.hppart > 0: #just making sure they didn't die this turn...
                if item == SaveMoveWho:
                    
                    USE=SaveMoveWhoPos
                    if item.picture==item.backup_grey: #so - without this a player that moved would be able to see the new 3 tile radius at their new position, this prevents that
                        USE=(item.x,item.y)
                else:
                    USE=(item.x,item.y)
				
				#don't forget this is cycling through all ally units
				#the fogFreeList collects all tiles that should be "cleared" of the fog
                fogFreeList.append((USE[0],USE[1]))
                for i in range((-lookRange),(lookRange+1)):#lookRange either 3 or 10
                    for j in range((-lookRange),(lookRange+1)):
                        #(item.x-(array_addx),item.y-(array_addy))
                        if (USE[0]+i)<=mapWidth-1 and (USE[0]+i)>=0 and (USE[1]+j)<=mapHeight-1 and (USE[1]+j)>=0:
                            if (USE[0]+i,USE[1]+j) not in fogFreeList:
                                if abs(i)+abs(j)<=lookRange:
                                    fogFreeList.append((USE[0]+i,USE[1]+j))

        fullFogList=[]
        for i in range(mapHeight): #long version of creating a new array
            THELIST=[]
            for j in range(mapWidth):
                THELIST.append(0)
            fullFogList.append(THELIST)
        for item in fogFreeList: #adjust fullFogList according to the free spaces in fogFreeList
            fullFogList[item[1]][item[0]]=1
            
        for item in enemy_sprites_no_edit:
            if fullFogList[item.y][item.x]==1: #this will only add enemies as blocked tiles on the grid if they are in tiles that have been removed from the fullFogList from the fogFreeList before
                grid[item.y][item.x] = 1
                pls_count_this+=1

    for item in y: # work to build out the player's free_space_list
        x,y = (item[0],item[1])
        if x+1 > mapHeight:
            check1 = x
        else:
            check1=x+1
        if x-1 < 0:
            check2=x
        else:
            check2=x-1

        if y+1 > mapWidth:
            check3 = y
        else:
            check3=y+1
        if y-1 < 0:
            check4=y
        else:
            check4=y-1

        try:
            if grid[check1][y] is 0:
                if (check1,y) not in free_space_list:
                    free_space_list.append((check1,y))
                if (check1,y) not in new_player_list:
                    z.append((check1,y))
        except IndexError:
            pass

        try:      
            if grid[check2][y] is 0:
                if (check2,y) not in free_space_list:
                    free_space_list.append((check2,y))
                if (check2,y) not in new_player_list:
                    z.append((check2,y))
        except IndexError:
            pass

        try:
            if grid[x][check3] is 0:
                if (x,check3) not in free_space_list:
                    free_space_list.append((x,check3))
                if (x,check3) not in new_player_list:
                    z.append((x,check3))
        except IndexError:
            pass

        try:
            if grid[x][check4] is 0:
                if (x,check4) not in free_space_list:
                    free_space_list.append((x,check4))
                if (x,check4) not in new_player_list:
                    z.append((x,check4))
        except IndexError:
            pass
    #
    if fogOfWar is True:
        show_map.fogFreeList=fogFreeList
        #above just defines one of the functions' variables that I use later on
```
