# Every Item Procedural

This repository contains a collection of CSV files with values of stats for
every procedural item in [**No Man's Sky**](https://www.nomanssky.com/). This
includes mainly technology upgrades but also the products (artifacts in game).

## Preamble

Each file includes the seed, procedural name, its perfection in percent and the
actual values of the stats.

There might be an ultra-low percentage of values that are not 100% accurate but
there are also cases where the value of a stat cannot be determined exactly due to
how it's displayed (e.g. `UP_RAIL1` has a damage range from `30` to `40` but always
shows `+2%`).

## Usage

This repository also contains Python scripts that can be used to gather the data. They
base on those shared by **ICE** and **DarkWalker** in the **No Man's Sky [Seed Central](https://discord.gg/AEXcap6) Discord**.

To run them, I suggest [**Python 3.7**](https://www.python.org) or newer.

The first script **prepare**s your save by adding the seeds to it. If you need to,
you can easily split this step into multiple parts by appending the current iteration
and how many you need in total.

There also needs to be at least one procedural item in the corresponding inventory.

```
python procedural_prepare.py PATH_TO_SAVE ITEM_ID [ITERATION TOTAL_ITERATIONS]
```

The second script reads the **procedural** data directly from memory. To do so,
you need to hover the cursor over the first item to reveal its stats. Then you can use
[Cheat Engine](https://cheatengine.org/downloads.php) to find the coresponding
addresses of the item/seed itself, the name, the description, and each of the up to
four stats.

The `TOTAL_ITERATIONS` here must match those from the preparation script (defaults to
`1` if not set). You can directly enter the addresses as they are displayed in
Cheat Engine and don't need to prepend a `0x`.

```
python procedural.py TOTAL_ITERATIONS ADDRESS_ITEM_SEED ADDRESS_DESCRIPTION ADDRESS_TITLE ADDRESS_STAT1 [ADDRESS_STAT2 [ADDRESS_STAT3 [ADDRESS_STAT4]]]
```

The third script **recompute**s the perfection of all entries in a file. This can
be necessary if you want to changed the digits or he values range is different than you
thought when you run the second script to gather the data.

Just uncomment the items you want to recompute and run the script.

```
python procedural_recompute.py
```
