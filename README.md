# Review

This is my review of JE McDermott et al., *Prediction of multi-drug resistance transporters using a novel sequence analysis method*,
F1000Research 2015, doi: [10.12688/f1000research.6200.1](http://dx.doi.org/10.12688/f1000research.6200.1)

## Decision

Approved with Reservations 

## Claims

The authors claim to implement a linguistic-based approach that allows the identification of functional patterns
from groups of functionally related proteins. The method uses regular-expressions that are generated using
a parse-tree that is modified via a genetic algorithm, and fitness is scored by accuracy using training data.

After application to ser-thr binding and zinc fingers, the authors apply the method to multi-drug transporters
and the genome of a high-temperature bacteria to explore the potential of finding novel MDR genes
that could result from lateral transfer.

## Reservations

### Data Availability

Not all of the code / data necessary to reproduce the results are currently provided. While acknowledging that
the primary algorithm (PILGram) is currently awaiting publication, it is not appar there are still steps that could be taken
to providing more of the data. It should be noted that when the PILGram algorithm is published, this publication
should be updted with references and links to make it easier for others to find. 

Ways to enhance the reproducibility:

* Provide the actual entries from PROSITE that were used for the positive and negative examples

* Provide the actual entries for training the Zinc finger expressions

* Provide the genome accession and gene annotations from the thermophilic bacteria that was annotated

* Provide the list of accessions annotated as MDR's using MDRPred
