# **Phylogenomics**


We will work with the orthogroups you have identified last week.
We will select subsets of them and obtain phylogenies for each of the sets to compare how the results and resolution of the analysis changes with the data that is used. 


## Data set selection and extraction of specific orthogroups

jeje


## Prepare alignments for the different sets

### A. Installing the required software

Since you are working on CHEOPS1, you can use packages that are available there. 
`module load mafft/7.471`

When working on a personal computer or elsewhere were the package isn't available you can install it. 

1. Using conda

```
conda create -n mafft
conda activate mafft
conda install -c bioconda mafft
```

2. Or downloading and following the instricution according to your OS: https://mafft.cbrc.jp/alignment/software/

### B. Implementing the commands

*MAFFT*: https://mafft.cbrc.jp/alignment/software/

`mafft -h`

`mafft --auto in > out`

Note: alignments need to be trimmed to remove poorly aligned regions that could yield inproper results.

```
conda create -n trimal
conda activate trimal
conda install -c bioconda trimal
```

(alternatively check: https://github.com/inab/trimal)

*TRIMAL*: http://trimal.cgenomics.org/getting_started_with_trimal_v1.2

`trimal -in example1 -out output1 -htmlout output1.html -gt 1`

## Obtain a phylogeny using IQ-TREE

### A. Installing the required software

On CHEOPS1:  `module load iqtree/2.1.4b`

When working on a personal computer or elsewhere: 

1. Using conda

```
conda create -n iqtree
conda activate iqtree
conda install -c bioconda iqtree
```

2. Downloading and following instruction according to OS: http://www.iqtree.org/doc/Quickstart#installation
3. IQ-TREE offers a web server as well: http://iqtree.cibiv.univie.ac.at

### B. Implementing the commands

*IQ-TREE*: http://www.iqtree.org/doc/Command-Reference

`iqtree -s <alignment> [OPTIONS]`


## Interpret the results

On your personal/course computers you can download FigTree. This will help you visualize the phylogeny you have obtained from IQ-TREE in the previous step. 

*FigTree*: http://tree.bio.ed.ac.uk/software/figtree/

Check the bootstrap values that support each of your clades. Is this expected? 
Compare your phylogeny to literature, do you have a similar placement of the different species?


