# The Bahamas: law history in git

The law of The Bahamas as a git history: one file per section or article, one commit per law on the day it took effect, and the law that made each change as the commit's author. `git blame` names the law behind every paragraph; `git log` lists every change to a section; `tools/on.py` gives the text in force on any day.

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law), which places it at `bs/`. The text is the Government of The Bahamas' own consolidation, the *Statute Law of The Bahamas* revised editions served as PDFs by [Bahamas Laws On-line](https://laws.bahamas.gov.bs), read from each PDF's text layer.

**What is in it**

| Folder | Act | Versions | History | Latest version |
| --- | --- | ---: | --- | --- |
| `constitution/` | The Constitution of the Commonwealth of The Bahamas | 1 | 1973-07-10 | the current consolidation (LRO 1/2006) |
| `penal-code/` | Penal Code (Ch. 84) | 7 | 2009-10-01 to 2016-12-31 | the current consolidation (LRO 1/2017) |
| `data-protection/` | Data Protection (Privacy of Personal Information) Act (Ch. 324A) | 1 | 2007-04-02 | the current consolidation (LRO 1/2008) |

- **Penal Code.** Two dated consolidations: the 2010 revised edition (LRO 1/2010), which the publisher's point-in-time index lists as current up to 30 December 2016, and the 2017 revised edition (LRO 1/2017), current from 31 December 2016 to today. Between them, each section whose marginal note in the 2017 edition names a newer law (for example "34 of 2011, s. 2.") takes its new wording on that law's commencement date: the Forestry Act 2010 (4 January 2011), the Probate and Administration of Estates Act 2011 (1 June 2011), the Animal Protection and Control Act 2010 (4 October 2011, repealing ss 161-184 and 223-231), the Penal Code (Amendment) Act 2011 (4 November 2011, murder and its sentences) and the Penal Code (Amendment) Act 2014 (12 November 2015, gangs and bulletproof vests). Act 28 of 2008 (ss 88A, 126, 127) has no commencement date anywhere on the site, so its changes are dated 31 December 2016, the day the first consolidation showing them became current, and its commit says so. Nine further sections differ between the editions with no note: years dropped from Act titles (s 10), an Act's name and a cross-reference corrected (ss 33, 65), commas (ss 154, 256), a heading's spelling (s 362), two stray letters in the typesetting (ss 360, 470), and the words "or any cultivated plant" gone from s 157. They are the publisher's, committed as "unexplained" on 31 December 2016.
- **Constitution.** One version: the 1973 text as printed in LRO 1/2006, whose footnote says it "to date has not been amended", credited to The Bahamas Independence Order 1973 (S.I. 1973 No. 1080) on 10 July 1973.
- **Data Protection Act.** One version: Act 3 of 2003 as printed in LRO 1/2008, from its commencement on 2 April 2007. The index lists no amending act and no section carries an amendment note.

Each folder's `README.md` lists every provision, how often it changed and when.

## A lawyer's questions as git commands

