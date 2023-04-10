# SLUICE

This repository contains the corpus SLUICE (SPARQL for Learning and Understanding Interrupted Customer Enquiries). SLUICE contains 21,000 artificially interrupted questions with their underspecified SPARQL queries. This was originally created for a [paper published at CUI 2023]().

The paper (by [Angus Addlesee](http://addlesee.co.uk/), and Marco Damonte) can be found [here]() and is titled: "Understanding and Answering Incomplete Questions".

If you use this repository in your work - please cite us:

Harvard:
```
Addlesee, A. and Damonte, M., 2023. Understanding and Answering Incomplete Questions. CUI 2023.
```

BibTeX:
```
@inproceedings{addlesee2023understanding,
  title={Understanding and Answering Incomplete Questions},
  author={Addlesee, Angus and Damonte, Marco},
  journal={CUI 2023},
  year={2023}
}
```

## Structure of corpus

In the corpus directory, you will find the corpus train and test set. Each instance in the SLUICE corpus contains the chopped question with the underspecfied SPARQL query, the original question with the full SPARQL query, and the metadata from the chopping (NER tag, chopped entity name, and chopped entity Wikidata ID).

The metadata directory contains variations of the corpus discussed in the paper that were ultimately rejected.

## Chopping Guide

Coming soon...

