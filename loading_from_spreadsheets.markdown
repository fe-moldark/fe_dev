---
layout: default
title: Loading Unit Classes and Weapons from Spreadsheets
permalink: /code/loading_from_spreadsheets
---

# Loading Unit Classes and Weapons from Spreadsheets

## Unit Classes

Below is how you would load an enemy into their class. I guarantee there is a more efficient way to do this, but I wrote this part a long time and have had zero issues. "If ain't broke, don't fix it" and all that.

```python
def returnClass(y):
    name=str(sheet.cell_value(y,1))#["A"+str(y)].value)

    saveWpnTypes=[]
    divide=str(sheet.cell_value(y,15))

    wpnTypes=divide.split(",")
    for weapon in wpnTypes:
        newW=weapon.replace("\"", "")
        saveWpnTypes.append(newW)
    
    addStats=[]
    for j in range(4,14):
        addStats.append(int(sheet.cell_value(y,j)))

    addLvl=[]
    for j in range(18,26):
        addLvl.append(int(sheet.cell_value(y,j)))

    pic=pygame.image.load(str(sheet.cell_value(y,16).replace("\"", "")))
    pic_grey=pygame.image.load(str(sheet.cell_value(y,17).replace("\"", "")))

    actualName=str(sheet.cell_value(y,0))
    return [name,saveWpnTypes,addStats,addLvl,pic,pic_grey,actualName]
        
class EnemyClass:
    def __init__(self,theList):
        name=theList[0]
        WeaponTypes=theList[1]
        stats=theList[2]
        newLvl=theList[3]
        pic=theList[4]
        pic_grey=theList[5]
        actualName=theList[6]
#some of this redundant, I know
        self.name=name
        self.actualName=actualName
        self.WeaponTypes=WeaponTypes
        self.stats=stats
        self.newLvl=newLvl
        self.pic=pic
        self.pic_grey=pic_grey

        EnemyClass.name=self.name
        EnemyClass.actualName=self.actualName
        EnemyClass.WeaponTypes=self.WeaponTypes
        EnemyClass.stats=self.stats
        EnemyClass.newLvl=self.newLvl
        EnemyClass.pic=self.pic
        EnemyClass.pic_grey=self.pic_grey

```
So for example, me calling the "Brute" enemy into its class from the spreadsheet would appear as:
`Brute=EnemyClass(returnClass(1))`
<br>
This would call on the second line in the spreadsheet (first line is 0, so second line is 1, etc).

<br>
##  Weapons
For the weapons it is a very similar process. A small subset of the weapons spreadsheet is pictured below:
<img src="/assets/spreadsheet_weapons.png" alt="">
So, when it loads up a player it uses the name of whatever items they have and checks them against an allGear list which contains all weapons, staves, items, and usable items (which are stats boosters and things like master seals).
```python
def returnItem(name):#
    for item in allGear:
        if str(item.name)==str(name):
            if str(item.__class__.__name__) == "Staff":
                new=Staff(item.name,item.rank,item.rang,item.uses,item.max_uses,item.addHeal,item.addXP,item.wpnType,item.value)
            elif str(item.__class__.__name__) == "Weapon":# or str(item.__class__.__name__) == "Staff":
                new=Weapon(item.name,item.rank,item.rang,item.uses,item.max_uses,item.weight,item.dmg,item.hit,item.wpnType,item.value,item.crit)
            elif str(item.__class__.__name__) == "Item":#class item
                new=Item(item.name,item.value,item.uses,item.max_uses)#
            elif str(item.__class__.__name__) == "UsableItem":#self,name,value,uses,max_uses,bonusWhat):
                new=UsableItem(item.name,item.value,item.uses,item.max_uses,item.bonusWhat)
            break
    try:
        return new
    except UnboundLocalError:
        print name, "ERROR on this one, possibly using an old save with a replaced weapon type"
        pygame.quit()
        sys.exit()

#below is an example class for an Item
class Item:
    def __init__(self,name,value,uses,max_uses):
        self.name = name
        self.value = value #(cost)
        self.uses=uses
        self.max_uses=max_uses

        Item.name=self.name
        Item.value=self.value
        Item.uses=self.uses
        Item.max_uses=self.max_uses
        
        
```

After this loads, if we are in a suspend save the "uses" attribute will change accordingly.

