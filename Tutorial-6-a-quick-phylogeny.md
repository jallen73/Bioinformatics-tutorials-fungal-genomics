## Tutorial #6 A Quick Phylogeny

This tutorial covers how to create a multiple squence alignment using MUSCLE (https://www.drive5.com/muscle/) and a Maximum-Likelihood phylogeny in IQ-TREE (http://www.iqtree.org/). Then, it includes instructions on how to visualize the phylogeny in FigTree (http://tree.bio.ed.ac.uk/software/figtree/). 

1. Start and open your VM. Then make a new directory for Tutorial 6 data.
<!-- -->
        mkdir Tutorial6-Phylo
        
2. Next we will creat two new conda environments and install MUSCLE and IQ-TREE. Run each of the following commands. When prompted by the install type 'y' to indicate you would like to proceed with the installation.
<!-- -->
        conda create -n muscle -c bioconda muscle
        conda create -n iqtree -c bioconda iqtree

3. Upload the file 'Tutorial-6-data.fasta' using the upload button on the VM shell. Rename and move the file into the Tutorial6-Phylo directory it using the following command. Then move into the Tutorial 6 directory.
<!-- -->
        mv Tutorial-6-data.fasta Tutorial-6-Phylo/Psuedo.Sticta.ITS.fasta
        cd Tutorial6-Phylo
 
 4. Build the multiple sequence alignment 
<!-- -->
        conda activate muscle
        muscle -align Psuedo.Sticta.ITS.fasta -output Ps.St.ITS.aln.fasta
        
After the alignment is finished, check for the output file using ` ls `. Once you have confirmed it is present you can deactivate the muscle conda environment using ` conda deactivate `.

 
