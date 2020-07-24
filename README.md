# StoryScript (WIP)

A simple language for writing choose-your-own-adventure type games.

## Motivation

When building a text adventure from scratch, we needed a way to structure branching paths as a result of the player's choices.

The target game engine is [Godot](https://godotengine.org), and we wanted to write our script separate from the game files. The solution, was to write in a simple language designed for making choices, and use a parser to convert the script files into game assets.

## Progress
A simple Python parser is almost complete. The target parser script (in GDScript) is still in the works. 

Syntax highlighting is available for Sublime Text 3.

## Sample

```
<Introduction>
You venture down into the crypts. A chill goes down your spine. 
You turn around to find a skeleton!
!Combat 1!

|Combat 1|
> Hit the skeleton
  [Strength > 5] !Enrage Skeleton! !Player hurt!
> Flee
  !Player flees!

<Enrage Skeleton>
You throw your best punch at the skeleton and knock its head off. The skeleton scrambles to retrieve its head, before returning to face you head on; angrier than ever.
!Combat 2!!

<Player hurt>
You try to hit the skeleton, but it is too fast! 

The Skeleton takes a swipe at your face. You stumble backwards.
!Combat 2!!

<Player flees>
You successfully escape the skeleton.
!END!

...

```

## Syntax
A StoryScript file contains different Sections, where each Section points to the next.

The `!section!` operator is used to go to the next section. For instance, `!SectionA!` means go to SectionA.

There are three types of sections: Text, Choice, and Image.

### Text

`<>` denotes a text section, and is structured like so:

```
<SectionName>
Text, and more text
!SectionA!
```

`SectionName` - Name of the current section
`SectionA` - Name of the next section

### Choice 

`||` denotes a choice section.
Within a choice, each option is listed as follows, where `[]` denotes a check. 

```
|ChoiceName|
> [CheckA] ChoiceText 
    [CheckB] SectionA SectionB
```

`ChoiceName` - Name of the current choice section

`CheckA` - an optional check to see if the player meets the requirements for displaying this choice. 

`CheckB` - a check to see if the player succeeded in the action of the choice.

`SectionA` - If CheckB succeeded, then go to SectionA

`SectionB` - If CheckB failed, then go to SectionB

For a choice that will always succeed, the following syntax should be used:

```
|ChoiceName|
> [CheckA] ChoiceText 
    SectionA
```

If ChoiceText is selected, then go to SectionA


### Images

`**` denotes an image section.

```
*ImageName*
Image.png
!SectionA!
```

