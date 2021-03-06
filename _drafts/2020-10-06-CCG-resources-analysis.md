---
layout: post
title:  "DragonAutochess DES308 Dev Log 1"
date:   2020-09-29
excerpt: "Brainstorming on the Leveling Mechanic"
project: null
tag:
- des308
- game design
- dev log
- AutoDragonchess
comments: false
---

These past few days I've been thinking on how to make a different leveling mechanic for the game. 
I want to change the formula that all the auto-battlers have used so far; a bit because I believe it would poorly translate for a purely singleplayer game, a bit because the math doesn't check out with a core change I want to make, and a bit because I just want to try something new.

There are two main changes I want to test, each one with their fair share of challenges to overcome. I'm going to talk about them but I won't go into too many details as:<br> 
_1._ I still don't know either<br>
_2._ and/or it has to be playtested because it heavily relies on balance.

## Increase the maximum level of units.

<figure>
 <a href="/assets/img/old-leveling-graph.jpg"><img src="/assets/img/old-leveling-graph.jpg"></a>
    <figcaption>Traditional Leveling Graph</figcaption>
</figure>

Traditionally auto-battlers have maintained the leveling structure shown in the picture above, or in mathematical terms
\\[ level(x)=3^{x-1} \\]
This presents a pretty big issue when I decide to increase the maximum level: the amount of units needed grows exponentially, if we wanted to have a 4 star (the technical term used in the genre so far, from now on I'll be using star and level interchangeably) we would need: \\[ {3^{3}}={27} \\] units. And if we go to 5 stars it would grow to: \\[ {3^{4}}={81} \\]

And we are already in the basically impossible territory.

So the first thing is going to make the leveling follow a linear function. something akin to 

\\[level(x)=3x-2 \\]

This basically means that every unit starts at level 1 and then everytime you find three more units of the same type, it levels up. 


## Units can have more than one spell.
The second change is a lot more experimental and revolves around giving units more spells (for now I'm thinking around 3 or 4).
As I said in [the previous post]({% post_url 2020-09-23-DES308-week-1 %}), the game is going to be somewhat inspired by Dungeons and Dragons, and an additional layer of complexity I might want  to try is multiclassing: being able to give some unit spells from another class.

For now I have three possible ideas, each with a couple of variations, so lets get started.

### 1. The unit level is the sum of the levels of the spells
In this one, there would be limited ways to acquire units, probably once every three or four fights, but after every fight you get a shop like in any every other auto-battler (random units, and can spend money to reroll them) where you can buy spells. The spells would be class-specific. 
Instead of leveling the units directly, getting duplicates of spells increase the spell level, and the unit level would be the sum of the levels of all the spell to it assigned.

#### Variant

The variant for this leveling system would be to instead have the units level separately (via duplicates), therefore probably, making units acquisition a bit faster, and have the number of spells assignable to it depend on the unit level _(e.g.: a level 1 unit can only have one spell, but a level 3 unit can have 2)_.

### 2. Units of the same class can have different spells

This one is the vaguest idea and one I really can't decided how I feel about. The idea is to have each unit only have one spell from among the class spell list.
To level up a unit you need three units of the same class, but not necessarily with the same spell; the leveled up unit would then get the spells that other units used had and increase the spells' levels accordingly.<br>
__E.g.: The unit in question as _Spell 1_; to level it up we use to units with _Spell 2_; the now level 2 unit would have _Spell 1_ at level 1 and _Spell 2_ at level 2.__

### 3. Level up units and they get more spells as they do

This is the simplest idea and the one I'm leaning on for now. It follows the more traditional path of auto-battlers, as in you can only buy units and you level up units with duplicates, but instead of just increasing their one spell in power each level-up, they gain additional ones first, and then upgrade them in sequence.
__E.g.: Get Spell 1 -> Get Spell 2 -> Get Spell 3 -> Level Spell 1 -> Level Spell 2 ...__

#### Variant

Here we can introduce multiclassing in a pretty elegant way in my opinion; my idea for now would be making an item that permanently changes the character class, and therefore everytime it levels it now gains spells of the new class.

## In conclusion

For now I don't want to overcomplicate my life too much, therefore I'll go with the third idea without implementing the multiclassing variant. After I will get some feedback I'll then decide if continuing with that one, maybe including the multiclassing or changing system altogether.