# Structure

| Folder | What it holds |
| --- | --- |
| `constitution/` | The Constitution of the Commonwealth of The Bahamas (`art-001.md` onward, `preamble.md`) |
| `acts/<year>/<NNN>-<slug>/` | A principal Act, by the year and number of its legislation number on Bahamas Laws On-line, e.g. `acts/1873/015-penal-code/` (1873-0015), `acts/2001/027-employment/` (2001-0027) |
| `subsidiary/<year>/<NNN>-<slug>/` | Subsidiary legislation (regulations, rules, orders), by its legislation number, e.g. `subsidiary/2015/011-early-childhood-care-national-standards-regulations/`; its README names the Act it is made under |

Each folder holds one file per section (`s-290.md` is section 290, `s-088-a.md` section 88A), article (`art-001.md`)
or schedule (`schedule-1.md`), and a `README.md` with the edition, the laws it lists and the provision headings. No
folder holds more than 1,000 entries.

## Dates

Each version is one consolidation the publisher serves (its current edition and the earlier editions it still
serves), committed at 12:00 America/Nassau on the day it took effect, which the `In-force:` trailer repeats.
`In-force-basis:` says where that day comes from:

- `commencement`: the law lists no amending law; the day is its own "Date Commenced" in the publisher's index;
- `last-listed-amendment-commencement`: the latest commencement among the amending laws the edition's own list of
  laws names, each taken from the publisher's Acts by Year pages or its index. The commit is credited to that law;
- `law-revision-edition`: used when the edition names no law that commenced after the edition before it, or names a
  law whose commencement the site does not give: the first day the publisher's point-in-time act index serves that
  revised edition (e.g. LRO 1/2017 from 31 December 2016), found by bisecting the index's date. Credited to the
  publisher.

An edition that none of these dates, or that would be dated no later than the edition before it, is held back and
listed in `data/held.csv`; so is a PDF without a text layer (no OCR is done). Days before 1970 are
stamped 1 January 1970 (git cannot store them), with the real day in the subject and `In-force:`. No date in this
repository is the day anything was downloaded.
