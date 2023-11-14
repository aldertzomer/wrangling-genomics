---
title: "Background and Metadata"
teaching: 10
exercises: 5
questions:
- "What data are we using?"
- "Why is this experiment important?"
objectives:
- "Why study *E. coli*?"
- "Understand the data set."
- "What is hypermutability?"
keypoints:
- "It is important to record and understand your experiment's metadata."
---

# Background

We are going to use a long-term sequencing dataset from a population of *Escherichia coli*. 

 - **What is *E. coli*?**
    - *E. coli* are rod-shaped bacteria that can survive under a wide variety of conditions including variable temperatures, nutrient availability, and oxygen levels. Most strains are harmless, but some are associated with food-poisoning. 
    
![ [Wikimedia](https://species.wikimedia.org/wiki/Escherichia_coli#/media/File:EscherichiaColi_NIAID.jpg) ](../img/172px-EscherichiaColi_NIAID.jpg)

<!-- https://species.wikimedia.org/wiki/Escherichia_coli#/media/File:EscherichiaColi_NIAID.jpg -->

 - **Why is *E. coli* important?**
    - *E. coli* are one of the most well-studied model organisms in science. As a single-celled organism, *E. coli* reproduces rapidly, typically doubling its population every 20 minutes, which means it can be manipulated easily in experiments. In addition, most naturally occurring strains of *E. coli* are harmless. Most importantly, the genetics of *E. coli* are fairly well understood and can be manipulated to study adaptation and evolution.
    
# The data

 - The data we are going to use is part of a long-term evolution experiment led by [Richard Lenski](https://en.wikipedia.org/wiki/E._coli_long-term_evolution_experiment).
 
 - The experiment was designed to assess adaptation in *E. coli*. A population was propagated for more than 40,000 generations in a glucose-limited minimal medium (in most conditions glucose is the best carbon source for *E. coli*, providing faster growth than other sugars). This medium was supplemented with citrate, which *E. coli* cannot metabolize in the aerobic conditions of the experiment. Sequencing of the populations at regular time points revealed that spontaneous citrate-using variant (**Cit+**) appeared between 31,000 and 31,500 generations, causing an increase in population size and diversity. In addition, this experiment showed hypermutability in certain regions. Hypermutability is important and can help accelerate adaptation to novel environments, but also can be selected against in well-adapted populations.
 
 - To see a timeline of the experiment to date, check out this [figure](https://en.wikipedia.org/wiki/E._coli_long-term_evolution_experiment#/media/File:LTEE_Timeline_as_of_May_28,_2016.png), and this paper [Blount et al. 2008: Historical contingency and the evolution of a key innovation in an experimental population of *Escherichia coli*](http://www.pnas.org/content/105/23/7899).
 
 
## View the metadata

We will be working with three sample events from the **Ara-3** strain of this experiment, one from 5,000 generations, one from 15,000 generations, and one from 50,000 generations. The population changed substantially during the course of the experiment, and we will be exploring how (the evolution of a **Cit+** mutant and **hypermutability**) with our variant calling workflow. The metadata file associated with this lesson can be [downloaded directly here](https://raw.githubusercontent.com/datacarpentry/wrangling-genomics/gh-pages/files/Ecoli_metadata_composite.csv) or [viewed in Github](https://github.com/datacarpentry/wrangling-genomics/blob/gh-pages/files/Ecoli_metadata_composite.csv). If you would like to know details of how the file was created, you can look at [some notes and sources here](https://github.com/datacarpentry/wrangling-genomics/blob/gh-pages/files/Ecoli_metadata_composite_README.md).



This metadata describes information on the *Ara-3* clones and the columns represent:

| Column           | Description                                |
|------------------|--------------------------------------------|
| strain           | strain name					|
| generation       | generation when sample frozen		|
| clade            | based on parsimony-based tree		|
| reference        | study the samples were originally sequenced for				|
| population       | ancestral population group |
| mutator          | hypermutability mutant status |
| facility         | facility samples were sequenced at |
| run              | Sequence read archive sample ID		|
| read_type        | library type of reads |
| read_length      | length of reads in sample |
| sequencing_depth | depth of sequencing |
| cit              | citrate-using mutant status		|


> ## Challenge
> 
> Based on the metadata, can you answer the following questions?  
> *Try using the command line where appropriate (except Q1 which will be a real challenge requiring more background knowledge not directly covered within this course (regular expressions and/or using awk)).*
> 
> 1. How many different generations exist in the data?
> 2. How many rows and how many columns are in this data?
> 3. How many citrate+ mutants have been recorded in **Ara-3**?
> 4. How many hypermutable mutants have been recorded in **Ara-3**?
>
> > ## Solution
>> 
> > 1. 25 different generations
> >    + This answer is easiest found by inspecting the metadata in a spreadsheet.
> >    + More challenging option is to use `awk` or regular expressions in combination with grep (see advanced extra work (not covered in the exam)).  
> >      Process: get the second field of the metadata, return an unique list and count.  
> >      + grep/regular expression (matching from `^` start until first `,` then only numbers `[0-9]`:  
> >        + `grep -P -o '^[A-Za-z0-9]+,[0-9]+,' Ecoli_metadata_composite.csv | sed -r "s/.+,([0-9]+),/\1/" | sort -u | wc -l`
> >          + first use grep to ONLY (-o) return the REGULAREXPRESSION (-P) match to the MOTIF line starting with (^) any alphabeth character followed by , and a number of more than 0 (+) length [0-9]+
> >          + sed is basically a one line search and replace. It searches in the grep output for the number and only returns (\1) the number found by ([0-9]+).
> >          + Next we make a sorted list, make it uniq and count the uniques lines.
> >          + Try asking [ChatGPT](https://chat.openai.com/share/e19bf110-dbce-40ba-a04e-5b379cf7e2c6) to explain the grep answer and be amazed! 
> >      + or if you followed the extra `awk` work:  
> >          + `awk -F',' '{print $2}' Ecoli_metadata_composite.csv | sort -u | wc -l`
> >            + awk will let you work with column data where -F specifies we use the comma as column separator
> >            + next we need to tell by "programming" that we want to see column 2 ($2).
> >            + subsequently we make a sorted list into a unique list and line count.
> >          + Why does awk return 26 instead of 25 as a count? Header?
> >    + Student contributed solution using the toolbox covered in the main instructions:  
> >      + `cut -d, -f2 Ecoli_metadata_composite.csv | tail -n+2 | sort -u | wc -l`  
> >         + The cut command can extract a specific COLUMN of data based on the specified delimiter (-d saying it is a comma). Then -f2 extracts the SECOND column.
> >         + The `tail -n+2` command uses explicit **+2** to start printing output from line 2 onwards to skip counting the header.
> >         + We subsequently sort and make UNIQUE (-u) and count the lines
> > 2. 62 rows, 12 columns
> >    + `tail -n+2 Ecoli_metadata_composite.csv | wc -l`
> >      + tail complete file from line 2 down, subsequently count the number of lines
> >    + `head -n1 Ecoli_metadata_composite.csv | grep ',' -o | wc -l`
> >      + This takes the first HEADER line only, finds with grep ONLY (-o) matching , and counts them. We need to add 1 for the total: 11+1 = 12
> > 4. 10 citrate+ mutants
> >    + `grep ',plus$' Ecoli_metadata_composite.csv | wc -l`
> >      + find plus in the LAST ($=end of line) column and count number of rows
> >      + Altrnative a count can be done in one go with grep -c: `grep -c ',plus$' Ecoli_metadata_composite.csv`
> > 6. 5/6 hypermutable mutants (depending if you look at the clade (+H) or the mutator label)
> >    + `grep -c '+H,' Ecoli_metadata_composite.csv`
> >      + It finds all lines that has the +H (hypermutator) flag. It also counts (-c)
> {: .solution}
{: .challenge}

<!-- can add some additional info relevant to interplay of hypermutability and Cit+ adaptations, but keep it simple for now -->

