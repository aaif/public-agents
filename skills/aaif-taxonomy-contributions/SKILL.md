---
name: aaif-taxonomy-contributions
description: Guides agents through contributing to the AAIF Common Taxonomy and Landscape workstream (aaif/ws-taxonomy-landscape). Use when a contributor wants to propose a new taxonomy term, define an accepted term, change an existing definition, or add something to the ecosystem landscape, and needs to know which path the workstream will actually accept.
metadata:
  author: Asish Singh
  organization: AAIF
  source: https://github.com/aaif/ws-taxonomy-landscape/blob/main/CONTRIBUTING.md
  version: "2.0"
---

# AAIF Taxonomy and Landscape Contributions

Use this skill when helping someone contribute to the AAIF Common Taxonomy and Landscape workstream at `aaif/ws-taxonomy-landscape`. The workstream maintains the shared vocabulary (taxonomy) and the ecosystem map (landscape) for all AAIF working groups. Most rejected contributions fail on routing, not content, so decide the route before drafting anything.

## Read the live rules first

Fetch `CONTRIBUTING.md` from the repository before advising. It is the governing document and has changed more than once. Where it disagrees with `docs/data-schemas.md` (for example on whether definition pull requests are welcome), `CONTRIBUTING.md` wins, because the schema doc's guidance on deferred fields predates the current process. Then check whether the taxonomy data still lives in `taxonomy/taxonomy-data.js` or has moved to `taxonomy/taxonomy.json` (a migration to JSON with schema validation was proposed in pull request #79), and edit whichever file is current.

## Route the contribution

| The contributor wants to | Correct path |
| --- | --- |
| Propose a new term | Ask the delegate from the owning working group to add it to the taxonomy spreadsheet linked in `CONTRIBUTING.md` and flag it in the workstream Discord channel. The weekly workstream meeting votes KEEP, CULL or DEBATE. Non delegates can also attend that meeting to advocate for the term. |
| Define a term that received a KEEP vote | A pull request, normally from a delegate of the owning working group, defining one term. Confirm the KEEP vote before drafting, since pull requests for terms without one are closed. |
| Define a term with no KEEP vote yet | Not a pull request. Route it through the spreadsheet and meeting first. An issue is acceptable for discussion but does not substitute for the vote. |
| Change or correct an existing definition | A pull request against the existing entry, with the reason stated. Pull requests titled `Update taxonomy term: <Term>` are the established shape. |
| Add or fix a landscape entry | Nothing yet. The landscape process has not been approved and landscape pull requests are closed. Note the proposal and hold it until `CONTRIBUTING.md` reopens that lane. |
| Question the process, ownership or placement | An issue, or the weekly meeting. |

## Before drafting a definition

1. Confirm the term exists in the taxonomy data and check its current entry.
2. Search open pull requests and issues for the same term. Several delegates draft in parallel, so overlaps are common. If one exists, reference it and offer to reconcile rather than racing it.
3. Check whether the term duplicates an existing concept. A genuine synonym belongs in that entry's `aliases`. Deliberately distinct concepts stay separate, and folding one into another needs the owning working group's agreement.

## The quality bar

The definition is one sentence. Supporting detail, examples and boundaries go in `scopeNote`. A good definition names something a reader can test against a borderline case, so it says what would make the term not apply, not merely what the thing is for. Keep it vendor neutral and free of product names. When a term has a contrasting counterpart (Tool and Skill, for example), its definition must say how it differs, and the pair should be linked through `contrastsWith` or `relatedTerms`. Point those fields only at terms already in the taxonomy, and propose any missing term separately.

## Pull request shape

Recent merged definitions (for example `Define universal term Subagent`, pull request #68) follow this shape.

- Title `Define universal term <Term>` for a universal term, or `Define taxonomy term: <Term>` for one owned by a working group.
- One term per pull request unless there is a reason to group them. Multi term pull requests may need more approvals.
- The entry keeps the existing field order. `category` stays `''` and `broaderTerm` stays `null` while those fields remain deferred. `workgroups` never contains `Universal`, and a term owned by no single group carries `[]`.
- The description names the KEEP vote (meeting date), the owning working group, and any overlapping pull request or issue.

## After submission

A single term pull request needs two approvals from delegates representing different working groups, and any delegate can veto. Once approved, a maintainer merges with Rebase and merge and the spreadsheet row is marked FINALIZED. If a pull request stalls, raise it at the weekly meeting rather than pinging reviewers repeatedly.
