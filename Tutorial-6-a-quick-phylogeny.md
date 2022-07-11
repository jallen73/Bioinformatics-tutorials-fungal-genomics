## Tutorial #6 A Quick Phylogeny

This tutorial covers how to create a multiple squence alignment using MUSCLE (https://www.drive5.com/muscle/) and a Maximum-Likelihood phylogeny in IQ-TREE (http://www.iqtree.org/). Then, it includes instructions on how to visualize the phylogeny in FigTree (http://tree.bio.ed.ac.uk/software/figtree/). 

1. Start and open your VM. Then make a new directory for Tutorial 6 data.
<!-- -->
        mkdir Tutorial6-Phylo
        
2. Next we will creat two new conda environments and install MUSCLE and IQ-TREE. Run each of the following commands. When prompted by the install type 'y' to indicate you would like to proceed with the installation.
<!-- -->
        conda create -n muscle -c bioconda muscle
        conda create -n iqtree -c bioconda iqtree

3. Upload the file 'Tutorial-6-data.fasta' using the upload button on the VM shell. This data file includes a selection of nuclear Internal Transcribed Spacer (ITS) sequences from an assortment of *Pseudocyphellaria* and *Sticta* species. Rename and move the file into the Tutorial6-Phylo directory it using the following command. Then move into the Tutorial 6 directory.
<!-- -->
        mv Tutorial-6-data.fasta Tutorial-6-Phylo/Psuedo.Sticta.ITS.fasta
        cd Tutorial6-Phylo
 
 4. Build the multiple sequence alignment. First activate the muscle conda environment, then run muscle by indicating the input alignment file as 'Pseudo.Sticta.ITS.fast' and name the output alignment file 'Ps.St.ITS.aln.fasta.'
<!-- -->
        conda activate muscle
        muscle -align Psuedo.Sticta.ITS.fasta -output Ps.St.ITS.aln.fasta
        
After the alignment is finished, check for the output file using ` ls `. Once you have confirmed it is present you can deactivate the muscle conda environment using ` conda deactivate `.

5. To build the Maximum Likelihood phylogeny, first activate the iqtree conda environment. Then, run IQ-TREE by indicating the input file as the output alignment from the previous step (-s Ps.St.ITS.aln.fasta) with 1000 bootstrap replicates (-B 1000) using all four threads available on your VM (-nt 4). 
<!-- -->
        iqtree -s Ps.St.ITS.aln.fasta -nt 4 -B 1000

Check out the log file output from this process to learn more about the phylogeny building process. You can use `  less Ps.St.ITS.aln.fasta.log  ` to view the file, then the down arrow to scroll through the file. One of the most important pieces of information in this fiel is the Best-fit nucleotide substition model that was selected. For this dataset, this was the resulting model that was selected based on the Bayesian Information Criteria, `  Best-fit model: F81+F+G4 chosen according to BIC  `. Type `  q  ` to exist viewing the log file.

6. Next, download the tree file. During the download process, the box will prompt you for the full path to the fiel you want to download. To easily get the full path including the file name that you can copy out of the shell using the following command.
<!-- -->
        readlink -f Ps.St.ITS.aln.fasta.treefile

Highlight the resulting path, which will automatically copy the text. Now click the download button on the top right of the shell, paste the path into the box then click 'Download.'

<img src="https://user-images.githubusercontent.com/17323363/178339460-65a7105f-642f-4d44-a03a-9f397aabda59.png" width="400">

7. To download FigTree navigate to the GitHub page for the program (https://github.com/rambaut/figtree/releases) then download the zip file. Move the zip file into a directory where you like to keep tools and programs handy on your local maching, unzip the directory, then double click 'FigTree v1.4.4.exe' to start the program.

<img src="https://user-images.githubusercontent.com/17323363/178339988-2a50d749-1788-41eb-aa92-07eb92638dd3.png" width="200">

8. Clicke File > Open, then select your .treefile and click Open. When asked what to name the node/branch labels, type 'boostrap' and click 'OK.'

<img src="https://user-images.githubusercontent.com/17323363/178340410-e77d6f86-1512-47a2-aa77-05e5c8156fb6.png" width="200">

Once you have your treefile open in FigTree you can edit and modify the format in many different ways. For now, we will make two edits. First, to reroot the tree select one branch by clicking on it. Here I have selected a long branch. 

<img src="https://user-images.githubusercontent.com/17323363/178340705-cc5c6449-5aa4-4a77-ad96-045169f3ab0c.png" width="600">

Then click 'Reroot' to the top left of the menu, and your phylogeny will end up looking something like this.

<img src="https://user-images.githubusercontent.com/17323363/178340839-e2747604-d71b-47df-88c7-031350c5ebcc.png" width="600">

Next, add the bootstrap values by clikcing 'Branch Labels' and using the drop down to choose 'bootstrap.'

<img src="https://user-images.githubusercontent.com/17323363/178340988-27c59ad8-0409-4646-a4ed-7c037724fa4d.png" width="600">

9. You can export the tree in a number of different file formats for further editing and beautification as needed by navigating to the menu under 'File.' For instance, you can use the free vector-editing software Inkscape (https://inkscape.org/) with an .svg file to easily edit the node and branch labels.
