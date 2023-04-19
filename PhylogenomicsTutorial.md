#**Phylogenomics**


We will work with the orthogroups you have identified last week.
We will select subsets of them and obtain phylogenies for each of the sets to compare how the results and resolution of the analysis changes with the data that is used. 


##Data set selection and extraction of specific orthogroups

jeje


##Prepare alignments for the different sets

Since you are working on CHEOPS1, you can use packages that are available there. 
module load mafft/7.471

When working on a personal computer or elsewhere were the package isn't available you can install it. 

1. Using conda

conda create -n mafft
conda activate mafft
conda install -c bioconda mafft

2. Or downloading and following the instricution according to your OS: https://mafft.cbrc.jp/alignment/software/


##Obtain a phylogeny using IQ-TREE

jeje

On CHEOPS1:  module load iqtree/2.1.4b

When working on a personal computer or elsewhere: 

1. Using conda

conda create -n iqtree
conda activate iqtree
conda install -c bioconda iqtree

2. Downloading and following instruction according to OS: http://www.iqtree.org/doc/Quickstart#installation
3. IQ-TREE offers a web server as well: http://iqtree.cibiv.univie.ac.at



##Interpret the results
