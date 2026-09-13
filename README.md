# Concordance briefs

The working sessions of the Concordance project: the minutes, the transcript and, when one was shown, the deck of each session, plus the framing decks of the project. This repository is a demonstration corpus for the tool and the third source of the project's own wiki, published by [demo-wiki](https://github.com/concordance-wiki/demo-wiki) together with the [glossary](https://github.com/concordance-wiki/demo-glossary) and the [specifications](https://github.com/concordance-wiki/demo-specs). Where those two repositories hold notes someone writes, this one holds the raw material a reader converts: transcripts, slide decks, PDF previews, and the notes that accompany them.

## Layout

```
meetings/2026/<date>-<slug>/   one folder per session
  <slug>.md                    the minutes: date, participants, the decision the session produced
  <slug>.vtt                   the WebVTT transcript, one cue per line spoken, speakers named
  <slug>.pptx                  the deck shown during the session, when there was one
  <slug>.pdf                   its preview
framing/2026/<date>-<slug>/    one folder per framing deck
  <slug>.pptx, <slug>.pdf      the deck and its preview
  <slug>.md                    the written form of the deck
```

The wiki's `concordance.yaml` types every file under `meetings/` as a `meeting`, every `.vtt` file as a meeting wherever it is, and everything else as a `document`, the source's default type; `convert: true` sends the decks through LibreOffice at build so that the site previews them and reads their text. The files of one folder are the twin resources of one page: every file shares the base name of the session, the minutes carry the title of the deck as their heading and declare their transcript under `source:`, the preview repeats the text of the deck, and every file of a folder lands in the same commit; the build adds these signals up, groups the files into one entity with one tab per file, and says why under the properties of the page.

The minutes name the decision each session produced by its identifier in the specifications (`decisions:` in the frontmatter) and name the terms of the glossary and the notes of the specifications by their titles, so that the recognition links them. The transcripts name the fictional participants of the corpus, four people of the project; the wiki's `pseudonyms.yaml` maps each name to a stable pseudonym and the build replaces the names, in the speaker of every cue and in the spoken text, before anything reads the transcript. The names are invented for the demonstration and the dictionary is committed for the same reason; a real wiki keeps its dictionary out of every public repository, as the [publishing transcripts](https://github.com/concordance-wiki/concordance/blob/main/docs/guides/publishing-transcripts.md) guide says.

The decks are written as flat ODF presentations (`<slug>.fodp`, kept out of the repository) and converted once with `soffice --headless --convert-to pptx` and `--convert-to pdf` into their folder.

Every markdown file passes `concordance lint` without a finding. This repository lints itself on every push with the linter built from the tool's repository (`.github/workflows/lint.yml`), then tells the wiki to rebuild. This README is not a note: the wiki's configuration excludes it.
