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

![image](https://user-images.githubusercontent.com/17323363/177419182-99aeacc5-2fe9-475e-a07b-24351aa3285b.png)

Here is what your query should look like

![image](https://user-images.githubusercontent.com/17323363/177419206-b1c08428-e568-467a-bf31-67de26613df5.png)

There are quite a few different options and settings you can change on this page. For now we will leave the defaults in place, scroll down and push the ‘BLAST’ button.

Many different scores are given for each match. You can see here that the highest hit is actually the sequence that we initially used for the search, and the E-value is zero. Click on a match with an E-value over 0.  By clicking on a match you should then be able to see one of the pairwise sequence alignments. 

You can read more about what each of the values in the output table mean for how well each database entry matched your query sequence at the bottom of this page: https://www.ncbi.nlm.nih.gov/Web/Newsltr/V15N2/BLView.html 

9. There is a lot to explore here, but for now we are going to do a second search. Return to the tab for the NCBI nucleotide database where you initially searched for the sequence you used as a query sequence.  

10.	Next, we want to select all 12 of these sequences. Click ‘send to’ in the top right, select ‘file’ and select ‘FASTA’ for the format. Then, click 'Create File' and a fasta file will download.

![image](https://user-images.githubusercontent.com/17323363/177420539-b67bcf33-c063-4170-8b8e-9ff8fdffe15d.png)

11. Navigate back to the nucleotide BLAST search page. Select the ‘Align two or more sequences’ box, which is circled in red below. 

![image](https://user-images.githubusercontent.com/17323363/177420709-1e09a218-1a1a-4993-a35e-d83d81b47fcc.png)

12.	The query sequence will be the same one we used for the last search, so type ‘EU558851.1’ into the query box. The subject sequences will be the fasta file you just downloaded. Use the ‘Choose File’ button and add your fasta file here. Then click BLAST. Once the search finishes, take a look at the ouput.

In the second part of this tutorial you searched a smaller set of sequences for similarity to your query sequence, rather than searching the entire NCBI nucleotide database. We will not repeat this smaller search in your Google Cloud VM.

#### Command-line BLAST on the virtual machine

