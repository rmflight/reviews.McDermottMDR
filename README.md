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
  * actual MDRPred code

* lack of description in the text leading to either lack of clarity or possible misunderstandings
  * length of generated reg-exes
  * description of reg-exes in general
  * justification of PP-PRE and TMR-PRE extensions to PRE, as well as match and score generation
  * elaboration of clustering, maybe adding to methods
  * supplemental table 1 needs **more** description

* language implying other methods are not "linguistic"

* Weak "substrate specificity" claim
  
Each of these reservations are further detailed below.

## Reservations

### Data & Code Availability

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

* Lack of code: Finally, beyond the models provided in Supplemental Table 1, there is no actual code
provided to actually create matches to either the training sequences or the thermophilic
bacteria, or any sequence of interest. I understand not providing PILGram code and application, however this publication
is about a "method", and I am surprised the "method" is not available as something that
can be run by the reader of the paper. This is also disconcerting given that the
details of calculating matches to PP-PRE's and TMR-PRE's is not very clear.

### Lack of Description

#### PILGram Algorithmic Details

Again I acknowledge that this is not the place to detail the full inner-workings of the PILGram
algorithm, and the example in the text for BMI is useful. However, most genetic algorithms have a 
defined chromosome length defining the solution. 
I would have expected an analogous situation for PILGram, in that one would have to define the
**length** of the regular expression. This does not appear to be the case here, given the variety
of reg-ex's noted for Zinc fingers and MDRs. As far as I can tell, this is likely due to the way that individual trees
can be recombined, but it is not clear from the text how different length reg-exes result.
Clarification of how different length regexes result would be useful.

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

#### Physiochemical Properties and TMR

I think I understand why the physiochemical properties (PP) and transmembrane region (TMR)
score were included for the MDRPred,
however there is currently no discussion of their inclusion or justification in the text.
From the current description of them, it is also difficult to imagine how something
matches the PP-PRE and TMR-PRE, including the PP and TMR scores as part of the match.
Therefore I recommend:

* Having a better description of the PP and TMR scores in Methods

* Justification for the inclusion of PP-PRE and TMR-PRE in MDRPred. Currently the only
justification is "Because we believed ...". I would hazard a guess that the accuracy drops
precipitously without them, but there is nothing in the text currently describing why they
are needed.

* Giving examples of how some PPs are different for different AAs

* Example of calculation of PP score and TMR score for a regex match

* Example of full match for a derived PP-PRE or TMR-PRE

#### Elaboration of clustering

In the "Results", "Functional motifs identified", a description of clustering the 
generated models is provided. The current
description is ambiguous. I think what was done was a vector of length 71 
(corresponding to the number of training sequences) was generated for each model,
with a 1 indicating a match to the model, and 0 indicating no match to the model.
These 36 vectors (one for each model) were subsequently clustered using hierarchical clustering. 

No description of what distance metric was used to calculate the distance between the 
model vectors, nor which hierachical clustering method was used is provided. 
In the R stats package, there are: two variations of Ward's minimum variance method, the complete
linkage method, the single linkage method, median, and centroid. The software, version,
and algorithm reference should be provided for completeness.

#### Supplemental Table 1

I believe supplemental table 1 could benefit from including:

* a description of what each column is beyond the title (for example, what is 
the difference between RESmall and RE??)

* a description of the PP that are included (it appears there are only 11
that end up being used)

* an indication of which are PRE, PP-PRE, and TMR-PRE

### Language implying other methods are not linguistic

In its current form, the abstract reads:

"In this paper we describe a linguistic approach to identify ..."

This implies that regular expressions in PROSITE and hidden markov models are not
"linguistic" approaches. However, in the text, describing regular expressions used
by PROSITE as the simplest form of grammar (regular grammars), and Hidden Markov models
as a type of regular grammar (Introduction, paragraph 3). If these are grammars,
then they are linguistic approaches. 

In fact, from the description in the manuscript, PILGram generates regular expressions
that in some cases are very similar to those used by PROSITE. I am unclear as to how
generating regular expressions using PILGram is a "linguistic" approach, but aligning
and finding common features (as in PROSITE or HMMs) is not. 

I understand that PILGram is able to generate discriminative reg-exes without alignment
first, and that is very useful (as exemplified by this manuscript), but from the current
description that does not make it "linguistic". 

### Weak "substrate specificity" claim

This is mentioned in the abstract, and 2 times in the introduction. The wording
in the abstract implies that the method is able to delineate substrate specificity,
i.e. that the method can generate regexes that are specific for different substrates.
However, the one result implies rather that the regexes identify the region responsible
for substrate specificity. These seem to be two different things in my mind, and
I think either the claim in the abstract and introduction should be dropped or clarified,
especially given that there is only one example provided.
Finally, the claim is weakened in the current text because the word **substrate** is
missing from the paragraph discussing the evidence for substrate specificity (Results, 
Drug reistance transporters, Functional motifs identified, last paragraph in that section,
no mention of "substrate", just specificity).

## Other Simple Improvements to Text

**Results**, "Functional motifs identified", last paragraph, there is 

**Methods**, under PILGram, first sentence, a reference is missing to SIEVE.

**Methods**, PILGram example, example grammar, spaces around symbols would greatly 
improve the readability

In **results**, actually identify the **core** of the PROSITE reg-ex that PILGram
is able to capture, noting that PILGram drops the first and last AA in the PROSITE
one, and adds **Q** to the set of alternatives compared to PROSITE.

**Results** paragraph 2 says "Supplemental Table 1", but I believe this should be
"Supplemental Figure 1".
