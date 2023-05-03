# **Phylogenomics**


We will work with the orthogroups as you already have learned how to identify last week. We will be working with the data in the `/scratch/phylog-course/` folder in CHEOPS. Create a folder of your own (if you don't already have one). We will select subsets of orthologues for each to work on, we will obtain phylogenies for each of the sets to compare how the results and resolution of the analysis changes with the data that is used. 


## Data set selection and extraction of specific orthogroups

Here are some orhtologues that you could use (Single-Copy): 

- 7050at6231.faa
- 8055at6231.faa
- 9097at6231.faa
- 3553at6231.faa
- 4183at6231.faa
- 5142at6231.faa
- 6503at6231.faa
- 6753at6231.faa
- 7230at6231.faa
- 7546at6231.faa

(check if they are available for all the datasets  `find . -name 7050at6231.faa`)


### Information about the orhtologue

*OrthoDB*: https://www.orthodb.org
*BUSCO*: https://academic.oup.com/bioinformatics/article/31/19/3210/211866

**A.** Before we start: we need to prepare/order the data in a logical way for our analysis. Do you have an idea how? Take a look at the current folder structure and names of the files.

**B.** Choose a strategy for sorting them (e.g. create new folders for each taxa where we place only the orthologues of interest we will work with, rename files in the individual folders per taxa, once each file can be traced back to their taxa of origin, re group the orhtologues in folder according to the genes and not the taxa).  

 - Copy the files needed to the new folders `for file in $(cat list); do cp "$file" new_folder; done`
 
**C.** Renaming files to match their taxa:

`for f in *.faa*; do mv -i -- "$f" "${f//.faa/celegans.faa}"; done`

**D.** Check the header of the file. Rename the header of the contig/gene so it matches the taxa and orthoglogue (think first about how you would do this on your own!):

`for FILE in *.faa;do awk '/^>/ {gsub(/.faa?$/,"",FILENAME);printf(">%s\n",FILENAME);next;} {print}' $FILE >>changed_${FILE}; done`


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

**A.** Alignement of genes from different species

*MAFFT*: https://mafft.cbrc.jp/alignment/software/

`mafft -h`

`mafft --auto in > out`

you should create a list with your file names and then put all the sequences together into a file

`while read f; do cat $f* >> $f"_for_mafft" ; done < genelist`

Note: alignments need to be trimmed to remove poorly aligned regions that could yield inproper results.

**B.** Trimming the alignment
```
conda create -n trimal
conda activate trimal
conda install -c bioconda trimal
```

(alternatively check: https://github.com/inab/trimal)

*TRIMAL*: http://trimal.cgenomics.org/getting_started_with_trimal_v1.2

`trimal -in example1 -out output1 -htmlout output1.html -gt 1`

**C.** Concatenate the gene alignments

*Concatenate.rb*: https://github.com/mmatschiner/tutorials

`ruby concatenate.rb -i 09/*.nex -o concatenated.nex -f nexus`

(alternatively check https://github.com/nylander/catfasta2phyml)

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

- Check the bootstrap values that support each of your clades. Is this expected? 
- Compare your phylogeny to literature, do you have a similar placement of the different species?
- When comparing phylogenies with different subsets of genes, what do you notice? How does support change?

*A novel nematode species from the Siberian permafrost shares adaptive mechanisms for cryptobiotic survival with C. elegans dauer larva*: https://www.biorxiv.org/content/10.1101/2022.01.28.478251v6.full

