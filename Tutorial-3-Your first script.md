## Tutorial #3 Your first script

Throughout these tutorials we will be using many different tools to run analyses. We won’t be writing any tools of our own, but it’s important for us to understand the basics of how writing a script that is executable works so we better understand what is happening when we use other tools, or scripts, to run analyses. The tools we use are essentially text files that process other text files to transform them into specific outputs, ususally text files again, that we want. Today we will write and run a classic, basic bash script called hello world and a second script that will search fasta files.

#### Hello World

1.	First, we will create a file for our script using nano with the following command. 
<!-- -->
        nano hw.sh
        
3.	Once your new file is open in nano, add the following lines to your script. 
<!-- -->
        #!/bin/bash
        echo ‘Hello World!’
        
5.	Exit nano and save your file. Then type the following command to change the access rights to the file so that it is executable. 
<!-- -->
        chmod +x hw.sh
        
7.	Now, you can run your program with the following command. 
<!-- -->
        ./hw.sh
        
And now you have written and run your first program. Congratulations! 

#### Search fasta

We can, and will often, pass files as inputs into scripts as well. We will write one more script today to illustrate how this works. 

1. Run the following command to create a file. 
<!-- -->
        nano search_fasta.sh
        
2. Write your program using the variable ‘$1’ to indicate the first item passed to the program when you run it. That is, $1 is ascribable to what you put in the command line after the name of the script as you run it. Type the following text into your script.
<!-- -->
       #!/bin/bash
       grep ‘>’ $1
       
3.	Exit nano and save your changes. Use the chmod command to make the file executable. 

5.	Now, run the program and search the fasta file that you made in the previous tutorial using the following command. 
<!-- -->
        ./search_fasta.sh Letharia.fasta
        
#### Commands used in this tutorial

chmod = used to change the permissions for files and directories. Read the documentation for this tool for more details on how to use it.       
echo = prints text to standard out
