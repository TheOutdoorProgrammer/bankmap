---
dusk: v1alpha1
namespace: stout
kind: repository
name: bankmap
title: Bank Failure Maps
attributes:
  visibility: public
  language: jupyter
---

A finished piece of analysis from March 2023 rather than a maintained project.
Silicon Valley Bank had just failed, the question was which US states have had the most bank failures and whether they cluster, and this repository answers it and stops.
Nothing here is meant to keep running.

`banklist.ipynb` is the whole of it, eight cells of geopandas, pandas and matplotlib.
It reads two inputs: the FDIC Failed Bank List as `banklist.csv`, which is 564 failures from October 2000 through Silicon Valley Bank on 10 March 2023, carrying bank name, city, state, FDIC certificate number, acquiring institution, closing date and fund; and the National Weather Service US states shapefile in `us_shape/`.
Failures are counted per state, reindexed against a hard-coded list of all fifty so that states with none read as zero rather than going missing (only 44 states appear in the data at all), joined to the shapefile geometry, and rendered as `Reds` choropleths.
It also prints the states with the most, the fewest, and close to the average number of failures.
Georgia leads with 93, then Florida with 76 and Illinois with 69.

The rendered maps are committed next to the notebook and embedded in the README: `lower48.png`, `max.png`, `min.png`, `average.png` and `unitedstates.png`.
Re-running the notebook reproduces exactly those figures, because the CSV is a snapshot.
A later answer means downloading a fresh Failed Bank List from the FDIC, at which point the fixed pieces below start to matter.

## Gotchas

**The README links to `all50.png`, which is not in the repository.** The all-fifty-states render is almost certainly `unitedstates.png`, which is committed and referenced by nothing.

**The colour scale is pinned to 0 through 100 rather than derived from the data.** Georgia sits at 93, so any newer data would run off the top of the ramp while the legend carried on claiming 100.
