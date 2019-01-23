# Shared Task on Cross-Lingual Morphological Analysis

We introduce the task of cross-lingual morphological analysis. Given a word in an unknown related language, for example "navifraghju" ("shipwreck" in Corsican), a human speaker of several related languages is able to deduce that it is a noun in the singular by making deductions from similar words, for example: "naufragi" (Catalan), "naufragio" (Spanish, Italian), "naufrágio" (Portuguese) and "naufrage" (French). In this task we invite participants to create computational models which will be able to do the same. Two language families are represented, Romance (fusional morphology) and Turkic  (agglutinative morphology). 

## Tracks

We present two tracks: a closed track and an open one.

**Track 1** Competitors get annotated data from related languages and learn
a model which can analyze unseen target language forms. In addition,
competitors are allowed to use the input forms in the test set when training their system.

**Track 2** Competitors get annotated data from related languages as well as an unannotated plain text corpus in the target language. They learn
a model which can analyze unseen target language forms. In addition,
competitors are allowed to use the input forms in the test set when training their system.

We encourage participants to provide thorough error analysis.

## Timeline

* Training set release: February 5, 2019
* Test set release: March 5, 2019
* Submissions due: March 8, 2019
* Results announced: March 12, 2019

On February 5, we release training sets for Romance languages (Catalan, French, Italian, Portuguese, Spanish) and Turkic languages (Bashkir, Kazakh, Kyrgyz, Tatar, Turkish). We also release development sets for the Romance language Asturian and the Turkic language Crimean Tatar. In addition, we release unannotated corpora for Asturian and Crimean Tatar.

On March 5, we relase additional test sets for two surprise languages. Additionally, we release unannotated corpora for both of the surprise languages. Competitors then train systems on the related language training sets for track 1 and the related language training set and unannotated data for track 2. They then submit their test set predictions. We will be evaluating system performance on the surprise language test sets.   

## Data Formats

### Uncovered data

We provide fully annotated _uncovered_ training and development sets for the
target language and related languages. Below, you can see an example
of the data format from `train/ast-track2-uncovered`:

```
por    marido      marido      NOUN    Gender=Masc|Number=Sing
por    dependem    depender    VERB    Mood=Ind|Number=Plur|Person=3|Tense=Pres|VerbForm=Fin
cat    carener     carener     ADJ     Gender=Masc|Number=Sing
cat    carener     carener     NOUN    Gender=Masc|Number=Sing
spa    depender    depender    VERB    VerbForm=Inf
ast    adoptó      adoptar     VERB    Aspect=Perf|Mood=Ind|Number=Sing|Person=3|Tense=Past|VerbForm=Fin
ast    roques      roca        NOUN    Gender=Fem|Number=Plur
```

Each line consists of five TAB separated fields (language code, word
form, lemma, POS, morphological features). Since every word form can
correspond to multiple analyses, a word form like "carener" can occur
on several lines with different POS and morphological features.

### Covered data

We also provide _covered_ data sets which are used as input data for
the analysis system during development and testing. Here each word
form occurs exactly once and the lemma, POS and morphological features
fields are empty. This is an example from `dev/ast-uncovered`

```
ast	otomana      _    _    _
ast	franxes      _    _    _
ast	amosaben     _    _    _
ast	principiu    _    _    _
```

When your system fills in analyses, you should output one line for
each analysis (the order of the output lines will not affect the
evaluation script). For example, these are the corresponding lines
from the file `dev/ast-uncovered`

```
ast    otomana      otomán       ADJ     Gender=Fem|Number=Sing
ast    otomana      otomanu      NOUN    Gender=Fem|Number=Sing
ast    otomana      otomanu      ADJ     Gender=Fem|Number=Sing
ast    franxes      franxa       NOUN    Gender=Fem|Number=Plur
ast    amosaben     amosar       VERB    Aspect=Imp|Mood=Ind|Number=Plur|Person=3|Tense=Past|VerbForm=Fin
ast    principiu    principiu    NOUN    Gender=Masc|Number=Sing
```

## Language codes

### Romance Languages

| Code | Language      |
|------|---------------|
| ast  | Asturian      |
| cat  | Catalan       |
| fra  | French        |
| ita  | Italian       |
| por  | Portuguese    |
| spa  | Spanish       |
| ???  | Surprise Language |

### Turkic Languages

| Code | Language      |
|------|---------------|
| bak  | Bashkir       |
| crh  | Crimean Tatar |
| kaz  | Kazakh        |
| kir  | Kyrgyz        |
| tat  | Tatar         |
| tur  | Turkish       | 
| ???  | Surprise Language |

### Baseline Results for Development Data

These are basline results for track 1 on the Asturian and Crimean Tatar development data

```

python3 scripts/eval_tabular.py results/ast-track2-dev-covered.sys dev/ast-uncovered

Recall for analysis: 43.87
Precision for analysis: 45.30
F1-score for analysis: 44.58

Recall for lemma: 61.66
Precision for lemma: 58.70
F1-score for lemma: 60.15

Recall for tag: 59.57
Precision for tag: 62.84
F1-score for tag: 61.16



python3 scripts/eval_tabular.py results/crh-track2-dev-covered.sys dev/crh-uncovered

Recall for analysis: 31.24
Precision for analysis: 38.44
F1-score for analysis: 34.47

Recall for lemma: 57.54
Precision for lemma: 60.36
F1-score for lemma: 58.92

Recall for tag: 38.19
Precision for tag: 46.95
F1-score for tag: 42.12
```
