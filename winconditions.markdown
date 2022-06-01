---
layout: default
title: Win Conditions
permalink: /code/winconditions
---

# How Win Conditions works

<span style="text-decoration: underline">So far I have programmed 5 different ways to win a level:</span>


<ol>
<li><span style="text-decoration: underline">SEIZE</span> a location on the map (think defeating a boss on a throne, then seizing it)</li>
<li><span style="text-decoration: underline">ROUT</span> (or kill) all enemy units in play.</li>
<li><span style="text-decoration: underline">KILL</span> a specific enemy unit in play.</li>
<li><span style="text-decoration: underline">SURVIVE</span> simply means survive x number of turns, think of it as needing to outlast hordes of enemies for only so long. Survive is not handled here for other reasons.</li>
<li><span style="text-decoration: underline">ESCAPE</span> has the exact same functionality of "Seize", however it's made to sound different for the chapter's intent. In both cases you need to "Seize" a certain tile to win.</li>
</ol>
<br>
Every level has its own WINCONDITIONS file that contains one of these win methods. The formatting for each looks as follows:
```
SEIZE
X
Y

ESCAPE
X
Y

ROUT

PROTECT
(name)

KILL
(name)

SURVIVE
(number of turns)
```
Very self explanatory, depending on which win condition is chosen the file is between 1 and 3 lines long. Now for how it is handled within the code - for the initial level load, that same file is loaded into a list named WINCONDITIONS. You can very easily dissect how it confirms if the different win conditions have been met, and this check occurs after every action taken by a friendly OR enemy unit.

The Seize / Escape conditions work directly from the unit's optionsList, and if selected, it will set that startEnd variable to True.
The Survive condition is checked when the turn counter increases after the enemy's turn is over and about to transition back to the player.

Full code below:


```python
if MyTurn is True or TheirTurn is True:

    #ROUT
    if WINCONDITIONS[0] in ["ROUT"]:
        if len(enemy_sprites_no_edit)==0 and waitOnXP is False and LevelUp is False:
            if (TheirTurn,(total_enemies_this_turn)) == (True,(enemy_list_brackets_x+1)) or MyTurn is True:
                startEnd=True
                
    #SEIZE-->LOCATED ELSEWHERE, DONT WORRY ABOUT IT HERE

    #KILL
    if WINCONDITIONS[0]=="KILL":
        checkForThere=False
        for enemy in enemy_sprites_no_edit:
            if str(enemy.name) == str(WINCONDITIONS[1]):#WINCONDITIONS[1] is enemy-to-kill name
                checkForThere=True
                break
        if checkForThere is False:
            startEnd=True

    #SURVIVE-------LOCATED ELSEWHERE

    #PROTECT     
    if WINCONDITIONS[0]=="PROTECT":
        checkForThere=False
        
        #if checkForThere is True, person is still alive
        for ally in ally_sprites_no_edit:
            if str(ally.name) == str(WINCONDITIONS[1]):
                checkForThere=True
                break
        
        for neutral in neutral_sprites_no_edit:
            if str(neutral.name) == str(WINCONDITIONS[1]):
                checkForThere=True
                break

        #startEnd=True
        if checkForThere is False:#if false means was nevver set to true, so not in the lists
            failedMission=True

            for ally in copy_ally_sprites_no_edit:#(copy of list created at beginning of turn)
                if str(ally.name) == str(WINCONDITIONS[1]):
                    failedMissionPerson=ally
                    break
            for neutral in copy_neutral_sprites_no_edit:
                if str(neutral.name) == str(WINCONDITIONS[1]):
                    failedMissionPerson=neutral
                    break


            #failedMissionPerson=WINCONDITIONS[1]
            #failedMissionQuote=WINCONDITIONS[2]    #WINCONDITIONS[2] is the 'death quote' of the WINCONDITIONS[1]

	if startEnd is True:#good thing
		#begin end of chapter conversation as opposed to failedMission

```

The startEnd variable indicates that the chapter will wrap up after this if set to True, and go into whatever end conversation the level has.
