## Genomes from metagenomes have similar phylogenetic behavior compared with isolate genomes

![histogram comparison](https://github.com/alexcritschristoph/mag-isolate-comparison/raw/master/fig.png)


To run this notebook, you'll want to download the files:
`bac120_metadata_r89.tsv`
`bac120_msa_individual_genes_r89.tar.gz`

from the GTDB server:
https://data.ace.uq.edu.au/public/gtdb/data/releases/release89/89.0/


Recently a BioRxiv preprint entitled "Anomalous phylogenetic behavior of ribosomal proteins in metagenome assembled genomes" reported a seemingly straight-forward analysis. They picked sets of 30 isolate microbial genomes and sets of 30 genomes assembled from metagenomes, and created phylogenetic trees for each set using each single copy gene. They then compared the differences between all of the SGC trees created for each set, and found that trees of genomes from metagenomes consistently were more different than trees of isolate genomes. Please note that they observe the pattern for *all metagenome assembled genomes they test, not just specific novel clades* - this is a point of confusion that is not made very clear by the preprint itself. 

They use this finding to make two claims, which can most charitably be summarized as:

>1. The methodology behind assembling and binning genomes from metagenomes is flawed.
>
>2. Specific novel lineages* described entirely by genomes from metagenomes are therefore not real.
>
>*Candidate Phyla Radiation (CPR) and ASGARD Archaea

### **There are multiple reasons why both of these claims were likely to be false:**

1. Isolates exist for [a member of the CPR](https://www.pnas.org/content/112/1/244.short) and more recently, [ASGARD Archaea](https://www.biorxiv.org/content/10.1101/726976v1).

2. [Dozens (hundreds?) of single cell amplified genomes](https://www.nature.com/articles/s41564-017-0098-y) exist for the Candidate Phyla Radiation. 

3. Dozens of [completed metagenome assembled genomes](https://www.nature.com/articles/nature14486) exist for the CPR. These are genomes that assembled in a single contig directly from a metagenome. (there are 45 such CPR genomes currently listed in GTDB).

4. [Previous direct comparisons](https://microbiomejournal.biomedcentral.com/articles/10.1186/s40168-018-0550-0) of single cell genomes and metagenome assembled genomes have shown good parity. 

5. The methods behind metagenomic assembly and binning [have been tested and validated on mock datasets](https://www.nature.com/articles/nmeth.4458).

6. [Pan-genomic analysis](https://www.biorxiv.org/content/10.1101/335083v1) of all proteins from CPR genomes has shown them to be distinct from the rest of bacteria and to broadly recapitulate their phylogenetic placement.

And the list goes on. (If you have a special addition, open a pull request!) There are many more anecdotal reasons, such as how the proposed issue could make it still possible for dozens of research labs to consistently assemble similar genomes with similar phylogeny and metabolism from multiple environments across the world, and how the same methods could reliably recapitulate genomes of known microbes [from the human microbiome](https://www.nature.com/articles/s41586-019-1058-x), and so on.

However, it is also important to address the analysis that was performed. Here, I replicate the analysis using genomes from a standardized bacterial taxonomy (GTDB) and find a similar effect as the authors originally observed. There are then two hypotheses that can be tested:

>A. The effect observed is due to poor quality and contamination due to inaccurate binning in metagenomes assembled genomes.
>
>B. The effect observed is due to differences in the phylogenetic distribution of genomes from metagenomes vs isolate genomes. 

**Here, I conduct a reproducible analysis that shows (B) entirely explains the differences observed. The phylogenetic 'anomaly' observed is entirely a function of the differences in phylogenetic distributions of metagenome assembled genomes and isolate genomes, and when controlled for, this effect disappears and metagenome assembled genomes have similar results to isolate genomes.**

Briefly: Two tests are conducted. 

In the first, high quality (<10 contigs, where most if not all SCGs will be assembled on the same contig) genomes from metagenomes are compared against isolate genomes using the same analysis, and it is found that their tree incongruence does not change at all, making it unlikely that genome quality has anything to do with the difference.

In the second, genomes from metagenomes are **matched one-to-one** with isolate genomes from either the same genus or the same order. With this, we have effectively controlled for differences in phylogenetic distribution between the isolate and genomes from metagenomes sets: this way, it is possible to **directly test the ability of metagenome assembly and binning to recapitulate genomes with normal phylogenetic behavior as fairly as possible**. In both controlled comparisons, we observe that the distributions of tree congruence for genomes from metagenomes is similar to that of isolate genomes.

Most importantly, please note the difference between the two distributions in the second test: the difference between the two for isolate genomes as well as genomes from metagenomes is much larger than any difference observed between isolate genomes and genomes from metagenomes in the original test. **Just by limiting selection to 1 genome per order instead of 1 genome per genus, we have dramatically changed the distribution of tree congruence**. In other words, it appears as though more deep branching, singleton lineages without close relatives are more difficult to accurately resolve - and we know that genomes assembled from metagenomes are far more likely to include these lineages.
