# What is this place?

For testing purposes and not to clog up other repositories 
I use this to test mods themselves and keep all versions, practical or not.

When a mod is ready, I like to use the direct link and load it into the hotfix merger.

For the love of god, please don't actually use any mods in here. Even I don't know which one's still work. Go to the BL3 mod repository at https://github.com/BLCM/bl3mods for functional mods.

The joy of modding is learning how the game works together. It's fun seeing how it fits together. And breaking it. 

You can contact me below with any questions you may have. I do join voice channels and actually chat, because it's easier to explain a lot of stuff (especially modding) verbally rather than typing. Because there's a *ton* of information, and talking through it helps someone understand it better and allows them to ask questions on the fly to gain better understanding.

Please note, I am a beginner in both modding and coding, but have a solid grasp on the basic and intermediate aspects of modding. With BL3 modding, we have to reverse engineer how the game works in order to make (read: the modding community has had to make it up on the fly and apply mods.

I'm a scientist and healthcare professional, not a computer engineer.

Discord: SkyMaster#6302


# Moxxi's XP Artifact Testing

I haven't done every mayhem level (only MH11) or any enemy except the Graveward.
I'll make a spreadsheet (not a forbidden word doc) with every mayhem level on NVHM and TVHM.
I'll use only 1 gun, a grenade, shield, artifact and COM to reduce the number variables.

While doing XP tests, this will also be a great way to test legendary drop rates (a controversial topic which would yeild good info).
Having someone to help with gathering a large sample size (n = 30) would greatly increase data reliability.

Preliminary suggests having the artifact doesn't boost the XP gain to the value it says, so I'll dig in the game files to find actual hard numbers.
For TLDR info, I'll only say what matters in game: it doesn't follow what it says thus far.

More info to come!


# Varkid Info

UPDATE

Am currently working my way through new game files. There's a lot.

Most of the information below is old/outdated, as he's coded differently than I anticipated. So if you want more proper info, check the raid folder.

#

With the new update, I suspect quite a few things have changed, but I haven't had the chance to dive into it yet.

I'm going to look into the evolution in much greater detail and figure out what conditions (if any) could possibly trigger the final evolution in normal varkids (AKA raid evolution).

My current theory is that the raid boss follows the same evolution pathway but can continue due to meeting a criteria found in it's own enemy file which allows it to evolve to the final form in the table `Table_VarkidShared_EvolutionChance`, any player character count, `SuperToRaid`, `BaseValueConstat=*VALUE*`. It may have an override for the `BaseValueConstant` which lets it keep going.

This could be disproved on the basis that when you enter the raid, he spawns in with a different UI name, meaning he has a special `/Conditions/Condition_VarkidHasNavForEvolve` he could draw from which the game uses to separate him from other varkids. But as above, there could be an override in the `BaseValueConstant` which could explain why he could keep going.

I suspect that normal varkids will not trigger a final evolution, but I do not actual data backing that claim up. 


## Old game file info

NOTE: This is before the update.

One interesting thing to note is that after super badass, the game says `SuperToRaid` for the final evolution stage. In BL2, there was a 3 step process: `super badass -> ultimate badass -> Verminvirous/supreme badass`, which is absent in BL3. Digging deeper, it appears that the game decides to go from `superbadass -> supreme badass`, omitting an evolution stage.

Upon a quick look at the wiki, the spawn chance values for ultimate badass -> Verminvirous/Supreme badass match the vaules for the `SuperToRaid` chance. This spawn rate is at 0% for normal mode and only a 7.5% chance in TVHM, which matches up with what's in the game data.

So, what's this mean?

The game is skipping an evolution step, and once a varkid reaches superbadass, it has a chance go straight to "Raid".

## Herme Info

So after playing the new raid boss (which was hella fun), we know that the boss is it's own entity and enemy name.  
I think that it has a special modifier which allows it to follow the evolution path one step further. 

Varkids as a whole have their own table for evolution chance, and I believe that the raid boss uses this table as well. 
After fighting and watching it evolve, one of my theories has been reinforced: the raid use the same pods rather than a unique one.
Evidence to support this is that the initial evolution of raid boss uses the same pod as a normal varkid. 

However, even though they use the same pod (based on visuals), the boss has another special modifier which separates itself from normal varkids by granting it immunity during evolution. (needs testing and data)

- CHECK INTO `Condition_VarkidIsInPod` for health values while in pod. This could explain something!

Furthermore, the line of code `SuperToRaid` in the game file `/Game/Enemies/Varkid/_Shared/_Design/Attributes/Table_VarkidShared_EvolutionChance` matches what the final evolution stage of the raid boss transformos into: a raid boss.


Currently known about herme
- He follows the same evolution path as normal varkids (unconfirmed in data; suspect = `/Game/Enemies/Varkid/_Shared/_Design/Attributes/Table_VarkidShared_EvolutionChance`)
  - is this actual? or does he have his own table?
- Pod looks the same as normal varkid pods, but has invincibility phases.
  - Find why this is, and what file it links itself to which allows this
  - Could this file be linked to a `BaseValueConstant`? Can this be applied to normal varkids? Would it affect the boss and normal varkids overall?
    - IE could he be killed while in his pod inside the raid (this would be bad)
      - Could work around this by redfining the reference: don't use the table. Just replace the enitre section.
      - `SparkPatchEntry,(1,1,0,),/Game/*FILEPATH/ITEM.ITEM*,*ROW*.ROW[1],0,,(AttributeToModify=*SOMETHING*'"/Game/*FILEPATH/ITEM.ITEM*"',ModifierType=*IF_THERE_IS_ONE*,ModifierValue=(BaseValueConstant=*VALUE*,DataTableValue=(DataTable=None,RowName=None,ValueName=None),BaseValueAttribute=None,AttributeInitializer=None,BaseValueScale=1.0))`
- His evolve trigger is damage.
- Can normal varkid data reference the same info that herme has? 


## Verme info

As for Vermivorous the Invincible, I have no idea on that. He's in the raid, but just kinda appears.

Things to investigate and gather data on:
- How he spawns (where does he come from)
- Why he spawns (conditions of spawning)
- Triggers (herme entering final stage is highly supsected, but not actual data. find timing info.)
- Is he referenced in any other files outside of the raid?
- Is he a throwback or something more?
- Can he be added into other spawn areas in the game?

funny idea

- can i turn him into a big baby and have him follow me as a pet

# Other Random Shit to do

- examine loot pool data files
  - new boss (herme and verme)
- what exactly can the diamond room spawn into it? does it have it's own loot pool? does it draw from multiple pools?
- how is card XP calculated? is it based on MH level, guardian rank, or does every enemy just have it's own value?
- How else to earn eridium? There's something out there. Just gotta find it. I don't want to farm my ass off. 
