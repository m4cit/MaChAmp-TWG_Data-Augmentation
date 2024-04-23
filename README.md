# MaChAmp-TWG_Data-Augmentation
Data Augmentation scripts for the parser MaChAmp-TWG as part of my bachelor thesis.


## Scripts
**1_unimorph_to_conllu.py**:
>Translates the original UniMorph file into the language / format of the CoNLLU file.

**2_improveUnimorph.py**:
>Looks up all verbs from the UniMorph file successively on dictionary.com, and categorizes them into 'transitive' and 'intransitive' (Very slow. Better to use a dictionary API if available.).

**3_improveRRG.py**:
>Checks and adds the transitivity of all verbs to the RRG CoNLLU file.

**4_filterForTrain.py**:
>Filters out all unused words / lines in the RRG CoNLLU file.

**generate.py**:
>Replaces words in the RRG CoNLLU file with randomly chosen ones from the UniMorph file.

**augment.py**:
>Replaces original words in the training file with random ones generated by the module 'generate.py', followed by the augmentation of the training file with new sentences.


## Requirements
- Python 3.6 or newer
- modules from the requirements.txt file


## Installation

1. ```
   pip install -r requirements.txt
   ```
3. Place all files and folders into the main directory of MaChAmp-TWG.


## Options
**-h, --help**  

**--unimorph0:**
>UniMorph Inaccurate verb replacements with regard to transitivity. In place of --unimorph1, --internal, --supertag, or --original.

**--unimorph1:**
>UniMorph Accurate verb replacements with regard to transitivity. In place of --unimorph0, --internal, --supertag, or --original.

**--internal:**
>For internal word swapping. In place of --unimorph0, unimorph1, --supertag, or --original.

**--supertag:**
>For internal supertag word swapping. In place of --unimorph0, unimorph1, --internal, or --original.

**--original:**
>Appends the training data by itself without changes. In place of --unimorph0, unimorph1, --internal, or --supertag. 

**-i, --RRGinput:**
>(OPTIONAL) Filtered RRG file input. Default file: "rrgparbank/conllu/filtered_acc_en_conllu.conllu".

**-o, --RRGoutput:**
>(OPTIONAL) Filtered RRG file output directory. Default directory: "rrgparbank/conllu".

**-t, --tag:**
>Word tags.

**-ti, --trainInput:**
>(OPTIONAL) train.supertags file input. Default file: "experiments/rrgparbank-en/base/train.supertags".

**-to, --trainOutput:**
>(OPTIONAL) train.supertags file output directory. If the directory is not specified, the default directory is used and filename changes to "new_train.supertags".

**-s, --extensionSize:**
>Extension size of the resulting training file. Must be >= 2. "2" doubles the size (sentences) of the base training file, thus does 1 run through the file (-s input-1).


### Available tags for replacement task (not for --supertag)
>**nS:**  Noun Singular
**nP:**  Noun Plural
>
>**aPoss:**  Adjective Possessive
>**aCmpr:**  Adjective Comparative
>**aSup:**  Adjective Superlative
>**vPst:**  Verb Past Tense
>**vPresPart:**  Verb Present Tense, Participle Form
>**vPstPart:**  Verb Past Tense, Participle Form
>
>**adv (for internal dataswap only):**  Adverb
>**advInt (for internal dataswap only):**  Adverb, Pronominal type: Interrogative
>**advSup (for internal dataswap only):**  Adverb Superlative
>**advCmpr (for internal dataswap only):**  Adverb Comparative
>
>**noun:**  All nouns
>**adj:**  All adjectives
>**verb:**  All verbs
>**all:**  All available tags


## Usage
augment.py [-h] [--unimorph0] [--unimorph1] [--internal] [--supertag] [--original]  
[-i RRGINPUT] [-o RRGOUTPUT] [-t TAG] [-ti TRAININPUT] [-to TRAINOUTPUT] -s EXTENSIONSIZE

**Example 1:**  
```
python augment.py --unimorph0 -t all -s 2
```

**Example 2:**  
```
python augment.py --supertag -s 10
```


## Sources
Tatiana Bladier, Kilian Evang, Valeria Generalova, Zahra Ghane, Laura Kallmeyer, Robin Möllemann, Natalia Moors, Rainer Osswald, and Simon Petitjean. 2022. RRGparbank: A Parallel Role and Reference Grammar Treebank. In _Proceedings of the Thirteenth Language Resources and Evaluation Conference_, pages 4833–4841, Marseille, France. European Language Resources Association.  

Kilian Evang, Tatiana Bladier, Laura Kallmeyer, and Simon Petitjean. 2021. Bootstrapping Role and Reference Grammar Treebanks via Universal Dependencies. In _Proceedings of the Fifth Workshop on Universal Dependencies (UDW, SyntaxFest 2021)_, pages 30–48, Sofia, Bulgaria. Association for Computational Linguistics.  

Tatiana Bladier, Jakub Waszczuk, and Laura Kallmeyer. 2020. Statistical Parsing of Tree Wrapping Grammars. In _Proceedings of the 28th International Conference on Computational Linguistics_, pages 6759–6766, Barcelona, Spain (Online). International Committee on Computational Linguistics.  

Kallmeyer, L., Osswald, R., Van Valin, R.D. 2013. Tree Wrapping for Role and Reference Grammar. In: Morrill, G., Nederhof, MJ. (eds) Formal Grammar. FG FG 2013 2012. Lecture Notes in Computer Science, vol 8036. Springer, Berlin, Heidelberg.  

[UniMorph](https://unimorph.github.io/)
