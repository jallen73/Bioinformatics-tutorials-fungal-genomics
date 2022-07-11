## Tutorial #8 Genome annotation with funannotate



### Set up funannotate and required databases
1. Start your VM and open a shell. Make a new directory for this tutorial and move into.
<!-- -->
        mkdir Tutorial8-annotation
        cd Tutorial8-annotation
2. Download the SUIS_asco_consensus.fasta file using [this link](https://drive.google.com/file/d/1VQ8LJJXiCIkn24742e6cW8oSfLA5AL5H/view?usp=sharing), upload it to your VM, then move it into the Tutorial #8 directory.
<!-- -->
        mv SUIS_asco_consensus.fasta .
        
3. Examine basic statistics about this genome assembly using Quast (http://quast.sourceforge.net/). First make a new conda environment,  install quast, activate quast, then run it.
<!-- -->
        conda create -n quast -c bioconda quast
        conda activate quast
        quast SUIS_consensus.fasta
    
4. Take a look at the quast results with the following commands.
<!-- -->
	cd quast_results/latest/
	less report.txt
5. Next, we will download databases of gene sequences that will be used for the homology-based genome annotation. First, start a screen because the downloading process may take a while, then activate the funannotate conda environment. Move up two directories so you are in /home/usr/ then make a directory called funannotate_db.
<!-- -->        
        mkdir funannoate_db
        screen -S fun
        conda create -n funannotate -c bioconda funannotate
        conda activate funannotate
   
6. We then set the location for the variable FUNANNOTATE_DB and add it to your list of global variables using the following commands. Change 'usr' to your user name.
<!-- -->
        export FUNANNOTATE_DB=/home/usr/Tutorial8-annotation/funannotate_db
        echo “export FUNANNOTATE_DB=/home/usr/Tutorial8-annotation/funannotate_db” >> ~/.profile
7. Next, download and setup the databases using the following command. 
<!-- -->
        funannotate setup -d $HOME/funannotate_db

8. Ensure all of the databases are fully up to date by running the following command.
<!-- -->
        funannotate setup -i all --update

9. Check that the set up worked properly by running the following command.
<!-- -->	
        funannotate database
10. [Download this file](https://drive.google.com/file/d/1NkPOLwSY6vOgQc77EZxtYRIjtI5-INtJ/view?usp=sharing), which includes amino acid sequences from the Pezizomycotina that will be used during genome annotation. Upload the file to your VM and move it into the Tutorial #8 directory.

### Create a bash script to clean, sort, and mask repititive regions

1. First, create a file for your bash script and open it in nano. Remember, we are running commands via a bash script so we have a record of the commands we used in our analysis.
<!-- -->
	nano annotate.sh
The first lines of your script should be the following.
<!-- -->
	#!/bin/bash
	#Annoation of Sulcaria isidiifera genome
	#Date

Then, we will want to run each of the following three commands to prepare the assembly for annation. The first command, 'clean,' removes duplicate and very short contigs. The second command sords the contigs and scaffolds by length and renames them sequentially (i.e., contig 1 will be the longest contig after this step is run). The third step masks repetitive regions like transposable elements and telomeres.
<!-- -->
	funannotate clean -i Suis_consensus.fasta --minlen 2000 -o Suis_consensus.clean.fasta
	funannotate sort -i Suis_consensus.clean.fasta -b scaffold -o Suis_consensus.sort.fasta
	funannotate mask -i Suis_consensus.sort.fasta -cpus 8 -o SUISv1.fasta

2. Exit nano and save your document. Use chmod to make the bash script executable, then run the following command.
<!-- -->	
	bash -i annotate.sh

### Genome annotation 

1. Next, we will annotate the genome using homology searches. Reopen your script 'annotate.sh'. Use the ‘#’ to add a comment in front of all of the lines of code you just ran. You want to keep that code to reference later, but you don’t want to rerun it.

2. Add the following two commands to your script. The backslashes here indicate that all three lines of code are part of the same command. We use the backslashes to make it easier for us to read long strings of code.
<!-- -->
	funannotate predict -i SUISv1.fasta -o suis_ann \
	    --species "Sulcaria isidiifera" \
	    --protein_evidence pezizo.pep \
	    --busco_seed_species aspergillus_fumigatus --cpus 8
	
	funannotate annotate -i suis_ann --cpus 8

3. Close and save your script. Then, run it using the following command.
<!-- -->
	bash -i annotate.sh

This step will take a few hours to complete. Exit your screen using ctrl+a+d. You can close and leave the shell now, but make sure to leave your VM running until these steps are complete. 

### Explore your genome annotation results

There are many different reasons one may want to annotate a genome, including conducting comparative genomics of many different organsims and identifying protein sequences to synthesize  and test antimicrobial qualities. In the example today we are interested in finding a specific protein in the genome, looking at where the protein occurs in relation to other proteins in the genome, and modeling its secondary structure. In this lab we will find the *APN2* gene, which is highly conserved gene that is part of the mating type locus in fungi.

1. Make a blast database out of the protein sequences of the annotations using the following command.
<!-- -->
	cd suis_ann/annotate_results
	conda activate blast
	makeblastdb -in Sulcaria_isidiifera.proteins.fa -out SUIS.proteins.fasta -dbtype prot 

2. The sequence below will be the query. Make a file called apn2.fasta using nano, and paste the following sequence into it.
<!-- -->
	nano apn2.fasta
	
>\>QEL51145.1 abasic endonuclease/DNA lyase [Letharia vulpina]
MGLRITTWNVNGIRNPFGYQPWRDKRSFAAMFDILEADIVVFQETKIQRKDLSDDMVLVPGWDCYFSLPR
HKKGYSGVVIYTRQSVCAPIRAEEGITGLLCSPNSSTNFSNLPEEQQIGGYPTPAQLAASAVDATTLDAE
GRSVVLEFPAFVLFGVYSPANRDETRDDFRLGFLDVLDARIRNLIAMGKRVFLTGDFNISREELDAANAE
VSMRKQGLTGLEFVSTPARRLFNHLLEGGKVFGERDEGREHSVLWDICRAFHPDRKGMFTCWEQKVNARP
GNCGARIDYVLCSLTMKDWFSDSNIQEGLMGSDHCPVYAVMKDAIFMDGVERDLRDVMNPPGMFSGGKRQ
REYSATSDPLPSSGKLIPEFFGRRNIRDMFAQKPSLPQSQSNGNSNKVAEVSGVTAANQGNSTAEMLGPI
EETAVEPCDSSVRVPTISPSAVGQKRSAPATTGSKSTKRGKSVFATAAAPMTGKGQQSLKGFFKPSAALI
SSVASAIHVREVPQTSLNDDTVGRAPADLAETYPAPDGHMKAASLESAIHTPRKVGTQHIPGESRFANAS
PIRNHKSVNQPQENVHDPVQSKESWSKLFTKPAAPRCEGHDEPCISLLTKKPGMNLGRSFWMCPRPLGPS
GAKEKNTQWRCQTFIWCSDWNPNATNG

3. Then, use this sequence as the query with blastp to search against the full complement of protein sequences and redirect the output to a file called apn2_blast.txt
<!-- -->	
	blastp -db SUIS.proteins.fasta -query apn2.fasta > apn2_blast.out
	
4. Look at your output using the less command. **note the name/number of the amino acid sequences that is the top hit result from your blast search. It should be something like 'FUN_009402-T1.'** Write down the name of the hit as you will need it in the next step. Deactivate the blast conda environment.

5. Next, we will extract the full APN2 amino acid sequence from the Suis annotations using samtools. First, install samtools in the quotidian conda environment.
<!-- -->
	conda activate quotidian
	conda install -c bioconda samtools
	conda deactivate
	conda activate quotidian
	
Then, index the proteins.fa file. Once it is indexed you can search specifically for the annotion that was the top hit for APN2 and redirect it to a fasta file. **rember to replace the 'FUN' number below with the number that was the best blast hit in the step above.**
<!-- -->
	samtools faidx Sulcaria_isidiifera.proteins.fa
	samtools faidx Suclaria_isidiifera.proteins.fa FUN_009402-T1 > suis_apn2.fasta

6. Look at the contents of the stde_apn2.fasta file using less. Open a web browser with ncbi blast. We will now use blastp to search this amino acid sequence against the whole NCBI protein database to see what the best match is for the recovered putative APN2 gene. 

