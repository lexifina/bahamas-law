# How this repository was made (The Bahamas)

This file is written by the build on 2026-10-29, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
| Bahamas Laws On-line: act index by letter, point in time | <https://laws.bahamas.gov.bs/cms/legislation/acts_only/by-alphabetical-order.html> | 2026-10-29 | Government of The Bahamas Copyright; the site may be used for informational non-commercial purposes (its Copyright page, quoted in licence_note) |
| Bahamas Laws On-line: Acts by Year | <https://laws.bahamas.gov.bs/cms/legislation/acts_only/acts-by-year.html> | 2026-10-29 | Government of The Bahamas Copyright; the site may be used for informational non-commercial purposes (its Copyright page, quoted in licence_note) |
| Bahamas Laws On-line: Copyright | <https://laws.bahamas.gov.bs/cms/?view=article&id=115:copyright&catid=14:general-articles> | 2026-10-29 | Government of The Bahamas Copyright; the site may be used for informational non-commercial purposes (its Copyright page, quoted in licence_note) |
| Bahamas Laws On-line: Constitution (Amendment) Act, 2017 (PDF) | <https://laws.bahamas.gov.bs/cms/images/LEGISLATION/AMENDING/2017/2017-0020A/2017-0020A.pdf> | 2026-10-29 | Government of The Bahamas Copyright; the site may be used for informational non-commercial purposes (its Copyright page, quoted in licence_note) |
| Bahamas Laws On-line: The Constitution, revised edition LRO 1/2006 (PDF) | <https://laws.bahamas.gov.bs/cms/images/LEGISLATION/PRINCIPAL/1973/1973-1080/1973-1080_1.pdf> | 2026-10-29 | Government of The Bahamas Copyright; the site may be used for informational non-commercial purposes (its Copyright page, quoted in licence_note) |
| Bahamas Laws On-line: Penal Code, Ch. 84, revised edition LRO 1/2010 (PDF) | <https://laws.bahamas.gov.bs/cms/images/LEGISLATION/PRINCIPAL/1873/1873-0015/1873-0015_1.pdf> | 2026-10-29 | Government of The Bahamas Copyright; the site may be used for informational non-commercial purposes (its Copyright page, quoted in licence_note) |
| Bahamas Laws On-line: Penal Code, Ch. 84, revised edition LRO 1/2017 (PDF) | <https://laws.bahamas.gov.bs/cms/images/LEGISLATION/PRINCIPAL/1873/1873-0015/1873-0015_2.pdf> | 2026-10-29 | Government of The Bahamas Copyright; the site may be used for informational non-commercial purposes (its Copyright page, quoted in licence_note) |
| Bahamas Laws On-line: Data Protection (Privacy of Personal Information) Act, Ch. 324A, revised edition LRO 1/2008 (PDF) | <https://laws.bahamas.gov.bs/cms/images/LEGISLATION/PRINCIPAL/2003/2003-0003/2003-0003_1.pdf> | 2026-10-29 | Government of The Bahamas Copyright; the site may be used for informational non-commercial purposes (its Copyright page, quoted in licence_note) |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constitution` | The Constitution of the Commonwealth of The Bahamas | 1 | 1973-07-10 to 1973-07-10 |
| `penal-code` | Penal Code (Ch. 84) | 7 | 2009-10-01 to 2016-12-31 |
| `data-protection` | Data Protection (Privacy of Personal Information) Act (Ch. 324A) | 1 | 2007-04-02 to 2007-04-02 |

The build made 10 commits:

| Commits | Kind |
| ---: | --- |
| 3 | first version of an act |
| 6 | one law on its in-force day |
| 1 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-10-29.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 62 laws in the record.
- 17 tags.

## Dates

