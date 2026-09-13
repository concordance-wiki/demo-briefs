---
date: 2026-07-09
participants: [Participant-1, Participant-2, Participant-4]
decisions: [specs/decisions/inference/minhash-for-twin-resources]
domain: ingestion
source: twin-resources-review.vtt
---
# Twin resources review

Working session on how the forms of one document, a deck, its notes, the transcript of the session where it was shown, are recognised as one page. Three participants: the maintainer, an author of the specifications and the quality owner. The transcript sits next to these minutes.

## What was said

- The commit and the folder never found a pair on their own: an initial import puts every file in one commit. A pair is founded by a declaration in the frontmatter, a shared base name, a title equal to a heading, or similar extracted text; the commit and the folder proximity only reinforce it.
- Similar text is the expensive signal. Each text goes to its comparison form, then to shingles of five words, then to a MinHash signature under a fixed seed; LSH banding enumerates the candidate pairs, so that the full matrix of a corpus is never built.
- A deck and its notes rarely share sentences: when the word counts of a pair differ by more than half, the pair is an inclusion rather than a duplicate, its content signal is capped and the finding says so. The base name and the title do the rest.
- The page of a merged document names the signals of every scored pair, and the lock wins over the score in both directions: `merged` pairs merge, `separated` pairs neither merge nor report.
- Two runs, or a shuffled input, give the same groups: resources are sorted by identifier before anything else and every output is sorted.

## Decision

MinHash for twin resources: the estimate on 128 functions decides which pairs are close, the exact Jaccard index is recomputed on the pairs estimated at one half or more, and the finding gives the share of lines in common. The quality owner reviews the wording of the duplicate candidate finding.
