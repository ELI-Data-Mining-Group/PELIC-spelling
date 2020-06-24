# PELIC_spelling

**Version 1.0  
Authors: Ben Naismith, John Starr, Eva Bacas
Contact: bnaismith@pitt.edu**

This repo provides information and code about applying spelling correction to the PELIC dataset.

<br>

## Table of contents
1. [Overview](#1-Overview)
2. [Repository contents](#2-Repository-contents)
3. [SCOWL wordlist](#3-SCOWL-wordlist)
4. [PELIC spelling](#4-PELIC-spelling)
5. [Licenses](#6-Licenses)

<br>

## 1. Overview
This README.md file introduces the PELIC-spelling repository which provides information and code about applying spelling correction to the PELIC dataset. To download and find out more about the PELIC dataset, see the [PELIC-dataset](https://github.com/ELI-Data-Mining-Group/PELIC-dataset) repository. For information regarding publications and presentations based on PELIC data, as well as for information regarding the people and parties responsible for the corpus, please visit the [Pitt ELI Corpus](https://github.com/ELI-Data-Mining-Group/Pitt-ELI-Corpus) repository.

Spelling correction is an important element to consider in any corpus study involving learner data. The decision whether to correct texts or not will invariably impact results: in some instances it may be preferable to use the raw text, maintaining its integrity and avoiding an additional layer of processing. However, for other projects, corrected text may provide a more accurate representation of the language features being investigated.

There are two main components to the spelling correction process, presented in two Jupyter notebooks:

1. The [SCOWL_wordlist](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/SCOWL_wordlist.ipynb): In this notebook we decide on a list of what we consider to be real words, using an edited version of the [SCOWL wordlists](http://wordlist.aspell.net/).
2. [PELIC_spelling](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/PELIC_spelling.ipynb): In this notebook we create a dataframe of misspellings, apply an automated spelling correction process, and re-incorporate the corrected text into our corpus.

<br>

## 2. Repository contents
The [PELIC-spelling](https://github.com/ELI-Data-Mining-Group/PELIC-spelling) repository contains 14 main files:

File        | File type | Description  
:---        | :--- | :---
[all_names.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/all_names.txt) | text | list of over 90,000 names (first and last) from the 1990 US census data. Names collected by the [_names_](https://pypi.org/project/names/) random name generator project
[contractions.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/contractions.txt) | text | short list of contractions approved as legitimate tokens (not misspellings)
[frequency_bigramdictionary_en_243_342.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/frequency_bigramdictionary_en_243_342.txt) | text | bigram frequency dictionary supplied by [SymSpell](https://github.com/wolfgarbe/SymSpell) spell correction module
[frequency_dictionary_en_82_765.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/frequency_dictionary_en_82_765.txt) | text | frequency dictionary supplied by [SymSpell](https://github.com/wolfgarbe/SymSpell) spell correction module
[hyphens.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/hyphens.txt) | text | list of hyphenated words which appear in PELIC and have been approved as legitimate tokens (not misspellings)
[PELIC_compiled_spellcorrected.csv](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/PELIC_compiled_spellcorrected.csv) | csv | final output of updated `PELIC_compiled.csv` with spelling correction
[PELIC_spelling.ipynb](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/PELIC_spelling.ipynb) | Jupyter notebook | notebook demonstrating how spelling correction is applied to PELIC texts
[PELIC-SCOWL.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/PELIC-SCOWL.txt) | text | a combination of the [SCOWL_condensed.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/SCOWL_condensed.txt), [contractions.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/contractions.txt), and [hyphens.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/hyphens.txt) lists
[README.md](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/README.md) | markdown | this file describing the repository
[SCOWL_condensed.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/SCOWL_condensed.txt) | text | final compiled word list based on SCOWL word lists
[SCOWL_supp.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/actually_ok) | text | short list of words manually approved as being legitimate words, e.g. proper names not found in SCOWL
[SCOWL_wordlist.ipynb](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/SCOWL_wordlist.ipynb) | Jupyter notebook | notebook demonstrating how the SCOWL_condensed word list is created
[SCOWL_wordlist.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/SCOWL_wordlist.txt) | text | the full SCOWL wordlist before condensing

<br>

## 3. SCOWL wordlist
This notebook produces a definitive list of 'real' words to use when deciding what to consider a word/non-word. The final output is the [SCOWL_condensed.txt](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/SCOWL_condensed.txt) file. The primary wordlists are from the SCOWL set of word lists, freely availabe at http://wordlist.aspell.net/.

The notebook is divided into two main sections:

- _Exploratory Data Anaylsis_ : Here, we examine the various SCOWL dictionaries which include different language varieties, proper nouns, slang, abbreviations, etc. From this exploration, we opt to include all available dictionaries _except_ the abbreviation dictionaries due to the high number of short strings of letters which may match learner errors. It is possible, however, to include these dictionaries if desired.

- _Compiling and condensing dictionaries_ : In the second part of the notebook, [SCOWL_condensed](https://github.com/ELI-Data-Mining-Group/PELIC-spelling/blob/master/SCOWL_condensed.txt) is created by combining the various SCOWL dictionaries and then removing duplicates, blanks, and possessives. The final wordlist is slightly less than 500k words.

<br>

## 4. PELIC spelling
This notebook adds further processing to `PELIC_compiled.csv`  in the [`PELIC-dataset`](https://github.com/ELI-Data-Mining-Group/PELIC-dataset) repo by creating a column of tokens and their parts of speech which have been corrected in terms of spelling.

The notebook is divided into four main sections:

- _Building a `non_words` dataframe_ : We first collect all of the non-words from the PELIC dataset (in `PELIC_compiled.csv`) by extracting all words which are not found in `SCOWL_condensed`:

```python
>>> non_words.head()
```
|    | tok_lem_POS                       | sentence                                                                                                                             |   answer_id |
|---:|:----------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------|------------:|
|  0 | ('beacause', 'beacause', 'NN')    | i organized the instructions by time, beacause to make tea people who want to make tea have to follow the instructions step by step. |           8 |
|  1 | ('wallmart', 'wallmart', 'NN')    | next, you need to buy a box of tea in wallmart or giant eagle.                                                                       |          11 |
|  2 | ('dovn', 'dovn', 'NN')            | first, you should take some hot water, you can use dovn, mircowave or other ways.                                                    |          13 |
|  3 | ('mircowave', 'mircowave', 'VBP') | first, you should take some hot water, you can use dovn, mircowave or other ways.                                                    |          13 |
|  4 | ('paragragh', 'paragragh', 'NN')  | every paragragh's instructions depend on a main idea.                                                                                |          16 |

- _Building a dataframe of misspellings and their frequencies_ : In the non-words dataframe above, each row is an occurrence of a misspelling (i.e. tokens). We then create a dataframe where each row is a misspelling type with frequency information attached:

```python
>>> misspell_df.sample(5)
```

| Index| misspelling   | tok_lem_POS                        |   freq |
|-----:|:--------------|:-----------------------------------|-------:|
| 9164 | spel          | ('spel', 'spel', 'VB')             |      1 |
| 5495 | invesigate    | ('invesigate', 'invesigate', 'VB') |      1 |
| 3645 | estmatied     | ('estmatied', 'estmatied', 'JJ')   |      1 |
| 9313 | straigten     | ('straigten', 'straigten', 'VB')   |      1 |
| 8455 | hobbys        | ('hobbys', 'hobbys', 'NN')         |      2 |

- _Applying spelling correction_ : Having collected and organized the misspellings, we then correct these occurrences using [`SymSpell`](https://github.com/mammothb/symspellpy). In SymSpell complete sentence context is not considered, only bigrams and frequencies. Though this is not ideal, other well-known spellcheckers (hunspell, pyspell, etc.) use the same strategy - frequency based criteria for suggestions, without considering co-text beyond bigrams. As such, it is important to remember that accuracy of corrected tokens will not be 100% and must be taken into consideration.

```python
>>> print(non_words2[['answer_id','misspelling','sentence','final_correction_POS']].sample(5))
# Sample of 5 rows and key columns
```

|answer_id | misspelling                       | sentence                                                                                      | final_correction_POS              |
|------------:|:----------------------------------|:----------------------------------------------------------------------------------------------|:----------------------------------|
|       11487 | ('celemony', 'celemony', 'NN')    | Third, the ANON_NAME_0-Ju international movie celemony is opened in my hometown.              | ('ceremony', 'ceremony', 'NN')    |
|       13444 | ('miliion', 'miliion', 'NN') | 200 miliion people                                                                       | ('million', 'million', 'NN') |
|       17707 | ('korian', 'korian', 'JJ')   | Korian pizza is healthier than American pizza.                                           | ('korean', 'korean', 'JJ')   |
|       35162 | ('grammer', 'grammer', 'NN') | Although my grammer was not impeccable, they could usually understand what I meant.      | ('grammar', 'grammar', 'NN') |
|       10839 | ('comunity', 'comunity', 'NN')   | Second, truth make our comunity be truthable sociaty.                                                | ('community', 'community', 'NN') |

- _Incorporating corrections into `pelic_df`_ : Finally, these corrected tokens are incorporated back into `pelic_df`, creating a new `tok_lem_POS` column for easy comparison to the original texts. Below is an example of an original and corrected text:

```python
>>> print(pelic_df.loc[pelic_df.text.str.contains('becuase')].iloc[1,11]) #uncorrected
[(('My', 'my', 'PRP$'), ('friend', 'friend', 'NN'), ('is', 'be', 'VBZ'), ('realy', 'realy', 'JJ'), ('nise', 'nise', 'RB'), ('guy', 'guy', 'NN'), ('.', '.', '.'), ('I', 'i', 'PRP'), ('like', 'like', 'VBP'), ('hem', 'hem', 'JJ'), ('becuase', 'becuase', 'NN'), ('he', 'he', 'PRP'), ('is', 'be', 'VBZ'), ('friendlly', 'friendlly', 'RB'), ('and', 'and', 'CC'), ('lovliy', 'lovliy', 'NN'), ('.', '.', '.'))]

>>> print(pelic_df.loc[pelic_df.text.str.contains('becuase')].iloc[1,12]) #corrected
[('My', 'PRP$'), ('friend', 'NN'), ('is', 'VBZ'), ('real', 'JJ'), ('nice', 'RB'), ('guy', 'NN'), ('.', '.'), ('I', 'PRP'), ('like', 'VBP'), ('hem', 'JJ'), ('because', 'NN'), ('he', 'PRP'), ('is', 'VBZ'), ('friendly', 'RB'), ('and', 'CC'), ('lovely', 'NN'), ('.', '.')]
```

We can see here that many approrpriate corrections have been made, including _beccuase_ -> _because_ , _nise_ -> _nice_ , _friendlly_ -> _friendly_ , and _lovily_ -> _lovely_ . Importantly, incorrect spellings that are actual words, e.g. _hem_ (should be _him_ in this case) are not corrected. In addition, as limited context is considered, there will be some inaccuracies, e.g. _realy_ (real nice is a frequent bigram) -> _real_ rather than _really_.  

Overall, the application of spelling correction is an important resource as it allows for more accurate tracking of what learners _may_ have been intending to write. For example, learners may know a word in every sense, except for its spelling. However, as with any automated text manipulation, the added layer of processing will allow for errors to enter the data, and as such, must be considered carefully when drawing conclusions from the data.

<br>

## 5. Licenses

**PELIC license:**
<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Dataset" property="dct:title" rel="dct:type">PELIC dataset</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/ELI-Data-Mining-Group/PELIC_dataset" property="cc:attributionName" rel="cc:attributionURL">Alan Juffs, Na-Rae Han, Ben Naismith</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/ELI-Data-Mining-Group/PELIC_dataset" rel="dct:source">https://github.com/ELI-Data-Mining-Group/PELIC_dataset</a>.

**SCOWL license:**
[SCOWL Copyright and License Agreement](https://www.maplesoft.com/support/help/Maple/view.aspx?path=License/SCOWL)

Spell Checking Oriented Word Lists (SCOWL) (http://wordlist.sourceforge.net/scowl-readme)
The collective work is Copyright 2000-2011 by Kevin Atkinson as well  as any of the copyrights mentioned below:

Copyright 2000-2011 by Kevin Atkinson
Permission to use, copy, modify, distribute and sell these word lists, the associated scripts, the output created from the scripts, and its documentation for any purpose is hereby granted without fee, provided that the above copyright notice appears in all copies and that both that copyright notice and this permission notice appear in supporting documentation. Kevin Atkinson makes no representations about the suitability of this array for any purpose. It is provided "as is" without express or implied warranty.

<br>

[Back to top](#PELIC-spelling)