| Question | Command |
| --- | --- |
| What did s 290 say on 2011-01-01? | `python tools/on.py 2011-01-01 penal-code s-290` |
| The same, with raw git (bash) | `git show $(git rev-list -1 --before="2011-01-01T23:59:59Z" main -- penal-code/s-290.md):penal-code/s-290.md` |
| The same, in PowerShell | `$r = git rev-list -1 --before="2011-01-01T23:59:59Z" main -- penal-code/s-290.md; git show "$($r):penal-code/s-290.md"` |
| Which law wrote each line? | `git blame penal-code/s-290.md` |
| Every change, word by word | `git log -p --word-diff penal-code/s-004.md` |
| Every law in the record, in order | `git log --reverse --format="%ad %an" --date=short main` |
| Everything one law changed | `git show law/<key>` (tags `law/<key>` mark each law's commit, e.g. `law/act-2011-034`) |
| The whole act on a date | `python tools/on.py 2012-01-01 penal-code` |

After a rebuild, refresh tags with `git fetch --force --tags`: a plain fetch keeps stale tags.

## Dates

- Each commit is dated at **noon, America/Nassau, on the day the change took effect**. The day is also in the `In-force:` trailer, which the tools read.
- Every date is a **"Date Commenced" from the publisher's own index**: the act index's "amended by" rows, or its Acts by Year list. No date is derived from publication.
- **The oldest Penal Code version** is the 2010 edition, dated 1 October 2009: the commencement of the last law in its list of laws (Act 1 of 2007, the Child Protection Act).
- `--before="YYYY-MM-DD"` alone uses your clock's time of day, so a law that took effect that day may be missed before noon. Use `T23:59:59Z` as above, or the tool.

## How it is checked

- Every version is read back from git on the day it took effect and on the day before (`tools/check_repo.py`); both must match `corpus.json`. Results are in `REPRODUCE.md`.
- **Today's text:** for each act, the last version is exactly the consolidation the publisher's index serves as current on the retrieval day (29 October 2026). `tools/parse.py` stops if the rebuilt Penal Code differs from the 2017 edition in any section.
- **Credits** come only from the publisher's marginal notes and its index. Anything they do not explain is committed by the publisher and labelled "unexplained".
- The repository is rebuilt from the same data a second time and must give identical hashes.

## What "author" means

The author of a commit is the law that made the change, with an e-mail address that cannot exist, so `git blame` and `git log --author` name laws. The committer is always Lexifina.

- **The first commit** of the Constitution and of the Data Protection Act is the law that made them (neither has been amended in the publisher's text). The Penal Code's first commit is the oldest version available (the 2010 consolidation), credited to the publisher; its message lists the laws the 2010 edition names, from 1873 to 2007.
- Blame credits whole lines (one paragraph per line). Use `git log -p --word-diff` to see exactly which words each change made.

## What it does not show

- **Amendments the publisher has not consolidated.** The site lists later amending Acts that no consolidation it serves includes: for the Penal Code, the Penal Code (Amendment) Acts of 2018 (commenced 31 December 2018), 2020 (9 December 2020) and 2024 (1 August 2024); for the Constitution, the Constitution (Amendment) Act, 2017 (commenced 10 May 2018), which the site serves only as a scanned image with no text layer. They are not in this history: the latest version of each act here is the publisher's current consolidation, not a text with those Acts applied. Nothing here reads text off a page image (no OCR).
- **Earlier history.** Every Penal Code change before the 2010 edition is folded into it.
- **Exact wording between the editions where two notes meet.** None of the Penal Code's sections names two of the newer laws, so no section needed a placeholder; if one did, its wording between the two laws would read "[The source does not give the text in force on this date.]".
- **Typesetting.** Running heads, page feet, footnotes, Part, Book and Title headings are left out; each file starts with its own number and the heading from the act's arrangement of sections. Spacing, quotes and dashes are normalised, and end-of-line hyphens are joined using the texts' own vocabulary. The words of the law are not changed. Marginal amendment notes are read for credits only.

## How it is built

`tools/fetch.py` reads the publisher's act index (a form posted per letter, with a point-in-time date), its Acts by Year pages, its Copyright page and the consolidation PDFs with curl, at most three requests a second, and caches each response by the sha256 of its address. `tools/parse.py` reads only that cache: `tools/pdftext.py` reads each PDF's text layer into sections, paragraphs and marginal notes; `parse.py` dates and credits each version and writes `corpus.json` and `corpus.d/`. The shared builder `tools/build.py` turns that into the commits. `REPRODUCE.md` lists every source, command, tool version and decision, and the result of the hash-for-hash rebuild.

## Sources

| Source | What it gives | Used for |
| --- | --- | --- |
| [Bahamas Laws On-line](https://laws.bahamas.gov.bs) (Government of The Bahamas) | Consolidated Acts as PDFs with a text layer, one per revised edition; a point-in-time act index with each amending Act's commencement date; Acts by Year | All text, dates and credits |


## Licence

See [LICENSE](LICENSE). The publisher's Copyright page states: "The legislation contained on this website is subject to Government of The Bahamas Copyright protection. Any reproduction shall ensure its accuracy, and the source and copyright status of the material is made evident to users. The website may only be used for informational non-commercial purposes and must not be used in a derogatory or defamatory manner." (The site's page metadata names the Isle of Man Attorney General's Chambers instead; that is a leftover from the iLAWSSYNC software the site runs on, not the Bahamas notice.) This repository is private. Lexifina's arrangement, messages, tables and tools are CC0.

This repository is not legal advice. The laws of The Bahamas are published in English, so there is no summary in another language.
