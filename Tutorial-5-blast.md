## Tutorial #5 Basic Local Alignment Search Tool

This tutorial covers how to use BLAST on the web, create a conda environment, install a package using conda, activate a package, make a blast database, and run a blast search in a Linux shell.

#### BLAST on the web

BLAST is a handy tool for searching a sequence of interest, which is called the query sequence, agains a database of sequences. The algorithm  uses a word-based heuristic to speed up local alignments, thus making it possible to query a massive sequence database quickly. The query and database can be amino acid or nucleotide sequences, though we will only work with nucleotide sequences in this tutorial. 

We will start by working with the National Center for Biotechnology Information Nucleotide Database. 

1. Navigate to the following URL: https://www.ncbi.nlm.nih.gov/nucleotide/

2.	Start by searching: ‘Pseudocyphellaria mallota ITS’

3.	Click on the first item returned and read through the information associated with this sequence.

5.	Click ‘FASTA’ at the top to see the sequences in fasta format.

6.	Open another tab and navigate to blast using this URL: https://blast.ncbi.nlm.nih.gov/Blast.cgi

7.	There are multiple different types of blast to choose from. We will use Nucleotide BLAST for now.

8.	Go back to the previous tab. You can either copy-paste the accession number (circled below in red) or the full sequence from this page to the ‘Enter Query Sequence’ box on the blast page.

