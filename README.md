# mankowkorp.github.io

The source of <https://mankowkorp.github.io> — a personal professional
biography, plus the public pages the Collab-Sorter OAuth application requires.

Hand-written static HTML. No build step, no framework, no dependencies.
GitHub Pages serves `main` directly, and `.nojekyll` disables Jekyll so files
are published exactly as committed.

## Layout

| Path | Live at | What it is | README |
|---|---|---|---|
| `index.html` | `/` | The biography. Method, then day work, then personal projects. The mail triage card repeats claims from `collab-sorter/`, so change both together. | this file |
| `migration/` | `/migration/` | Evidence page — a migration against an immovable cutoff | [↗](migration/README.md) |
| `guards/` | `/guards/` | Evidence page — scans that reported clean because they could not run | [↗](guards/README.md) |
| `scripted-review/` | `/scripted-review/` | Evidence page — a console-only review made repeatable | [↗](scripted-review/README.md) |
| `collab-sorter/` | `/collab-sorter/` | Project page for the mail triage service | [↗](collab-sorter/README.md) |
| `websites/` | `/websites/` | Project page — end-to-end site work | [↗](websites/README.md) |
| `verification/` | `/verification/` | Project page — backup, and a verifier that could not fail | [↗](verification/README.md) |
| `privacy.html` | `/privacy.html` | Privacy policy for the mail triage service | — |
| `style.css` | `/style.css` | The whole design system. Every page links it. | — |
| `demo/` | `/demo/` | **Generated. Do not edit.** See below. | — |
| `google*.html` | | Search Console verification token. Do not remove. | — |

### `demo/` is written by a different repository

Those files are produced by a workflow in the (private) Collab-Sorter repo and
pushed here automatically whenever the interface changes. **That workflow runs
`rm -rf demo/` before copying**, so anything added to that folder by hand —
including a README — is deleted on the next publish. Document it here instead.

## The rules

This repository is **public**. Everything committed to it is permanently
visible, and the site is indexed by search engines. These constraints are not
style preferences:

1. **No real person is ever named** — not a client, a client's customer, a
   colleague, or the person the mail triage service was built for.
2. **No employer, industry, location, or internal system** appears anywhere.
   Any one of those alone is fine in isolation; together they identify an
   organisation that has not agreed to be named here.
3. **No findings that describe unfixed problems.** Pages may describe method,
   or defects that are closed. A page must never document a live weakness.
4. **No credentials, hostnames, ticket references, or repository names**, in
   any file, including this one.
5. **No code from private repositories.**

Rule 2 is the one that most often gets broken by accident, because every part of
it seems harmless on its own — an industry, a region, a job title, a team size.
None of them identifies anyone alone; the combination identifies an organisation
that never agreed to be named. Nothing here has broken it, and keeping that true
is the entire point of scanning before every push.

## Making a change

1. Edit the page.
2. **Update that folder's `README.md` in the same commit.** Each one records
   what its page claims and what must not appear in it; a page that outgrows
   its README is how the rules above quietly stop being true.
3. Check nothing from *The rules* leaked. Scan across every page at once,
   and include a control pattern that you know is present — a scan that reads
   nothing prints exactly the same output as a scan that finds nothing.
   **Test any new pattern against the pages as they actually are, not against
   examples you invent.** The e-mail check was written and tested against
   made-up addresses; on its first real run it flagged all ten of the demo's
   RFC 2606 addresses, because the generator puts the reserved name in the TLD
   (`hello@x.test`) and the exclusion only handled it as a domain
   (`@example.com`). A guard tested on data its author made up is tested
   against the author's assumptions.
4. Verify locally: `python3 -m http.server`, then confirm every link returns
   200 before pushing.

CI enforces step 2: a push that changes a page without touching its README
fails. It cannot check that the README is *correct*, only that it was
considered.

## What is deliberately not here

The site does not carry a résumé, an employment history, dates, titles, or a
skills list — and it is not a portfolio of everything that has been built.
Several finished projects are excluded on purpose. That is a decision, not a
gap, and reversing it should be deliberate.
