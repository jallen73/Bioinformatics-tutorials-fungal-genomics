## Tutorial #8 Genome annotation with funannotate

1. Start your VM and open a shell. Make a new directory for this tutorial and move into.
<!-- -->
        mkdir Tutorial8-annotation
        cd Tutorial8-annotation
2. Download the SUIS_asco_consensus.fasta file from this GitHub repository, upload it to your VM, then move it into the Tutorial #8 directory.
        mv SUIS_asco_consensus.fasta .
        
3. Examine basic statistics about this genome assembly using Quast (http://quast.sourceforge.net/). First make a new conda environment,  install quast, activate quast, then run it.
<!-- -->
        conda create -n quast -c bioconda quast
        conda activate quast
        quast SUIS_asco_consensus.fasta
    
4. Take a look at the quast results with the following commands.
<!-- -->
        cd quast_results/latest/
	      less report.txt
5. Next, we will download databases of gene sequences that will be used for the homology-based genome annotation. First, start a screen because the downloading process may take a while, then activate the funannotate conda environment. Move up two directories so you are in /home/usr/ then make a directory called funannotate_db.
        
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

