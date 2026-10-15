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

## Deployment

This repository deploys the `en-US` text host, `https://iso-20022-text-en-us.beneficialstrategies.com`, as a Cloudflare Worker with static assets (`wrangler.jsonc`),
through Cloudflare Workers Builds: the `main` branch deploys, and every other branch gets a preview address. The build fetches the
[hub](https://github.com/Beneficial-Strategies/iso-20022-text) (`HUB_REF` and `HUB_REPO` choose another version of it, for a preview) and lays this repository
over it, so a change in the hub reaches this host the next time this repository builds.

## Help keep this text maintained

This text is free, and it is only as good as the people who read it. Most of it was drafted with AI tools and **has not been read by a person who works with ISO 20022 in English (US)**. If you do, you can help in minutes:

* Say how a word should be translated: **[Glossary entry](https://github.com/Beneficial-Strategies/iso-20022-text-en-US/issues/new?template=glossary.yml)** ("when ISO 20022 says `Cheque` it should say `Check`"). The form asks which **variety** (general, or an industry or institution) uses it, so differences by region are captured, and a variety that comes up often can get a text of its own.
* Correct a definition: **[Wrong, unclear or missing translation](https://github.com/Beneficial-Strategies/iso-20022-text-en-US/issues/new?template=definition.yml)**.
* Take over the care of the language, a variety or a business area: **[Offer to review or maintain](https://github.com/Beneficial-Strategies/iso-20022-text-en-US/issues/new?template=volunteer.yml)**. Co-maintainers and sponsors change what this text can become: contact support@beneficialstrategies.com.

See [CONTRIBUTING.md](CONTRIBUTING.md) for how issues and pull requests work here.

## Status, license and warranty

This text is provided **free of charge and as is**, under the MIT license (see `LICENSE`), without warranty of any kind. We make our best-faith
effort toward an accurate text, but it is not verified by a professional translator, and entries may be machine drafts that no person has reviewed.
**Do not rely on it for legal, financial or compliance decisions**: the authoritative text is ISO's English.

**The controls here are lax at present**: there is no formal review process, release gating or ownership policy beyond what you can see in this
repository. We intend to improve them over time (named maintainers per area, required reviews, release checks) should the libraries gain adoption
and sponsorship. Taking over the care of a language, or of an area of one, is welcome.

The English text this repository translates or adapts is ISO's.

**ISO 20022 material.** The ISO 20022 specification, its schemas, code sets and their text are ISO's. ISO and its Registration Authority publish them to be used and reproduced freely under the [ISO 20022 Terms of use](https://www.iso20022.org/terms-use) and the [Intellectual Property Rights Policy](https://www.iso20022.org/intellectual-property-rights). **This is not the official ISO 20022 site. The sole source of up-to-date material is <https://www.iso20022.org/>.** ISO's material is provided "as is", without warranty. The license of this repository covers what we wrote, not ISO's material. This is not legal advice.