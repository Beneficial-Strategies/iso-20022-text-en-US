# ISO 20022 text: en-US

The en-US text of the ISO 20022 message explorer and library. This repository holds **only what differs from the ISO English**: anything not written here shows the ISO English text.

## What to edit

Two things, and nothing else:

* **`glossary.json`** is the list of rewrite rules that turn the ISO English of the hub into American English: word stems (`authoris` -> `authoriz`),
  whole words (`cheque` -> `check`) and phrases (`Town Name` -> `City Name`). The build applies them to every name (including the values of a dropdown), definition and format
  text, so one line here fixes the word everywhere. Spelling first; the term swaps are judgement calls, each listed so it can be reviewed or removed.
* **`types/<first letter>/<Type>.json`** (when present) holds an **exception** for one type: only the entries and properties that differ, e.g.
  `{ "isoType": "ChequeType2Code", "definition": "Specifies the type of check." }` or an entry under `isoElements`, `isoCodes` or `isoRules`. An entry here wins over a glossary rule.
  Keep element names, acronyms (IBAN, BIC, ...) and `|` (a line break) as they are in the hub.

Everything not written here is the hub's text, with the glossary applied. Who changed what and when is the repository's history.

## Building what the host serves

```sh
node ../iso-20022-text/build/overlay.mjs --spoke . --out /path/to/output
```

The output is the complete text of every type, in the shape of the [convention](https://github.com/Beneficial-Strategies/iso-20022-text/blob/main/SPECIFICATION.md).
It is never edited by hand and not committed. There is no automatic check on pull requests yet.

## Status, license and warranty

This text is provided **free of charge and as is**, under the MIT license (see `LICENSE`), without warranty of any kind. We make our best-faith
effort toward an accurate text, but it is not verified by a professional translator, and entries may be machine drafts that no person has reviewed.
**Do not rely on it for legal, financial or compliance decisions**: the authoritative text is ISO's English.

**The controls here are lax at present**: there is no formal review process, release gating or ownership policy beyond what you can see in this
repository. We intend to improve them over time (named maintainers per area, required reviews, release checks) should the libraries gain adoption
and sponsorship. Taking over the care of a language, or of an area of one, is welcome.

The English text this repository translates or adapts is ISO's, and ISO's own terms apply to it. The license above covers what is written
in this repository, not ISO's text. This is not legal advice.