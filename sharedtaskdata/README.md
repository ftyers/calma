# Shared Task on Related Language Morphological Analysis

## Data Formats

### Uncovered data

We provide fully annotated training and development sets for the
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

We also provide covered data sets which are used as input data for
the analysis system during development and testing. Here each word
form occurs exactly once and the lemma, POS and morphological features
fields are empty. This is an example from `dev/ast-uncovered`

```
ast	otomana	_	_	_
ast	franxes	_	_	_
ast	amosaben	_	_	_
ast	principiu	_	_	_
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

## Tracks

There three different tracks with varying degrees of supervision.

**Track 1** is a traditional supervised learning scenario. Competitors
get annotated data from the target languages and learn a model which
can analyze unseen target language word forms.

**Track 2** provides additional supervision in form of related
language data. Competitors get annotated data both for the target
language and related languages. They then learn a model which can
analyze unseen target language forms.

**Track 3** does not provide any target language
supervision. Competitors get no annotated target language
data. Instead they get annotated data from related languages and learn
a model which can analyze unseen target language forms.

## Language codes

### Germanic Languages

TBD

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
