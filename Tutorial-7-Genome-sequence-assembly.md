## Tutorial #7 Genome Sequence Assembly with Flye

This tutorial includes how to use screens, download files from external sources using wget, assemble genome sequences from Nanopore MinION long-read sequence data using flye, and how to view assembly graphs using Bandage. Perhaps most importantly, it includes instructions for one way to document your analyses as you go. 

### Prepare your VM and conda environments

1. Start your VM and open a shell, then make a new directory for this tutorial.
<!-- -->
        mkdir Tutorial7-assembly
        
2. Activate your 'quotidian' conda environment and install wget.
<!-- -->
        conda activate quotidian
        conda install -c anaconda wget
Type `  y ` when prompted. Once the installation is finished `  deactivate quotidian  `.

3. Create a new conda environment for flye (https://github.com/fenderglass/Flye) and install it. 
<!-- -->
        conda create -n flye -c bioconda flye
        
### Download the data

4. Once the installation is finished, move into the Tutorial7-assembly directory and start a screen. Screen allows you to start a subterminal within the shell that you are already working. Even if your computer disconnects from the internet, or the shell disconnects from the google server, processes you start in a screen will continue running and you can return it once you reestablish your connection. You can also use screens to simultaneously run multiple different processes. To install screen and start a screen run the following command.
<!-- -->
        conda install -c conda-forge screen
        screen -S assembly
        
5. Once the screen has started, move into the Tutorial #7 directory and activate the quotidian conda environment.
<!-- -->
        cd Tutorial7-assembly
        conda activate quotidian

6. The fastq files for *Sulcaria isidiifera* are available from the European Nucleotide Archive (https://www.ebi.ac.uk/ena/browser/view/PRJEB48709?show=reads). You can read more about this critically endangered lichen on the Red List website (https://www.iucnredlist.org/species/70386122/70386125). This sequence data was generated on the Nanopore MinION platform in the Allen Lichen Lab as part of the Org.one program.

To download the reads use the following command. 
<!-- -->
        wget ftp://ftp.sra.ebi.ac.uk/vol1/run/ERR738/ERR7385058/Sulcaria_isidiifera.tar.gz

**The download will take a while**, so if you want to leave this screen while the download continues you can use 'Ctrl+a+d' to leave the screen and let it continue running. To see a list of all screens running at any given time use `  screen -ls  ` and to return to a screen use `  screen -r <name of screen>  `. We can return to the screen where the download is running using the following command.
<!-- -->
        screen -r assembly
7. Once the download is complete, you will have to decompress the directory using the following command.
<!-- -->
        tar -xvf Sulcaria_isidiifera.tar.gz 
8. Once the decompression is complete, delete the original file that you downloaded to save space.
<!-- -->
        rm Sulcaria_isidiifera.tar.gz
        
### Documenation and bioinformatics

Keeping track of which commands you ran, in which order, with all of the specific options and settings you used is essential for reporting your results, and for conducting reproducible and verifiable analyses. There are many different approaches to documenting your analyses. In this class we will take a relatively simple approach.

Each major process that you run will be written into a bash script, and you will add analyses to the script as you go. Now, think back to lab one when we put a grep command in a bash script. Imagine adding a second command to that script. If you then closed that script and ran it, both analyses would run. 

Now that we are running more complex and time-consuming analyses, we don’t want to re-run every analysis in our bash script every single time we add a new step. To avoid re-running a line in our script we can use the pound symbol (#) to comment out the lines we don’t want to run at any given time. Keep this in mind as we set up our script for the day. 

1. Use nano to start building your analysis documentation. 
<!-- -->
        nano SUISassembly.sh
2. Enter the following text into your new nano file. Make sure EVERYTHING is spelled correctly. You may just want to copy-past this into your terminal.
<!-- -->
        #!/bin/bash
        #This line will not run because it starts with a comment
        #
        #Assembly of Sulcaria isidiifera genome
        #Bioinformatics tutorial #7
        #
        #Today's Date
        #Genome assembly and polishing
        #
        conda activate flye
        flye --nano-hq fast5_pass/*.fast5 --out-dir flyenanohq --threads 8  
        conda deactivate

Let’s break this script down a bit. On the first line we have the header text for all bash scripts. Then, I have a second line of text illustrating what beginning a line with ‘#’ does. Then we title this whole bash script that we are beginning. What is it that we are analyzing and for what project? Next I leave a line break so it is easier to read the script, then add the date and the specific tasks we are accomplishing. After that, another line break to help with readability. Then, we have to activate the conda environment for flye. On the next line we run flye. We use the –nano-hq flag to indicate that we are using high-accuracy nanopore reads. We name the output directory flyenanhq to indicate the assembler and the setting we used. Threads indicates the number of parallel threads to run the process with, here we set it to 8, which is maximum available on this VM. Finally, we deactivate the conda environment.

3. Close and save your new script. Then use the following command to make it executable: 
<!-- -->
        chmod +x SUISassembly.sh

4. To run your your script use the following command.
<!-- -->
        bash -i SUISassembly.sh
**Now is a good time to take a break. The assembly will take at least half a day to run.**

### Assembly graphs in Bandage

While we wait for the assembly to finish we can download Bandage and look at some sample data.

1. Download the program Bandage, which we will use to look at our assembly graphs: https://rrwick.github.io/Bandage/
2. Move the folder onto the desktop, right click and select ‘extract all’ to decompress the file. 
3. Open the decompressed folder, than open the folder title ‘Bandage’ within that folder. 
4. To start Bandage click the word Bandage with the assembly graph symbol next to it: 
<img src="https://user-images.githubusercontent.com/17323363/178351250-c537840e-21e6-41d0-9a75-a896713f500f.png" width="300">

5. Open the sample data by clicking: File > Load graph > then selecting ‘sample_LastGraph’ that was provided with the program download.
6. Next, click ‘Draw graph’
<img src="https://user-images.githubusercontent.com/17323363/178351275-bd77b1a8-af4c-487c-9e7a-65ae0551c123.png" width="300">
7. Select the longest node by clicking on the longest thick line.
8. Under 'Graph Display' change the color to 'color by depth.'
<img src="https://user-images.githubusercontent.com/17323363/178351518-4c7249b1-a205-4ebd-a094-0a9786a7ffa2.png" width="200">
9. Find a node that’s ~10,000 bp. Select it by clicking on it. Then navigate to Output > Copy selected node sequence to clipboard. 
10. Open a web browser and navigate to blast on the NCBI database. Use blastn to search this sequences against the whole NCBI database. 
11. Now select one of the thin lines. The thin lines are called edges. These represent the connections between two nodes. Take a look at what appears in the 'Selected edge' box on the right when you select a thin line.

### Examining flye results

1. If your google cloud connection reset since you launch your flye assembly, you can return to it now. You will first have to switch your user to ‘usr.’ Then, to reattach the screen use the following command: screen -r assembly
2. Move into the output directory for your flye assembly. If you followed these instructions exactly the output path will be as follows: 
<!-- -->
        cd Tutorial7-assembly/flyenanohq

3. Use ` ls ` to list all of the directory contents. 
4. Let’s explore a few key components of the output. The ‘assembly_info.txt’ file is one of the most useful outputs. Use the less command to take a look at it. 
<!-- -->
        less assembly_info.txt
5. The file with the actual assembled genome sequence is assembly.fasta, which you should also take a look at using less.
6. Next, download the assembly graph. Check out instructions in tutorial #6 for how to download files. As a hint, you may want to start by running the following command.
<!-- -->
        readlink -f assembly_graph.gfa
7. Once the assembly graph is downloaded, navigate back to Bandage and open this new assembly graph. This assembly graph is much more complicated than the data that comes with Bandage.

The data you assembled comes from an organism with a very diverse microbiome. Lichens host an incredible amount of bacterial, fungal, algal and animal diversity. The next step in genome assembly is metagenomic filtering, which is not included in this set of tutorials as it is a fairly complex process. Thus, we will skip straight to genome annotation in the next step and use an assembly that has already been filtered to include only the the lichenized fungal genome.                                                                                                                         
