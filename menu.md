---
layout: default
title: Menu reference
nav_order: 2
permalink: /menu/
description: "What every menu option does."
---

# Menu reference

What every option does. Four tabs, swipe or tap to switch.
{: .fs-6 .fw-300 }

Opening the menu pauses the game, so a frame you are counting down to cannot
slip past.

## Play

### States

Two save slots. Each shows a picture of the moment it was saved.

| Option | Does |
|:-------|:-----|
| Save to State 1 or 2 | Saves over that slot |
| Load from State 1 or 2 | Goes back to it |

{: .note }
> Save states never touch your in game save, so loading an old one cannot undo
> your progress.

### Autosave

| Option | Does |
|:-------|:-----|
| Enable autosave | Saves in the background, off by default |
| 30s, 60s, 120s, 300s | How often |
| Load Autosave | Goes back to the last one |

Uses its own slot, so it never overwrites States 1 or 2.

### Speed and Sound

| Option | Does |
|:-------|:-----|
| FPS cap | Speed limit, 1 to 600. Normal is 59.7 |
| Mute | Turns sound off |

Sound only plays near normal speed, and mutes itself when you speed up or slow
down. It is also silent for the whole of a link session.

## View

### Display

| Option | Does |
|:-------|:-----|
| RNG tools | Master switch for predictions. Off hides the frame list and stops the work behind it |
| Owner info | Shows your IDs and the seeds |

### Prediction

| Option | Does |
|:-------|:-----|
| Method M1, M2, M4 | Which stat roll pattern to predict. Leave on M1 unless your catches do not match |
| Frames | How far ahead to predict. 100k by default. Bigger reaches further but uses more memory |

### Graphics and Control

| Option | Does |
|:-------|:-----|
| Enhancement | Sharper, smoother pixels. Off by default |
| Joystick D-pad | Swaps the arrow buttons for a thumbstick |

## Data

### Current Active Set

Tells you whether predictions work on this ROM.

| Reading | Meaning |
|:--------|:--------|
| `Set A`, `Set B`, `Set C` | Working |
| `Checking…` | Wait a second |
| A set, then `· profile` | Working, through a profile you added. Your `label` follows in quotes, if you gave one |
| `-` | Not recognised. A panel on the main screen says why, and whether a profile can help |

Under a profile, chips underneath show which readings you have and which are
missing.

### Files

| Option | Does |
|:-------|:-----|
| Import all files | Loads a whole zip at once |
| Import names | Names instead of `#280` |
| Import dispositions | Words instead of `00` to `24` |
| Import spawn table | Fills in Entity and Lv |
| Import ROM profile | Makes a modified ROM work |

Rows show what is loaded, with an X to remove it. See
[Adding your own files]({{ site.baseurl }}/import-files/).

### Save values

| Option | Does |
|:-------|:-----|
| Edit values | Edit the game's flags and counters directly |
| Import value labels | Words instead of numbers in that editor |

Changes are live and stick when you next save in game.

### Additional content

| Option | Does |
|:-------|:-----|
| Add bonus items | Adds a batch of otherwise unobtainable key items |
| Set bonus roamer | Brings the roamer back after it is caught or defeated, identical to before |
| Transform Link Entities | Applies trade based form changes to your roster, keeping everything else the same |

### Save File

| Option | Does |
|:-------|:-----|
| Extract save | Copies your save out |
| Load save | Loads a save in and restarts |
| Save file sharing | Move entities between this save and another one |
| Restore save backup | Go back to an automatic backup |

Sharing backs up both saves first, checks both still work before writing
anything, and warns you about anything this game will not recognise.

## System

| Option | Does |
|:-------|:-----|
| Theme | System, or one of nine colour schemes |
| Navbar | Which chips are on the top bar, and what the two speed chips run at |
| Customize portrait or landscape | Drag the buttons and panels where you want them |
| Change Time | Set a specific date and time |
| Dead Battery | Reports a flat internal battery, stopping the in game clock. On Set A that also pins the seed the game starts from. The other sets do not use the clock for their seed |
| Link play | Trade over your wifi, up to 4 players |
| Export or Import settings | Back up every setting to one file |
| Reset | Restarts the game |
| Guide | Opens this guide in your browser |
| Terms of use | Opens in your browser |
| Privacy policy | Opens in your browser |
| Open source licences | Licences for the open source code framelad uses |
| Rate the app | Opens the Play Store page |

{: .note }
> Link play is your local wifi only. No internet, no servers, no accounts.
> While linked, autosave and predictions pause and some buttons grey out.

{: .tip }
> There is something hidden on the version line. Keep tapping it.

## Why is something greyed out?

| Cause | What it stops |
|:------|:--------------|
| The ROM is not recognised | Spawn tables, value labels, the value editor, bonus content, save sharing |
| A link session is running | The same list, plus pause, speed, quick load and the menu |
| The slot is empty | Load State, Load Autosave |
| Dead Battery is on | Change Time |

Import ROM profile is never greyed out, because that is the one an unrecognised
ROM needs.