Each commit is dated at noon (America/Nassau) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Each law is dated by the "Date Commenced" the publisher's act index or its Acts by Year list gives for it; no date is derived from publication. https://laws.bahamas.gov.bs/cms/legislation/acts_only/by-alphabetical-order.html

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `b0fcf82c1bdbc0f4c3450f584432e54bab82c3540cb87fe7354364ccad74db59` (822548 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3d00541d258745461ab52b1b0cb4e1716a27a95d`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
- Python 3.12.10; git version 2.46.0.windows.1.

## Checks

9 versions of 3 acts read back from git on the day each took effect and on the day before: 0 mismatches. Trailers: 0 commits whose trailers git cannot parse. Health: 0 merge commits on main, 0 commit dates that go backwards, 0 commits dated after the build.

No second build of this corpus has been compared yet.

## Decisions made by hand

- Sources: only laws.bahamas.gov.bs, the official legislation site.
- Text: each consolidation PDF's own text layer; running heads, page feet, footnotes and footnote markers, and Part, Book and Title headings are dropped; marginal headings become each provision's first line; quotes and dashes are normalised to ASCII; end-of-line hyphens are removed when the joined word occurs elsewhere in these texts and kept when the hyphenated form does, or either half is capitalised.
- Every date is a commencement date from the publisher's own index; no publication date is used.
- Constitution: one version, the 1973 text as printed in LRO 1/2006 (the publisher's only consolidation, still current in its index on the retrieval day), whose footnote states the Constitution "to date has not been amended"; credited to The Bahamas Independence Order 1973 (S.I. 1973 No. 1080) and dated 10 July 1973, the commencement date the index gives.
- Constitution: Constitution (Amendment) Act, 2017 (No. 2017-0020, commenced 2018-05-10 per the index) is left out: the site serves it only as a scanned image with no text layer (no OCR), and the current consolidation does not include it.
- Penal Code: two dated consolidations from the publisher's point-in-time index: LRO 1/2010 (listed up to 2016-12-30) and LRO 1/2017 (listed from 2016-12-31). The first is dated 2009-10-01, the commencement of the last law in its list of laws (Act 1 of 2007, the Child Protection Act), and credited to the publisher as the oldest version available.
- Penal Code: a provision whose words differ between the editions and whose marginal note in LRO 1/2017 names a law not in LRO 1/2010's list of laws takes its LRO 1/2017 wording on that law's commencement date (from the index's "amended by" rows, else its Acts by Year page), credited to that law. 52 provisions are credited this way.
- Penal Code: the other 9 provisions whose words differ carry no such note (corrected cross-references, removed short-title years, punctuation and the typesetting of each edition); they are committed by the publisher as unexplained on 2016-12-31.
- Penal Code: provisions with the same words in both editions keep the 2017 edition's paragraph breaks in every version, so only wording changes show in the history.
- Penal Code: the 2010 edition prints the law "29 of 1953" as "29 or 1953"; it is read as Act 29 of 1953.
- Penal Code: Act 28 of 2008 (title not given) has no commencement date on the site; its 3 provisions are dated 2016-12-31, the day the first consolidation containing them became current, and its commit says so.
- Penal Code: Penal Code (Amendment) Act, 2018 (No. 2018-0037, commenced 2018-12-31) is not in any consolidation the site serves (the current one is LRO 1/2017), so it is not in this history; today's official consolidation is the 2017 edition.
- Penal Code: Penal Code (Amendment) Act, 2020 (No. 2020-0033, commenced 2020-12-09) is not in any consolidation the site serves (the current one is LRO 1/2017), so it is not in this history; today's official consolidation is the 2017 edition.
- Penal Code: Penal Code (Amendment) Act, 2024 (No. 2024-0007, commenced 2024-08-01) is not in any consolidation the site serves (the current one is LRO 1/2017), so it is not in this history; today's official consolidation is the 2017 edition.
- Data Protection Act: one version, the revised edition LRO 1/2008, dated by the commencement the index gives (2007-04-02) and credited to the Act itself (No. 3 of 2003): the index lists no amending act on any day checked, the edition's list of laws names only the Act and its commencement order, and no provision carries an amendment note (notes naming laws: 0).

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- none: no model wrote or changed any legal text, date or credit; parsing is deterministic code.
