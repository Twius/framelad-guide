---
layout: default
title: Troubleshooting
nav_order: 4
permalink: /troubleshooting/
description: "Common problems and what they mean."
---

# Troubleshooting

Common problems, and what the app is telling you.
{: .fs-6 .fw-300 }

## Predictions do not work on my ROM

When framelad cannot read a ROM, **Current Active Set** reads `-` and a panel
takes the place of the Examine readout on the main screen. The panel, not the
`-`, tells you which of two problems you have, and it carries the ROM digest you
will need if you go on to write a profile.

### The panel says the addresses were not recognised

framelad knows this game, but the copy you are running has moved them. This is
normal for a modified ROM, and a
[ROM profile]({{ site.baseurl }}/import-files/#rom-profiles) is what fixes it.

### The panel says the game is not supported

The ROM's code is not one of the five framelad knows. A profile can still help,
but only if this really is a modified version of one of those five, because every
profile has to name one of them as its `base`. No file can teach framelad a game
it does not already know.

### I added a profile and nothing happened

Profiles only apply when the ROM loads. Accept the reload prompt, or go back and
open the ROM again. If it came from a zip, dismiss the summary first and the
prompt appears behind it.

### It says the profile is for a different ROM

The hash does not match. It was still saved, which is normal if you are setting
up profiles ahead of time. Otherwise check the hash, and make sure it is
lowercase.

## A file would not import

Nothing changes when a file is refused, so you can just fix it and try again.

### Spawn tables

| Message | What to fix |
|:--------|:------------|
| `slot rates must total 100` | The rates in one list do not add up to 100 |
| `invalid spawn table file` | Broken JSON. Look for a stray comma |
| `map id out of range` | A map number above 65535 |
| `duplicate map id` | The same map listed twice |
| `empty source list` | A source with nothing in it. Delete the line |
| `too many slots` | More than 12 entries in one list |
| `too many maps` | More than 1024 maps |
| `entity id out of range` | An id outside 1 to 2047 |
| `level out of range` | A level outside 1 to 100 |
| `level min above max` | The levels are the wrong way round |
| `rate must be at least 1` | A rate of zero or missing |
| `file too large` | Over 10 MB |
| `unsupported title` | Fix the ROM first, see above |

### Profiles

| Message | What to fix |
|:--------|:------------|
| `not a framelad profile file` | Add `"framelad_profile": 1` at the top |
| `invalid rom_hash in profile` | Needs 40 lowercase characters |
| `unknown base ROM code in profile` | `base` must be one of the five codes |
| `unknown address key in profile: <key>` | A misspelled address name, named at the end of the message |
| `invalid value for <key> in profile` | A number out of range, or with extra text in it |
| `this profile is from a newer version of framelad` | Update the app |
| `index_table_addr requires entities.count in profile` | Add `count` to the `entities` block, or drop `index_table_addr` |

### Names, dispositions and value labels

These ignore bad entries and keep the good ones, so a refusal means the whole
file failed. Usually that is broken JSON, or every number being out of range.

| File | Numbers must be |
|:-----|:----------------|
| `names.json` | 1 to 2047 |
| `dispositions.json` | 0 to 24 |
| Value labels | Inside a `flags` or `vars` block |

### Something in my zip did not load

The summary splits this two ways.

**Skipped** means framelad did not recognise the filename. Check the spelling
against [the list]({{ site.baseurl }}/import-files/#what-each-file-adds).
Folders inside the zip do not matter, but names do.

**Rejected** means it recognised the file and the contents failed. The reason is
printed next to it, and it is one of the messages above. Rejected files are
named by type rather than filename, so a spawn table shows as
`spawn table (Set C)`.

One reason only turns up here: `too much data to import at once` means the file
was inside its own limit, but the zip as a whole went over 64 MB. Split it.

If it says `No recognized files found`, none of the names matched. If it says
the zip could not be read, the archive itself is damaged.

## Something is blank

| What | Why |
|:-----|:----|
| Entities show as `#280` | No names file, or that id is not in it |
| Disp shows `00` to `24` | No dispositions file |
| Entity and Lv are blank | No spawn table for this spot, or none for this game |
| Lv shows `-` | A static spawn, or no spawn list here |
| The isle filter does nothing | That set has no isle mechanic |
| Storage or Daycare is empty under a profile | Your profile does not include that address. Check the chips under Current Active Set |

The ✦ on a row is always right, even when Entity and Lv are blank. So are the
stats, as long as the method under View, Prediction matches your game.

### The frame list disappeared

1. **RNG tools** is off, under View, Display.
2. It was removed in the layout editor, under System, Controls.
3. You are in landscape, or a link session is running. It does not show in
   either.

## Things that look wrong but are not

**Sound goes quiet when I speed up.** By design. Sound only plays near normal
speed, and it stays silent for the whole of a link session.

**Egg rows show `-` for stats.** Egg stats cannot be predicted. The rest of the
row, including ✦, is exact.

**A pending egg shows `?`.** On two of the three sets, disposition and rareness
are genuinely not decided until you accept the egg.

**Two rows in a row look identical.** They share a hidden value and differ only
in which entity comes out. That is real, not a display bug.

**Loading an old save state undid my progress.** It cannot. Save states never
touch your in game save.

## Still stuck

Open View, Display, **Owner info**. If the seeds are missing or the current seed
never changes, the problem is the ROM not being recognised, not your files. Go
back to the top of this page.
