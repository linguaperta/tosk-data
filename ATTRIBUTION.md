# Attribution

The Duelingo course packs are built from open data by the pipeline in the `duelingo` repository
(`pipeline/`). This file lists every source, its license, and how it was changed.

## Wiktionary (CC BY-SA 4.0, also GFDL)

* **English Wiktionary** (https://en.wiktionary.org), Italian and Dutch entries, via the
  wiktextract/kaikki.org machine-readable dumps (https://kaikki.org/dictionary/Italian/,
  https://kaikki.org/dictionary/Dutch/). Used for lemmas, parts of speech, gender, plurals,
  inflected forms, English glosses (`tr_src.en = "wiktionary"`) and conjugation tables
  (`verbs/*.jsonl`).
* **English Wiktionary translation tables** (https://kaikki.org/dictionary/English/): Italian and
  Dutch words listed for the same English sense give Dutch glosses for Italian words
  (`tr_src.nl = "wiktionary-pivot"`).
* **Dutch Wiktionary** (https://nl.wiktionary.org) via https://kaikki.org/nlwiktionary/: Dutch glosses
  for Italian words (`tr_src.nl = "nlwiktionary"`) and the perfect auxiliary (hebben/zijn) of Dutch verbs.

Changes: glosses shortened and filtered, archaic/regional forms dropped, compound tenses
(passato prossimo, perfectum) generated from the auxiliary and the participle, stem/ending splits
and regularity flags computed. Authors: the Wiktionary contributors (see each entry's page history).
Wiktextract: Tatu Ylonen, "Wiktextract: Wiktionary as Machine-Readable Structured Data", LREC 2022.

## Tatoeba (CC BY 2.0 FR)

Example sentences and their translations from https://tatoeba.org (per-language exports from
https://downloads.tatoeba.org/exports/). Sentence ids `s:N` and `src: "tatoeba:N"` refer to
https://tatoeba.org/sentences/show/N, where the author of each sentence is listed; translations
carry their own Tatoeba id in `tr_src`. Changes: filtered by length and vocabulary, tokenized and
aligned to the lexicon. Text is unchanged.
Pairs whose numbers, weekdays/months or names disagree (a link to another variant of the sentence)
are left out (`pipeline/trcheck.py`).

## Word frequencies (CC BY-SA 4.0)

hermitdave/FrequencyWords, 2018 lists `it_50k.txt` and `nl_50k.txt`
(https://github.com/hermitdave/FrequencyWords), derived from OpenSubtitles (http://www.opensubtitles.org).
Used only to rank words (`freq`).

## Written with Claude

Course structure (`course.yaml`), curated vocabulary lists and their glosses (`seed.yaml`; items with
`tr_src: "claude"`), the Dutch glosses for Italian verbs used in grammar skills, a few Dutch perfect
auxiliaries missing from Wiktionary (zijn, hebben, worden, blijven) and all grammar notes
(`grammar/*.md`) were written with Claude (Anthropic) for this project and are released under
CC BY-SA 4.0 like the rest of the repository.

### Generated example sentences

Where Tatoeba has too few easy sentences for a grammar slot or word, Claude (Anthropic) wrote short
example sentences with their translations: `content/{it,nl}/sentences/gen-*.jsonl`, ids `g:{course}:{n}`
(`sentence_ids.tsv`), `src` and `tr_src` = `claude-gen`. They were checked mechanically by the
pipeline (`python -m pipeline gen`) and reviewed for naturalness, and are released under CC BY-SA 4.0
as part of the course packs. Counts (2026-10): Italian 2113 of 20 314 sentences, Dutch 762 of 14 767;
the rest are Tatoeba sentences.
