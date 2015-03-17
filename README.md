# Review

This is my review of JE McDermott et al., *Prediction of multi-drug resistance transporters using a novel sequence analysis method*,
F1000Research 2015, doi: [10.12688/f1000research.6200.1](http://dx.doi.org/10.12688/f1000research.6200.1)

## Decision

Approved with Reservations 

## Claims

* Implement a linguistic-based approach that allows the identification of functional patterns
from groups of functionally related proteins

* The method uses regular-expressions that are generated using a parse-tree that is modified
via a genetic algorithm, and fitness is scored by accuracy using training data.

* Able to find discriminative patterns for serine-threonine phosphatases, zinc fingers, and multi-drug resistance (MDR) transporters

* Predict MDR transporters in a newly sequenced hyperthermophile bacteria as a potential pool for novel MDR transporters
that could be transferred to current bacteria as novel source of antibiotic resistance

* PILGram is able to identify and separate based on the binding region responsible for substrate specificity

## Praises

From this version of the manuscript (v1), the claims are justified. Regular expressions are a linguistic construct,
the authors are able to reproduce previously defined regexes without prior alignment using the PILGram
method, and classify zinc fingers and MDRs by counting the number of regexes matching a particular
sequence, resulting in the MDRPred method. This method, MDRPred was then applied to a newly sequenced 
bacterium and possibly novel MDR transporters identified.

Although I think the general claims can be justified from the text, there are some areas of concern
that I think should be addressed. 

These reservations fall under these major areas:

* data availability for reproducibility
  * actual id's for positive and negative examples

* lack of description in the text leading to either lack of clarity or possible misunderstandings
  * length of generated reg-exes
  * description of reg-exes in general
  * justification of PP-PRE and TMR-PRE extensions to PRE, as well as match and score generation, 

* weak evidence supporting a particular claim
  * substrate specificity
  
Each of these reservations are further detailed below.

## Reservations

### Data Availability

Not all of the code / data necessary to reproduce the results are currently provided. While acknowledging that
the primary algorithm (PILGram) is currently awaiting publication and that this is **not** the place to describe
the particulars of that software, I think there are still steps to be taken to improve the reproducibililty of **this**
publication by providing more of the data. It should be noted that when the PILGram algorithm is published, this publication
should be updated with references and links to make it easier for others to find. 

More data that should be included:

* Provide the actual entries from UniProt that were used for the positive and negative examples

* Provide the actual entries from UniProt for training the Zinc finger expressions

* Provide the genome accession and gene annotations from the thermoplastic bacteria that was annotated

* Provide the list of accessions annotated as MDR's using MDRPred

* Date of download of PROSITE data. prosite.dat on Mar 17, 2015 shows 198 positive matches for PS00125, and I'm
assuming 2018 (hard to tell from file) positive matches for PS00028.

### Lack of Description

#### PILGram Algorithmic Details

Again I acknowledge that this is not the place to detail the full inner-workings of the PILGram
algorithm, and the example in the text for BMI is useful. However, most genetic algorithms have a 
defined chromosome length defining the solution. 
I would have expected an analogous situation for PILGram, in that one would have to define the
**length** of the regular expression. This does not appear to be the case here, given the variety
of reg-ex's noted for Zinc fingers and MDRs. As far as I can tell, this is likely due to the way that individual trees
can be recombined, but it is not clear from the text how different length reg-exes result.

#### Describing REGEXE's

I use regular expressions regularly, but even still I found it difficult to follow the regular expressions
listed in the text without looking to a reference. A short description, even in the supplemental
materials of general features of the reg-exes would be useful. For example, the fact
that [ABC] means one of either A or B or C at that position, that {3, 8} means either
3 or 8 letters between the previous and the next thing, and that [^ABC] means none
of either A or B or C.

Further, having examples of what portion of a sequence is matched, especially
for the serine-threonine case where the sequence interval in general overlaps
between the PROSITE pattern and the PILGram derived pattern. But also having examples
for the Zinc finger showing the attributes shown, or describing what part of the regex
encodes which features would help a lot.

#### Physichemical Properties and TMR

I think I understand why the physiochemical properties (PP) and transmembrane region (TMR)
score were included for the MDRPred,
however there is currently no discussion of their inclusion or justification in the text.
From the current description of them, it is also difficult to imagine how something
matches the PP-PRE and TMR-PRE, including the PP and TMR scores as part of the match.
Therefore I recommend:

* Having a better description of the PP and TMR scores

* Justification for their inclusion in MDRPred. I am guessing that the accuracy drops
precipitously without them, but there is nothing in the text currently describing why they
are needed.

* Giving examples of how some PPs are different for different AAs

* Example of calculation of PP score and TMR score for a regex match

* Example of full match for a derived PP-PRE or TMR-PRE


