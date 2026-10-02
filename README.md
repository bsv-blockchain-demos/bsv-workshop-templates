# BSV Workshop Templates

Markdown templates and draft learning materials for authors preparing BSV blockchain workshops. The repository provides a common structure for workshops, reusable technical modules, demonstrations and practical exercises.

## Start here

- [Workshop template](workshop/workshop-template.md): plan a complete session, including objectives, an agenda, exercises and assessment.
- [Primitive module template](primitives/primitive-module-template.md): explain a reusable capability, its transaction structure and its practical application.
- [Templates index](00-templates-index.md): browse the repository's original navigation and editorial notes.

Draft workshops are available for [payments](payments.md), [data inscription](data-inscription.md) and [tokenisation](tokenization.md).

## Use the templates

1. Copy the workshop template into a new Markdown document and set its audience, level, duration and prerequisites.
2. Choose the relevant sections from [workshop/sections](workshop/sections/) and modules from [primitives](primitives/).
3. Replace placeholders with specific learning outcomes, explanations and exercises appropriate to the audience.
4. Add links to the actual demonstration code, required tools and supporting references.
5. Run each exercise in the intended environment, record the expected result, and update the document's status and `last_updated` metadata.

The materials can be read on GitHub or edited with any Markdown editor. No dependency installation or build step is required.

## Repository guide

| Location | Contents |
| --- | --- |
| [workshop/](workshop/) | Complete workshop template and individual section outlines. |
| [primitives/](primitives/) | Modules covering payments, identity, data inscription, tokens, proofs, overlays and other capabilities. |
| [demos/](demos/) | Templates for demonstrations and proofs of concept. |
| [use-cases/](use-cases/) | A template for explaining application scenarios. |
| [code/](code/) | A template for documenting a code showcase and its run instructions. |
| [shared/](shared/) | Glossary and reference templates. |
| [meta/](meta/) | A changelog template. |

## Current scope

These materials are drafts. Several documents contain placeholders, illustrative code or descriptions of companion applications that are not included in this repository. In particular, the workshop references to files such as `wallet.js`, `transactions.js` and `token.js` describe proposed examples rather than files available here.

Before delivering a workshop, supply and test its companion application, verify technical claims and links, and make the network and funding requirements explicit for any transaction exercises.

## Licence

**Open BSV Licence v6.** See [LICENSE.txt](LICENSE.txt) for the full terms. The licence applies to this project's original code and documentation and restricts use to the BSV blockchain defined in the licence. Third-party code, assets and referenced standards retain their respective terms.
