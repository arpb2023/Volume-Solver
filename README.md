# Volume-Solver

**Compare two LandXML surfaces and read the earthworks volume — then hand it over as DXF or LandXML.**

Volume Solver is a free, single-file tool that runs entirely in your browser. Drop in two
surfaces, set which is which, and get cut, fill and net volumes with a coloured difference
map, cross sections, and per-region quantities. No install, no account, no build step, and
nothing is ever uploaded — the whole thing runs on your machine, offline.

### ▶ Run it now

[Launch Volume Solver](https://howtocivilengineer.github.io/Volume-Solver/) (click open link in new tab)

Open the link, drop two LandXML surfaces on the page, and go. Works on desktop and mobile,
(desktop is recommended).

---

## Video walkthrough

*A full video walkthrough is coming soon.*

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
- **Regions** — draw a boundary on the map or import outlines from a DXF, and get cut, fill
and net inside each one.
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
outlines in from a DXF. Each region carries its own cut, fill, net and area.

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

### Keeping the DXF a sensible size

On noisy work — two surveys of the same ground, where the difference is close to survey
noise — a band map can dissolve into thousands of single-cell specks, and the file balloons.
**Smallest feature kept** absorbs islands below the size you set into the band around them.
It is the difference between a readable plan and stipple, and it typically takes the file
down by an order of magnitude. When most of the map turns out to be specks, the tool says so
— that is a sign the difference is near the noise floor and the colours should be read as a
trend rather than a boundary.

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
region boundaries, and exported files before using them for design, construction,
measurement, payment, or other engineering decisions.

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

*Built for surveyors and civil engineers who want a fast, free way to measure, review and share earthworks volumes—without requiring Civil 3D or other desktop software.*
