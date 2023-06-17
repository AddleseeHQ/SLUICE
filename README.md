# SLUICE

This repository contains the corpus SLUICE (SPARQL for Learning and Understanding Interrupted Customer Enquiries). SLUICE contains 21,000 artificially interrupted questions with their underspecified SPARQL queries. This was originally created for a [paper published at CUI 2023]().

The paper (by [Angus Addlesee](http://addlesee.co.uk/) and Marco Damonte) can be found [here](https://www.amazon.science/publications/understanding-and-answering-incomplete-questions) and is titled: "Understanding and Answering Incomplete Questions".

If you use this repository in your work - please cite us:

Harvard:
```
Addlesee, A. and Damonte, M., 2023. Understanding and Answering Incomplete Questions. Proceedings of the 5th Conference on Conversational User Interfaces (CUI).
```

BibTeX:
```
@inproceedings{addlesee2023understanding,
  title={Understanding and Answering Incomplete Questions},
  author={Addlesee, Angus and Damonte, Marco},
  booktitle={Proceedings of the 5th Conference on Conversational User Interfaces (CUI)},
  year={2023}
}
```

## Structure of corpus

In the corpus directory, you will find the corpus train and test set. Each instance in the SLUICE corpus contains the chopped question with the underspecfied SPARQL query, the original question with the full SPARQL query, and the metadata from the chopping (NER tag, chopped entity name, and chopped entity Wikidata ID).

The metadata directory contains variations of the corpus discussed in the paper that were ultimately rejected.

## Chopping Guide

This work used SPARQL, a query language that is executed over RDF knowledge graphs. We published a follow-up paper to this one (using AMR) at Interspeech called: "Understanding Disrupted Sentences Using Underspecified Abstract Meaning Representation" that can be found [here](https://www.amazon.science/publications/understanding-disrupted-sentences-using-underspecified-abstract-meaning-representation)

In order to create similar corpora, you need to follow these general steps:

1. We need some graph representation, like RDF or AMR, and a corpus of sentences paired with their graph meaning representations.
2. There must be some way to align the text's words to the parts of the graph that those words contribute. Here is Figure 1 from [our AMR paper](https://www.amazon.science/publications/understanding-disrupted-sentences-using-underspecified-abstract-meaning-representation).
[image of an AMR graph colour coded with its corresponding sentence](./amr-alignment.png)
3. With the RDF in our SPARQL queries, we used the nodes textual labels to fuzzy match with words in the sentence (matching "Beyonce" and "Beyoncé" for example). Otherwise, you can use the output of alignment models - the output of which is shown in the above image.
4. Once a match is found, we then remove the matching text from the question or sentence, and then underspecify the graph MRL by deleting the nodes and edges that the removed text provided.
5. The removed content should be replaced with some UNKNOWN tag or variable (we used the ?unknown variable in RDF).
6. The removed text and replaced graph content can be now be paired to represent the completion turn. For example, "Europe" and it's graph content in RDF.
7. You now have a collection of incomplete questions and their underspecified MRL's, with their corresponding completions (and MRL of the completion).
8. The new task is to parse the incomplete question, and then parse the completion with your semantic parser. The (hopefully) generated UNKNOWN tag must then be replaced by the completion parse to conjoin the representations. The resulting parse is correct if the UNKNOWN tag was in the correct location in the MRL structure. Obviously both parses also have to be correct to accurately reconstruct the original questions meaning.
9. This can be done with basically any graph MRL corpus, and evaluation results should be compared to the original tasks SotA system when given the full original question or sentence (as this is the upper bound). So in the SLUICE corpus, the primary evaluation metric is the correct answer rate. In [the AMR paper](https://www.amazon.science/publications/understanding-disrupted-sentences-using-underspecified-abstract-meaning-representation), it is Smatch.

