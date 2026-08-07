# Volume Solver

**Compare two LandXML surfaces and read the earthworks volume — then hand it over as DXF or LandXML.**

Volume Solver is a free, single-file tool that runs entirely in your browser. Drop in two
surfaces, set which is which, and get cut, fill and net volumes with a coloured difference
map, cross sections, and per-region quantities. No install, no account, no build step, and
nothing is ever uploaded — the whole thing runs on your machine, offline.

### ▶ Run it now

[Launch Volume Solver](https://howtocivilengineer.github.io/Volume-Solver/) (click open link in new tab)

Open the link, drop two LandXML surfaces on the page, and go. No files to hand? Press
**Load sample**: a built-in 260 × 180 m site with two platforms sharing a 2.6 m vertical face,
a detention basin, ground with a ridge and a gully so there's real cut and real fill, and
pavement boxes already set on the slab and car park with a section cut through the lot. Same
numbers every time, so it's a safe place to learn the tool — change a depth and watch the
volume and the section move together.

Works on desktop and mobile (desktop is recommended).

---

## Video walkthrough

A dedicated walkthrough is on the way. In the meantime, the **How To Civil Engineer** channel
covers the thinking behind these tools and how they're used on real work:

[youtube.com/@howtocivilengineer](https://www.youtube.com/@howtocivilengineer)

---

## What it does

Volume Solver takes two surfaces — existing ground and design, stripped and subgrade, or the
same site surveyed twice — and gives you a volume you can interrogate rather than a single
number from a black box. It sits alongside your main design software as a fast cross-check
and a zero-cost way to measure, review and share earthworks quantities.

- **Reads LandXML TIN surfaces** exported from Civil 3D or any package that writes them,
with a switch for files written easting-first instead of the LandXML standard.
- **Grid-based volume** between the two surfaces, computed on a fine grid you choose, with a
second coarser grid running alongside as a convergence check so you can see whether the
number has settled.
- **Level changes on either surface** — raise or lower a surface and everything recomputes,
which is how you test a strip depth or a formation shift without going back to CAD.
- **Coloured difference map** with editable bands. Band edges are chained, so one band's top
is the next band's bottom and there are no gaps; the outer two ends are fixed by the
measurement itself and cannot be typed over.
- **Cross sections** — cut a line anywhere on the map and read four levels against each
other: each surface as it arrived, and each surface with your level change applied.
- **Regions with their own depth** — draw a boundary on the map or import outlines from a
DXF, get cut, fill and net inside each one, and push the comparison surface straight down
inside it: a slab box at 450, a pavement box at 300, a landscaping strip at 150, all in one
model.
- **Label orientation** — draw a line in any direction and the exported difference labels,
region names and legend all read along it, so the DXF drops into a rotated viewport without
a field of sideways text.
- **Metric and imperial** — the toggle declares what your files are already in and relabels
throughout, including cubic yards. It never rescales your coordinates.
- **Multilingual** — English, Português, Français and Español.

---

## The workflow

The panel is laid out in the order you actually work:

**1 · Surfaces** — drop in two LandXML files, set which is the base and which is the
comparison, and apply a level change to either. Volume is measured from the base surface up
to the comparison surface: positive is fill, negative is cut.

**2 · Grids** — a computation grid that sets the volume, and a display grid that sets the
colour map. The volume always comes from the fine grid, so the map can be coarsened for
readability without blunting the number.

**3 · Volume** — cut, fill, net and common area, with both grids reported side by side and
the percentage between them, so a number that hasn't converged is obvious.

**4 · Colour bands** — edit the band edges, colours and count. Band volumes are measured on
the same fine grid, so they add up to the net above. *Fit to data* re-spaces every band
across the measured range.

**5 · Regions** — draw a closed boundary by clicking corners on the difference map, or bring
outlines in from a DXF. Each region carries its own cut, fill, net and area, and its own
**depth below surface**.

A depth is a vertical push down into the comparison surface inside the boundary — the
pavement or slab box you'd otherwise model upstream. It applies on top of any level change
you've set for the whole surface, so a 0.3 m surface drop plus a 0.45 m slab depth puts those
cells 0.75 m below where the surface arrived. Depths are down-only, because a region depth
that could go either way would quietly mean something else.

Where two regions overlap, the one lower in the list wins, and the region being covered says
so on its card rather than leaving you to guess.

**6 · Export** — choose the fill style, cell size, smallest feature kept and label spacing,
then write out a DXF or a LandXML difference surface.

**Section** — in the top bar. Click two points on the difference map and a section strip
opens along the bottom, with four switchable lines: each surface continuous as it arrived,
and each surface dashed with its level change applied. Greens are the base surface, browns
and yellows the comparison.

---

## Exports in detail

| Output | What it contains |
| --- | --- |
| **DXF** | The coloured difference map, the band table as a legend, difference labels on their own grid, and any regions. Each band sits on its own layer with its colour on the layer, so you can freeze or isolate a band in CAD. |
| **LandXML surface** | The difference between the two surfaces as a TIN in its own right, at a spacing you choose, ready to import as a surface and contour or label like any other. |

Both exports state every level change that was applied — surface offsets and region depths —
in the DXF legend and in the LandXML surface description. Those numbers live only in your
browser session, so without them nobody could reproduce the volume from the two source files.
If the output is going anywhere near measurement or payment, that record matters.

### Keeping the DXF a sensible size

On noisy work — two surveys of the same ground, where the difference is close to survey
noise — a band map can dissolve into thousands of single-cell specks, and the file balloons.
**Smallest feature kept** absorbs islands below the size you set into the band around them.
It is the difference between a readable plan and stipple, and it typically takes the file
down by an order of magnitude. When most of the map turns out to be specks, the tool says so
— that is a sign the difference is near the noise floor and the colours should be read as a
trend rather than a boundary.

---

## Coming from Civil 3D

Volume Solver isn't trying to replace Civil 3D. It reads the same LandXML surfaces Civil 3D
writes, so it sits alongside it as a fast, free way to cross-check a volume, review someone
else's design, or share a quantity with someone who doesn't have a seat. Three things it does
differently are worth knowing about.

### 1. Regions can be dropped, without modelling anything

Giving different areas different depths in Civil 3D means building the geometry: a surface per
area, or a corridor, or feature lines with vertical faces at every boundary. It works, but
it's a lot of modelling for what is conceptually one number per area — and a near-vertical
face in a TIN is the one thing a TIN handles least gracefully.

Here a region depth is a mask over the computation grid, not geometry. Draw a boundary, type a
depth, and the comparison surface is pushed straight down inside it. A slab box at 450, a
pavement box at 300, a landscaping strip at 150 — three numbers, one model, and re-running the
whole set at a different depth takes seconds rather than a rebuild. Where two regions overlap,
the lower one in the list wins and the covered region says so rather than leaving you to guess.

It is deliberately limited to a constant depth per region. The moment you want falls within an
area, batters between areas, or a real transition at a boundary, that's a design, and it
belongs upstream in your grading software.

### 2. Exported labels can be set to any orientation

In Civil 3D you set elevations on a grid and the labels rotate to suit the viewport twist,
because the labels are live objects that know which way the view is facing. A DXF has no such
intelligence — text sits at whatever angle it was written at, and a plan rotated to suit a
site's skew ends up with a field of sideways numbers.

The **Angle** tool solves it the way you'd think about it on paper: draw a line in the
direction you want the labels to read, and every difference label is written at that angle.
The angle is normalised to plan-readable, so drawing the line either way round gives text the
right way up rather than upside down. The legend stays square to the sheet, because a table
isn't read off the ground. The readout shows the bearing clockwise from north, and one button
puts it back.

Each label is anchored on its decimal point, and the drawing says so beneath the legend — so
anyone setting out from the plan knows exactly what the text is pinned to.

### 3. Sections show the surfaces before and after your changes, together

A Civil 3D section view shows the surfaces that exist. To see what a strip depth or a
formation shift would look like in section, you first have to build the surface that
represents it.

Cut a section here and you get four lines at once: each surface as it arrived, drawn
continuous, and each surface with its level change applied, drawn dashed — including any
region depth, which reads as a genuine step rather than a smoothed batter. The two adjusted
lines are hatched against each other, because those are what the volume is actually measured
between. Toggle any of the four off. Change an offset or a region depth and the section
redraws with it, so you can test an idea in section before committing it to a surface.

### Other differences worth knowing

- **It runs in a browser, offline, for free.** Anyone you send the file to can open the tool
and check your working, seat or no seat.
- **The volume tells you whether it has converged.** Two grids are computed side by side and
both are reported, with the percentage between them. A number that hasn't settled is visible
rather than implied.
- **Noise gets filtered on the way out.** On survey-versus-survey work a band map can dissolve
into thousands of single-cell specks. **Smallest feature kept** absorbs them, and if most of
the map turns out to be specks the tool says so — that's a sign the difference is near the
noise floor.
- **The band range can't be faked.** The outer ends of the colour bands are fixed by the
measurement itself and can't be typed over, and band edges are chained so there are no gaps
between them.
- **The export carries its own working.** Every level change and region depth is written into
the DXF legend and the LandXML description, so the number can be reproduced from the files.

---

## Privacy

Everything happens locally in your browser. No file you open is sent anywhere, and there is
no server, tracking or account. You can save the page and run it with no internet connection
at all.

---

## Run it locally / self-host

The whole tool is one HTML file with no dependencies and no build step.

- **Run offline:** download `index.html` and open it in any modern browser.
- **Self-host:** it's already served from this repository via GitHub Pages. Any static host
works — just drop the file in and open it.

---

## Tech

Plain HTML, CSS and vanilla JavaScript in a single file. No frameworks, no bundler, no
package install. The LandXML parser, the rasteriser and volume integration, the band tracing
and the DXF / LandXML writers are all hand-rolled and run client-side.

---

## Feedback

Found a bug, have a surface that doesn't import cleanly, or have an idea to make Volume
Solver better? Open an issue.

If you're reporting a bug, including a sample of the LandXML that caused the problem is the
fastest way to help reproduce and fix it. Feature requests, usability suggestions, and
general feedback are always welcome.

---

## Disclaimer

Volume Solver is provided as a free tool to assist with surface comparison, earthworks
quantity checking, and design review. It is not a replacement for professional surveying,
engineering judgement, or certified design software.

The user is responsible for verifying imported surfaces, grid resolution, level changes,
region boundaries, region depths, and exported files before using them for design,
construction, measurement, payment, or other engineering decisions.

While every effort has been made to produce accurate results, no guarantee is provided that
the software is free from errors or suitable for any specific project. Always check outputs
against original survey data, independent calculations, and appropriate professional
standards.

Use of Volume Solver is at your own risk. The developer accepts no responsibility for
losses, damages, or consequences arising from the use of this software.

---

## License

*License to be confirmed.*

---

*Built for civil engineers and other designers who want a fast, free way to measure, review and share earthworks volumes — without needing Civil 3D or any other desktop software.*
