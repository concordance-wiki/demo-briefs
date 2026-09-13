---
date: 2026-06-18
participants: [Participant-1, Participant-2, Participant-3]
decisions: [specs/decisions/publication/purpose-built-contract-viewer]
domain: inference
source: contract-import-scope.vtt
---
# Contract import scope review

Working session on what the contract import reads and what it leaves to the notes. Three participants: the maintainer, an author of the specifications and the integrator of the wiki. The transcript of the session sits next to these minutes and the build shows both on one page.

## What was said

- An API note that declares a contract gets one operation per operation of the contract; the operation matching rule attaches each one to the operation note that names the same operation id, or the same method and path. The note absorbs the imported operation, which never exists twice.
- An operation nobody wrote about keeps the properties of the contract only and is reported by the operation unmatched check, a warning, so that someone writes the note.
- The contract file lives next to its note, under `contracts/`, and the fingerprint cache keeps its parsed text between two builds.
- A contract that cannot be fetched or parsed yields the contract unreachable finding; the note keeps its hand-written operations and the build goes on.

## Decision

The interactive console the specification named for OpenAPI contracts is not used: it weighs more than the page budget, expects to fetch the contract over the network and offers to call the API from the page. The contract of an API is shown by a purpose-built contract viewer, an island rendered from a JSON fragment of the contract, loaded on demand. The schemas of the contract become candidate objects, listed on the to-do page.
