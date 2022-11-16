# dna-data-generator
This project aims to reproduce the method described in [[1]](#1) *DNA synthetic
sequences generation using multiple competing Markov models.* by Pratas et al. and evaluate it.


# The method
The method used in paper, which serves as base to this project is two-stage data generator utilising multiple finite-context models in order to generate
synthetic DNA data sequences. This data generator consists of two stages: firstly, creating multiple finite-context models/Markov
chains of varying orders on a given sequence, and secondly, using lowest entropy to select the best
model for any given subset of the new sequence (in this case, 100-nucleotide blocks). Pratas et al
argued that this method performs significantly better than any single Markov Chain model as it
compensates for non-stationary nature of DNA sequences.

We aim to evaluate this approach with:
1) **Information Content** -  the informativeness of a sequence as the inverse of its probability of occurrence presented as plots and processed as signal with forward-backward low-pass filter with Blackman window of size 21. Due to insufficient
details, like cut-off frequencies and scaling, the full replication of filter design used in the paper wasn’t possible.
2) **Kullback-Leibler Divergence** - measuring the difference between the probability distribution of the original sequences and
that of the corresponding synthetic sequence.
3) **Machine Learning predictive task** -  additionally, simple classification task trained on original and synthetic data from Kaggle called ”DNA Sequence Dataset” by Nagesh Singh
Chauhan [[2]](#2) which contains 4,380 human DNA sequences of unknown origin classed as one of seven
possible classes representing gene families (0: G protein coupled receptors, 1: tyrosine kinase, 2:
tyrosine phosphatase, 3: synthetase, 4: synthase, 5: ion channel, 6: transcription factor).


# The setup

Because this topic was rather experimental we provide a Jupyter notebook with our
work in order to present results alongside the code as opposed to executable script. The code was implemented in Python on Google Colab. The whole
implementation is reproducible as we included pickled sequences that were used for analysis.

# The output

Computational limitations and the fact we chose to implement this from scratch meant that
we struggled to have enough RAM to generate models of greater than order 12 against such large
datasets. Pinho et al had suggested various memory saving techniques which we implemented;
however, time constraints meant we could not fully reimplement some of these. Therefore, the full
set of competing models only had orders k = 2, 4, 6, 8, 10, 12 while the original paper also had models
of orders 14 and 16.
For the purpose of comparison of Information Content, the following sequences were generated:
- seqA: based on chromosome 1, generated using a single finite-context model of order 6, processed with word size of 5
- seqB: based on chromosome 1, generated using a three finite-context models of orders 4, 8, 12,
processed with word size of 5
- seqC: based on chromosome 1, from all 6 competing models of orders 2, 4, 6, 8, 10, 12 processed
with word size of 5
- seqE: based on chromosome Y, generated using all 6 competing models of orders 2, 4, 6, 8, 10,
12 processed with word size of 1
- seqF: based on chromosome Y, generated using all 6 competing models of orders 2, 4, 6, 8, 10,
12 processed with word size of 3
- seqG: based on chromosome Y, generated using all 6 competing models of orders 2, 4, 6, 8, 10,
12 processed with word size of 5


For the purposes of comparison of Kullback-Leibler Divergence, we generated four different types
of sequences against the full sequence of chromosome 21:
- random seq: A sequence generated purely randomly from C, G, A, and T serving as baseline
- single seq: A sequence generated from a single Markov chain of order 6
- half seq: A sequence generated from three competing models of orders 2, 6, and 10
- full seq: A sequence generated from all competing models of orders 2, 4, 6, 8, 10, 12

# Authors
This implementation was done by Alicja Karlowicz and [Benjamin Lee](https://github.com/BananaLee) for Security, Privacy and Explainability in Machine Learning project

# References
<a id="1">[1]</a>  Pratas, Diogo & Bastos, Carlos & Pinho, Armando & Neves, Ant´onio & Matos, Lu´ıs. (2011). DNA synthetic
sequences generation using multiple competing Markov models. IEEE Workshop on Statistical Signal Processing
Proceedings. 133-136. 10.1109/SSP.2011.5967639.

<a id="2">[2]</a>  Nagesh Singh Chauhan. DNA sequence dataset https://www.kaggle.com/datasets/nageshsingh/dna-sequence-dataset
