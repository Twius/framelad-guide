---
layout: default
title: Setup
nav_order: 1
permalink: /
description: "Get framelad running in four steps."
---

# Setup

Four steps to get running.
{: .fs-6 .fw-300 }

## 1. Install

Get framelad from the Play Store.

## 2. Point it at your ROMs

Open the app. The library is empty at first.

1. Tap the folder picker.
2. Choose the folder holding your ROM backups.
3. Allow access when Android asks.

You only do this once.

{: .note }
> You supply your own ROM backups. framelad includes none, and links to none.

## 3. Load a ROM

Tap it in the list. The game starts, with the frame list below it.

{: .note }
> Tap the game picture to pause, and tap it again to carry on. While paused it
> dims and says **PAUSED**. The pause button on the top bar does the same.
> Locking your phone or switching apps also pauses, and it stays paused until you
> resume.

## 4. Check it works

Open the menu, go to **Data**. The top row says **Current Active Set**.

| It says | Meaning |
|:--------|:--------|
| `Set A`, `Set B` or `Set C` | Working. You are done. |
| `Set A · profile "my build"` | Working, through a profile you added. The quoted part is your profile's `label`, and is left off entirely if it has none. |
| `Checking…` | Wait a second. |
| `-` | Predictions are off for this ROM. See [Troubleshooting]({{ site.baseurl }}/troubleshooting/). |

## Hunting a frame

The whole loop is four steps.

1. **Pick a source** from the chips above the list. `Auto` is usually right. Use
   `Static` for a fixed spawn.
2. **Filter** by tapping a column header, so only the rows you want remain.
3. **Tap the row** you want. It pins, and a countdown starts.
4. **Act a few frames before it says `now!`**, usually 3 to 7. Take the step,
   cast the line, break the rock.

You get the row you pinned. Going early covers the delay between your input and
the game reading it, so if you keep landing on the wrong row, adjust how early
you go.

{: .tip }
> Use the `>>` chip to fast forward toward a distant frame, then `>` for normal
> speed on the last stretch.

## What the colours mean

In the frame list:

| Look | Meaning |
|:-----|:--------|
| Gold ✦ | Rare |
| Blue 🏝️ | Isle eligible |
| `-` under Lv | No spawn list for this spot, or a static spawn |

A row gets one colour, and isle outranks rare. So a rare entity that is also isle
eligible reads blue, not gold. The ✦ stays either way.

Two more colours, and one more marker, appear in the Examine readout, which
reads a real entity rather than a prediction.

| Look | Meaning |
|:-----|:--------|
| Green 🦠 | Carrying the virus |
| Purple | Isle eligible and carrying the virus |
| Dimmed 🦠 | Cured, or immune |

The virus is only given to an entity you already own, so it never appears on a
prediction row.

The ✦ on a row is always right, even when Entity and Lv are blank. So are the
stats, as long as the method under View, Prediction matches your game. Egg rows
never show stats at all, because egg stats cannot be predicted.

## Optional extras

Nothing below is required.

| Want | Where |
|:-----|:------|
| Names instead of `#280` | [Add your own files]({{ site.baseurl }}/import-files/) |
| Save states with thumbnails | Play, States |
| Autosave every 30 to 300 seconds | Play, Autosave |
| A different colour scheme | System, Theme |
| Move the buttons around | System, Controls |
| Trade over your wifi | System, Link |

Every option is listed in the [menu reference]({{ site.baseurl }}/menu/).
