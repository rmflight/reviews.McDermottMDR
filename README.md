# Review

This is my review of JE McDermott et al., *Prediction of multi-drug resistance transporters using a novel sequence analysis method*,
F1000Research 2015, doi: [10.12688/f1000research.6200.1](http://dx.doi.org/10.12688/f1000research.6200.1)

## Decision

Approved with Reservations 

## Claims

The authors claim to implement a linguistic-based approach that allows the identification of functional patterns
from groups of functionally related proteins. The method uses regular-expressions that are generated using
a parse-tree that is modified via a genetic algorithm, and fitness is scored by accuracy using training data.

After application to ser-thr binding and zinc fingers, the authors train the method on multi-drug transporters
to predict possible MDR's in the genome of a high-temperature bacteria to explore the potential of finding novel MDR genes
that could result from lateral transfer.

## Reservations

### Data Availability

Not all of the code / data necessary to reproduce the results are currently provided. While acknowledging that
the primary algorithm (PILGram) is currently awaiting publication and that this is **not** the place to describe
the particulars of that software, I think there are still steps to be taken to improve the reproducibililty of **this**
publication by providing more of the data. It should be noted that when the PILGram algorithm is published, this publication
should be updted with references and links to make it easier for others to find. 

More data to include:

* Provide the actual entries from PROSITE that were used for the positive and negative examples

* Provide the actual entries for training the Zinc finger expressions

* Provide the genome accession and gene annotations from the thermophilic bacteria that was annotated

* Provide the list of accessions annotated as MDR's using MDRPred

### Other Algorithmic Details

Again I acknowledge that this is not the place to detail the full inner-workings of the PILGram
algorithm, however, most genetic algorithms have a defined chromosome length defining the solution.
I would have expected an analagous situation for PILGram, in that one would have to define the
**length** of the regular expression. This does not appear to be the case here, given the variety
of regex's noted for Zinc fingers and MDRs. As far as I can tell, this is likely due to the way that individual trees
can be recombined, but it is not clear from the text how different length regexes result.

### Dependence on Accuracy as Fitness Metric
