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

You just searched a smaller set of sequences for similarity to your query sequence, rather than searching the entire NCBI nucleotide database. We will now repeat this smaller search in your Google Cloud VM.

#### Command-line BLAST on the virtual machine

1. To navigate to your virtual machine, go to the Google Cloud Console, then click the three horizontal lines in the top left corner > Compute Engine > VM Instances.

![image](https://user-images.githubusercontent.com/17323363/177422128-dcec7fbc-d3f9-43ce-ae50-1e8c5d1bfb0b.png)

2. Once you are on this page, click the three vertical dots on the far right of the VM and clicke 'Start/Resume.' Once the circle to the left turns green with a white check mark, click SSH to open a shell.

![image](https://user-images.githubusercontent.com/17323363/177423041-38e4d20d-f3ef-4af6-b616-d458334db20a.png)

3. We will start by creating a conda environment for blast and installing it. Execute the following command. When asked whether or not you would like to proceed, type 'y' for yes. The options after calling conda indicate the following:   
        'create' - make a new conda environment   
        '-n blast' - call your new conda environment 'blast'  
        '-c bioconda' - search the bioconda repository  
        'blast' - this is the name of the package you would like to find and download 
<!-- -->
        conda create -n blast -c bioconda blast 
        
4. To start your newly created conda environment execute the following command.
<!-- -->
        conda activate blast

5. To view the options available for blastn execute the following command.
<!-- -->
        blastn -h
        
6. Next we will want to do some searching, but we need to move some sequence data on to the VM to do so. Keeping files and directories organized is one of the most importan skills a bioinformatician can possess, and we will start building some file organization habits from the start. First, make a directory called 'Tutorial5-BLAST' then move into it using the following commands.
<!-- -->
        mkdir Tutorial5-BLAST
        cd Tutorial5-BLAST
        
7. Make a file called PSMA.fasta whose contents are the sequence below using nano (check Tutorial #2 for hints). 

>EU558739.1 Pseudocyphellaria mallota voucher Stenroos 5556 (TUR) small subunit ribosomal RNA gene, partial sequence; internal transcribed spacer 1, 5.8S ribosomal RNA gene, and internal transcribed spacer 2, complete sequence; and large subunit ribosomal RNA gene, partial sequence
GTCGTAACAAGGTCTCCGTAGGTGAACCTGCGGAGGGATCATTACCGAGAGAGGCTCGCGCCTCGGGGGC
TTTGGCCCCCGTCGTCTCACCCGTGCGCACATCCACCGGTGTTGCCTTTGGCGGCCTCTGCCGCGCAAGA
ACCCCAACTCTTTGCAACGTTTGTGTCGTCCGAGTGGTTACCGAATAACTAAAACTTTCAACAACGGATC
TCTTGGTTCTGGCATCGATGAAGAACGCAGCGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAA
TCATCGAATCTTTGAACGCACATTGCGCCCCTTGGCATTCCGAGGGGCATACCTGTTCGAGCGTCAGTAC
ACCCCTCCAGCGCGGCTGGGTGATGGGCGGCGTCCCCCCCGGGGACGGGCCCGAACGGCAGTGGCGGCCC
GGCGTGGCTCCCAGCGCGGTGAATTTCGTTCGCTGGGGAGGCGCGCCCGGGTCCGGCCAGTCAACCCTGT
GGCTTTGCAGTTTGACCTCGGATCAGGTAGGGATA

8. Upload the fasta file you downloaded earlier with the 12 *Pseudocyphellaria mallota* ITS sequences (see Tutorial #4 for how to upload a file). You will notice that the file was not uploaded into your current directory, Tutorial5-BLAST, but was instead uploaded to your home directory. You can move it into your current directory using the following command. Note that we are directing the command to find the file named 'sequence.fasta' in the directory above the current directly using '..' and we are telling it to put the file in our current directory using '.'
<!-- -->
        mv ../sequence.fasta .
 
 Then rename the file using the following command.
 <!-- -->
        mv sequence.fasta PseuITS.fasta

9. To make the sequences in PseuITS.fasta into a blast database execute the following command.
<!-- -->
        makeblastdb -in PseuITS.fasta -out PseuITS.fasta -dbtype nucl
        
        
