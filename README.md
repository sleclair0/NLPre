# Natural Language Preprocessing (NLPre)

[![Build Status](https://travis-ci.org/NIHOPA/NLPre.svg?branch=master)](https://travis-ci.org/NIHOPA/NLPre)
[![codecov](https://codecov.io/gh/NIHOPA/NLPre/branch/master/graph/badge.svg)](https://codecov.io/gh/NIHOPA/NLPre)

NLPre is a text (pre)-processing library that helps smooth some of the inconsistencies found in real-world data.
Correcting for issues like random capitalization patterns, strange hyphenations, and abbreviations are essential parts of wrangling textual data but are often left to the user.
The library is developed by the [Office of Portfolio Analysis](https://dpcpsi.nih.gov/opa/aboutus) at the [National Institutes of Health](https://www.nih.gov/) and many of the utilities are designed to correct for historical artifacts in our data.
The goals of NLPre are a set of functions that can act in a pipeline independent of one another with a consistent and predictable result.

NLPre is part of the [`word2vec-pipeline`](https://github.com/NIHOPA/word2vec_pipeline).

### Installation

    pip install git+git://github.com/NIHOPA/NLPre.git

### Timeline to release

+ [x] Import modules from pipeline_word2vec
+ [x] Document which functions exists in README
+ [x] Write unit tests for individual functions
+ [x] Write unit tests for pipelines (multi-function)
+ [x] Write doc strings for all functions
+ [x] Format as proper python package
+ [x] Complete import (missing ABBR phrase replacement)
+ [ ] Clean and format the README
+ [ ] Upload to pypy


### What's included?

| Function | Description |
| --- | --- |
| [**dedash**](nlpre/dedash.py) | When text is passed though a word-processor sometimes hyphenations with with newlines are inserted. This module attempts to correct the hyphenation pattern by joining words that if they appear in an English word list. <br> `How is the treat- ment going` -> `How is the treatment going` |
| **decaps** | We presume that case is important, but only when it differs from title case. This class normalizes capitalization patterns. <br> `James and Sally had a fMRI` -> `james and sally had a fMRI` |
| [`separated_parenthesis`](nlpre/separated_parenthesis.py) | Separates parenthetical content into new sentences. This is useful when creating word embeddings, as associations should only be made within the same sentence. This parser returns a document that is sentence chunked and appends parenthetical content as a new sentence to the sentence following the sentences it was found in. Terminal punctuation of a period is added to parenthetical sentences if necessary. <br> `Hello (it is a beautiful day) world.`<br>`Hello world. it is a beautiful day .` |
| **replace_from_dictionary** | Noun phrases from a predefined dictionary are replaced. The [MeSH](https://www.nlm.nih.gov/mesh/) dictionary comes included. |
| **replace_phrases** | Phrases found though an abbreviation finder (not included yet), are replaced. |
| **titlecaps** | WHY ARE SOME SENTENCES IN ALL CAPS? These sentences are converted to lower case. |
| **token_replacement**| Simple token replacement (% -> `percent`) |
| **pos_tokenizer**| Parts of speech are filtered out by using a white-list. |
| **unidecoder**| Converts Unicode phrases into ASCII equivalent, (`β-sheet` -> `b-sheet`). |
| **identify_parenthetical_phrases** | `What is Health and Human Services (HHS)?` gets tokenized as `counter[(('Health', 'and', 'Human', 'Services'), 'HHS')]` |

