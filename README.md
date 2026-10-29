#Active World State -  Kingdom Decay System
>A system to simulate Stampede-like event from Lit-RPG stories. This system idea is to put pressure to players and to make the world actively respond to players’ actions. Monsters will spread to the overworld fields or sub-zones. Preferably for MMORPGs since they have high active player counts.

## Table of Contents
[1. Overflow Conditions](#1-overflow-conditions)

[2. System Escalation & World States](#2-system-escalation--world-states)

[3. Node Resolution & Restoration](#3-node-resolution--restoration)

[4. Essential Technical Setup]($4-essential-technical-setup)

[5. Technical Breakdown] (#5-technical-breakdown)

## 1. Overflow Conditions
	Overflow will happen automatically on conditions.
  If a dungeon goes neglected for several days, the monsters will pour out to the immediate field. This will create Overflow condition.

## 2. System Escalation & World States
	If the Overflow is not handled, it will infect to the nearby fields.
  Settlement won’t be free from this infection. If the adjacent field is in Overflow, the people will be in panic and the trades get disturbed. As the result, the price will inflate. This is a Chaos state.
	If the Chaos is not handled, the settlement’s people will migrate and no people and economy get left behind. Effectively creating a ghost town. This is Collapse state.
	Furthermore, if the infection keeps on progressing and spread to most areas of a Kingdom, then the Kingdom will migrate everyone.
  With no military to handle the monsters, all areas will be taken over by those monsters. This is Kingdom Collapse state. The monsters will be more aggressive.

## 3. Node Resolution & Restoration
	For the resolution and restoration of the infections:
  -	Dungeon: doing culling will settle the Overflow and prevent the pouring to the adjacent field.
  -	Field: there is a need to kill monsters from the dungeon. There will be Elite comes out to take a revenge for the pawns. Killing this monster will make the monsters retreat back to where they come.
  -	Settlement (Chaos and Collapse): people will return later when the surrounding fields are cleared out from the Overflow.
  -	Kingdom Collapse: reclaiming most of the fields and settlements will call back the Kingdom’s military and they will help restoring the Kingdom’s order into normal state.

## 4. Essential Technical Setup
	There are several things to look out, they are:
  -	New players must have a place to be safe. The easiest location to think of is Adventurers’ Guild Headquarter with the guild veterans handling surrounding fields’ conditions.
  -	New update will be in trouble if players cannot handle the dungeon when the pressure builds up. Kingdom’s guards may have a way to help this issue.

## 5. Technical Breakdown
	This is the explanation of this system idea using example numbers. Developers need to adapt to the game world and server condition.
-	Do all checks on server reset except several state changes. This is to reduce the server overhead. Keep the numerals hidden from payers. This system may use game’s working system already, like enemy defeated on a map report to server.
-	Dungeon neglect is only integer number of total kill in the dungeon, not limited to 1 floor. For example, 5,000 monster kills per day. Then a check will compare total kill on server reset. If not fulfilled, +1 on consecutive neglect counter: if fulfilled, the counter reset to 0. If the counter is equal or more than a set number, for example 7 days, then the system is in full work.
-	When the neglect is fulfilled, immediate field or sub-zone will change the spawn table from normal to Overflow; it is dungeon F1 spawn table. Better set the pair in beforehand to avoid crashing to another dungeon’s territory or creating unnecessary confusion. Change the skybox to help player understands the change.
-	Overflow Field will have similar counter and kill count. For example, 3 days and 2,000 kills. Unlike dungeon, the kills won’t reset the state to normal. It will spawn elite monster, better taken from rare spawn from F1 table. Set it only as the key for recovery and gives no exp and no loot. To prevent players to try to farm it. If the overflow field reaches the threshold (3 days neglected), then it will propagate to all adjacent fields. 
-	On settlements, caravans, villages, towns, and capital, if any of the adjacent field is in overflow, then the settlement will turn into Chaos state. No need to change many things. Only need to add new dialogues for that state and inflate the item prices. For example, +200%. It is set that high to punish player base for ignoring the monsters’ march.
-	The settlement will turn into Collapse state if it is hit directly by the overflow. The condition of this happening is when the overflow field is not recovered for 3 days. This state will de-spawn NPCs and change the skybox.
-	Finally, the Kingdom Collapse. This event happens when a set percentage of the kingdom’s area hit by the overflow (collapsed for settlements), for example 50%. This state will change other fields and settlements into overflow state and collapse state. In this state, the propagation speed will not stay the same (3 days), but quicker (1 day for example). Same set percentage or other number is required to recover the total area of the kingdom, 50% in this example. Since the propagation is faster, this event will be like a tug-of-war between the system and player base. 
-	When the Kingdom Collapse is recovered, all of the fields and settlements reset into normal. Dungeons will reset to 0 neglect counter.
-	One thing to consider, the propagation should not exceed the kingdom’s border.
-	Save haven for new players will be a separate area with guild HQ and its surrounding fields that will be immune to overflow. This area is set for the base in case total server collapse happened; all kingdoms and realms are in collapse state.
-	For new updated area, it will be unfair to make the dungeon counter active immediately. There will be not enough player to reach the kill count. The counter should freeze. To show its state, there will be guard or knight NPCs on the entrance and maybe in some floors. The handover to player will be per dungeon, when a set condition is fulfilled by a number of unique players. For example, those who can dive into F3 of the dungeon. By assumption that they could kill the F1 monsters without problems. When enough player number is reached, the NPCs will de-spawn.
