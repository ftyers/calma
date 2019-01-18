# Shared Task on Cross-Lingual Morphological Analysis

We introduce the task of cross-lingual morphological analysis. Given a word in an unknown related language, for example "navifraghju" ("shipwreck" in Corsican), a human speaker of several related languages is able to deduce that it is a noun in the singular by making deductions from similar words, for example: "naufragi" (Catalan), "naufragio" (Spanish, Italian), "naufrágio" (Portuguese) and "naufrage" (French). In this task we invite participants to create computational models which will be able to do the same. Two language families are represented, Romance (fusional morphology) and Turkic  (agglutinative morphology). 

## Tracks

There are two different tracks with different degrees of supervision.

**Track 1** is a traditional supervised learning scenario. Competitors
get annotated data from the target languages and learn a model which
can analyze unseen target language word forms. In addition,
competitors are allowed to use the input forms in the test set when training their systems.

**Track 2** does not provide any annotated target language
data. Instead competitors get annotated data from related languages and learn
a model which can analyze unseen target language forms. In addition,
competitors are allowed to use the input forms in the test set when training their systems.

## Timeline

* Training set release: February 5, 2019
* Test set release: March 5, 2019
* Submissions due: March 8, 2019
* Results announced: March 12, 2019

On February 5, we release trining sets for Romance languages (Asturian, Catalan, French, Italian, Portuguese, Spanish) and Turkic languages (Bashkir, Crimean Tatar, Kazakh, Kyrgyz, Tatar, Turkish). On March 5, we relase additional training and test sets for two surprise languages. Competitors then train systems on the target language training sets for track 1 and on the related language training sets for track 2 and submit their annotated test sets. We will be evaluating system performance on the surprise languages.   

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


### Turkic Languages

| Code | Language      |
|------|---------------|
| bak  | Bashkir       |
| crh  | Crimean Tatar |
| kaz  | Kazakh        |
| kir  | Kyrgyz        |
| tat  | Tatar         |
| tur  | Turkish       |  

### Baseline Results for Development Data

```
python3 scripts/eval_tabular.py results/ast-track1-dev-covered.sys dev/ast-uncovered

Recall for analysis: 77.28
Precision for analysis: 70.34
F1-score for analysis: 73.65

Recall for lemma: 87.10
Precision for lemma: 79.39
F1-score for lemma: 83.07

Recall for tag: 80.65
Precision for tag: 75.62
F1-score for tag: 78.05

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


python3 scripts/eval_tabular.py results/crh-track1-dev-covered.sys dev/crh-uncovered

Recall for analysis: 90.32
Precision for analysis: 81.32
F1-score for analysis: 85.58

Recall for lemma: 95.52
Precision for lemma: 89.45
F1-score for lemma: 92.39

Recall for tag: 91.21
Precision for tag: 83.71
F1-score for tag: 87.30


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

### Baseline Results for Test Data

```
python3 scripts/eval_tabular.py results/ast-track1-test-covered.sys test/ast-uncovered

Recall for analysis: 75.05
Precision for analysis: 69.30
F1-score for analysis: 72.06

Recall for lemma: 85.30
Precision for lemma: 78.15
F1-score for lemma: 81.57

Recall for tag: 78.44
Precision for tag: 74.87
F1-score for tag: 76.61

python3 scripts/eval_tabular.py results/ast-track2-test-covered.sys test/ast-uncovered

Recall for analysis: 44.35
Precision for analysis: 44.41
F1-score for analysis: 44.38

Recall for lemma: 61.88
Precision for lemma: 57.96
F1-score for lemma: 59.86

Recall for tag: 61.44
Precision for tag: 63.68
F1-score for tag: 62.54


python3 scripts/eval_tabular.py results/crh-track1-test-covered.sys test/crh-uncovered

Recall for analysis: 91.60
Precision for analysis: 82.04
F1-score for analysis: 86.56

Recall for lemma: 96.63
Precision for lemma: 89.71
F1-score for lemma: 93.04

Recall for tag: 92.40
Precision for tag: 84.25
F1-score for tag: 88.14


python3 scripts/eval_tabular.py results/crh-track2-test-covered.sys test/crh-uncovered

Recall for analysis: 30.53
Precision for analysis: 36.74
F1-score for analysis: 33.35

Recall for lemma: 56.55
Precision for lemma: 58.76
F1-score for lemma: 57.63

Recall for tag: 38.23
Precision for tag: 45.85
F1-score for tag: 41.69
```
