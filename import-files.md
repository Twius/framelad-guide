---
layout: default
title: Adding your own files
nav_order: 3
permalink: /import-files/
description: "Optional files that add names and spawn data, and how to load them."
---

# Adding your own files

framelad ships no game data. Entities show as `#280`, dispositions as `07`.
If you want names and spawn data, you supply the files.
{: .fs-6 .fw-300 }

All of this is optional. The app predicts frames without any of it.

## What each file adds

| File | What you get |
|:-----|:-------------|
| `names.json` | Names instead of `#280` |
| `dispositions.json` | Words instead of `00` to `24` |
| `set_axve.json`, `set_axpe.json`, `set_bpee.json`, `set_bpre.json`, `set_bpge.json` | Entity and Lv filled in for wild frames |
| `set_a.json`, `set_b.json`, `set_c.json` | Words in the value editor |
| `profile.json` | Makes a modified ROM work at all |

## Loading them

### All at once, in a zip

This is the easy way.

Build this on your computer:

```
framelad files
    Names
        names.json
    Dispositions
        dispositions.json
    Spawn Tables
        set_axve.json
        set_axpe.json
        set_bpee.json
        set_bpre.json
        set_bpge.json
    Save Values
        set_a.json
        set_b.json
        set_c.json
```

Then:

1. Right-click the **framelad files** folder.
2. Choose **Send to**, then **Compressed (zipped) folder**. On a Mac, choose
   **Compress**.
3. Copy the zip to your phone.
4. In framelad: menu, **Data**, **Import all files**, pick the zip.

A summary tells you what went in and what did not.

You do not need all of it. Include only the files you actually have, and leave
out the rest. Most people only ever need one spawn table, the one for the game
they play.

{: .important }
> **The filenames are what matter.** framelad decides what a file is by its
> name, so `names.json` has to be called that. Capitals do not matter, the rest
> of the name does. The folders are only there to keep you organised, and the
> app ignores them.

### One at a time

Menu, **Data**, then tap the row for the file you want. Each row shows what is
currently loaded, and an X to remove it.

## Which spawn file for which game

Spawn tables are per game. Name the file after your ROM code.

| ROM code | Spawn file | Value labels |
|:---------|:-----------|:-------------|
| `AXVE` | `set_axve.json` | `set_a.json` |
| `AXPE` | `set_axpe.json` | `set_a.json` |
| `BPEE` | `set_bpee.json` | `set_b.json` |
| `BPRE` | `set_bpre.json` | `set_c.json` |
| `BPGE` | `set_bpge.json` | `set_c.json` |

## What goes inside each file

Every file is plain JSON. Numbers used as labels go in quotes.

### names.json

```json
{
  "1": "First one",
  "2": "Second one",
  "280": "Another one"
}
```

Ids run 1 to 2047. Names are cut at 24 characters. Leave out any id you do not
have a name for.

### dispositions.json

```json
{
  "0": "First",
  "1": "Second",
  "24": "Last"
}
```

Indices run 0 to 24. There are exactly 25.

### Spawn tables

```json
{
  "maps": {
    "16": {
      "field": [
        { "entity_id": 101, "level_min": 2, "level_max": 3, "rate": 60 },
        { "entity_id": 102, "level_min": 3, "level_max": 4, "rate": 40 }
      ],
      "water": [
        { "entity_id": 120, "level_min": 20, "level_max": 30, "rate": 100 }
      ]
    }
  }
}
```

| Part | Rule |
|:-----|:-----|
| Map number | `(group x 256) + number`. Group 1, map 5 is `261` |
| Source name | `field`, `water`, `fish_1`, `fish_2`, `fish_3` or `rock` |
| `entity_id` | 1 to 2047 |
| `level_min`, `level_max` | 1 to 100 |
| `rate` | Percentages |

{: .warning }
> **The rates in each list must add up to exactly 100.** This is the single most
> common reason a spawn file is refused. They are percentages, not weights.

Up to 12 entries per list, and up to 1024 maps per file.

### Value labels

```json
{
  "flags": { "0": "First flag", "16": "Another flag" },
  "vars": { "0": "First constant", "64": "Another constant" }
}
```

Numbers count from zero, matching what the value editor shows. Labels are cut at
40 characters.

{: .note }
> Value labels go by address set, not by game, and the numbering is different in
> each set. Use the table above to pick the right one.

## ROM profiles

Only needed if **Current Active Set** reads `-` and your ROM is a modified
version of a supported game. This one is genuinely technical, since you have to
know where the addresses moved to.

You do not have to work the hash out yourself. When a ROM is not recognised, the
panel that replaces the Examine readout shows it under **ROM digest, tap to
copy**. That string is what goes in `rom_hash`.

```json
{
  "framelad_profile": 1,
  "rom_hash": "0000000000000000000000000000000000000000",
  "base": "AXVE",
  "label": "My modified ROM",
  "inherit": true,
  "addrs": {
    "rng_seed_addr": "0x03004818",
    "owner_id_base": "0x02024EA4"
  }
}
```

| Key | What it is |
|:----|:-----------|
| `framelad_profile` | Always `1` |
| `rom_hash` | Your ROM's SHA-1, 40 lowercase characters. Copy it from the panel |
| `base` | Which of the five games it is built from |
| `label` | Optional. Any name you like, cut at 63 characters. It shows beside the set in the Data tab |
| `inherit` | `true` starts from the base game's addresses and changes only what you list. Leave it out and it is `false`, which starts from nothing, so every address you do not list is unavailable |
| `addrs` | The addresses that moved |

A profile only takes effect the next time the ROM loads, so accept the reload
prompt afterwards. It cannot add a game framelad does not already know, only
move a known game's addresses.

In a zip, a profile needs a name that starts with `profile` and ends with
`.json`, such as `profile-mine.json`. Several can go in one zip.

<details markdown="block">
<summary>Every address name a profile accepts</summary>

Anything not on this list is refused by name.

`rng_seed_addr`, `owner_id_base`, `roster_base`, `map_id_addr`, `storage_base`,
`spawn_base`, `map_ptr_addr`, `owner_ptr_addr`, `storage_ptr_addr`,
`battle_flags_addr`, `base_stats_addr`, `flags_offset`, `flags_count`,
`vars_offset`, `vars_count`, `roamer_offset`, `roamer_loc_addr`,
`key_items_offset`, `key_items_capacity`, `security_key_offset`,
`hatch_counter_offset`, `map_header_addr`, `avatar_state_addr`,
`nursery_offset`, `nursery_slot_stride`, `nursery_pending_off`,
`form_table_addr`, `isle_value_offset`, `zone_flag_index`, `names_table_addr`,
`record_owned_offset`, `record_seen_offset`, `record_seen1_offset`,
`record_seen2_offset`, `record_bytes`, `sf_roster_offset`,
`sf_roster_count_offset`, `map_grp_off`, `map_num_off`

Values are text, either `"0x02024EA4"` or plain digits. An `entities` block also
accepts `count`, `index_table_addr`, `base_stats_stride`, `storage_banks` and
`storage_slots_per_bank`. If you give `index_table_addr` anything other than `0`,
you have to give `count` with it.

</details>

## Size limits

| File | Limit |
|:-----|:------|
| Spawn table | 10 MB |
| Names | 1 MB |
| Value labels | 200 KB |
| Dispositions | 100 KB |
| Profile | 50 KB |
| A whole zip | 64 MB |

## If a file is refused

Nothing changes and a message says why. The messages are listed in
[Troubleshooting]({{ site.baseurl }}/troubleshooting/).
