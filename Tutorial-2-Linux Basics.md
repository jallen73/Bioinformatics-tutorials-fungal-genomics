# Tutorial #2 Shell Basics

This tutorial shows users how to open a shell in Google Cloud and introduces some handy basic functions to help navigate Google Cloud shell. These commands are the same in both Cloud Shell and a Linux-based shell. 

##### 1.	Open a console using the button in the top right, circled in the image below.

![image](https://user-images.githubusercontent.com/17323363/176061816-8d0126b9-7008-461e-bc6f-18c85cc531c9.png)

Once your console is open it should look something like this, you may need to drag the console up to take up the whole screen: 
 
![image](https://user-images.githubusercontent.com/17323363/176061836-422007e5-3746-407e-8fc8-488cf3e6f24e.png)

#### Next, we will practice using a set of common Linux commands. Push 'Enter' after each of the following commands to execute them.

1.	First, use the following command to list all of the contents of the current directory.
<!-- -->
    ls
   
2.	Next, to read the document that is present in your current directory use the following comamand.
<!-- -->   
    less README-cloudshell.txt

3.	When you are done reading the text file type the following.
<!-- -->
    q
    
4.	To make a new folder, which we call a directory, called ‘lab1’ use the following command. 
<!-- -->
    mkdir lab1
    
5.	To move into the new directory, use the change directory command.
<!-- -->
    cd lab1
    
note: to move up a directory type: cd ..  
note 2: you may also give a specific location when using cd, like so: cd home/user/lab1

6. For the final command in this section, we will use a command to print text to standard out. 
<!-- -->
    echo ‘hello world!’

#### Next, we will use a built-in text editor called nano and create fasta files, a common file format for storing sequence data. We will then manipulate the fasta files using a series of commnads.

1. First, create a file called 'L_columbiana.ITS.fasta' using nano. 'L columbiana' stands for *Letharia columbiana* and ITS stands for nuclear ribosomal Internal Transcribed Spacer, a gene region that is frequently used for DNA barcoding and phylogenetics in fungi.
<!-- -->
    nano L_columbiana_ITS.fasta
    
2.	Paste the following text into the console:

>Letharia_columbiana_ITS
TTACCGAGAGAGGGGCTCCGCGCTCCCGGGGGTTTCGGCCCCCAACTCTTCACCCGTTGCCTATCGACCTTTTGTTGCTTTGGCGGGCCCCGGGGTCTCCCCGCGCCGGCTTCCGGGCCGGTGAGCGCCCGTCGGAGGCCCATTAAAATCTGTTTCAATCAGTGACGTCCGAGTAAAAACACAATMGTAAAAACTTTCAACAACGGATCTCTTGGTTCCAGCATCGATGAAGAACGCAGCGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACGCACATTGCGCCCCTCGGTATTCCGGGGGGCATGCCTGTTCGAGCGTCATTGCACCCCTCAAGCGTAGCTTGGTATTGGGTCTTCGCCCCCGCGGCGTGCCCGAAAATCAGTGGCGGTCCGGTGTGACTTTAAGCGTAGTAAATTTTCGTCCGCTTTGAAAGTCCGCGCCGTGGCCGGCCAGACAACCCCCTCTATTTCAATAATTGACCTCGGATCAGGTAGGGATACCCGCTGAACTTAA

3.	Check that the text looks correct. Then, exit nano by holding down CTRL+x. You will be asked if you want to save your changes. Push ‘y’ to save the text. Push enter when you are asked if you would like to save it to the file name ‘L_columbiana_ITS.fasta’

4.	Make a second file called L_vulpina_ITS.fasta using the same set of commands as above, and the sequence below. 

>Letharia_vulpina_ITS
AAGGATCATTACTGAGAGAGGGGCTTCGCGCTCCCGGGGGTTTCGGCCCCCAACTCTTCACCCATTGCAACCTACCTTTGTTGCTTTGGCGGGCCCCGGGGGTCTCCCCGCGCTGGCTTTCGGGCCGGTGAGCGCCCGTCGGAGGCCCATTAAAATCTGTTTCAATCAGTGACGTCCGAGTAAAAACACAATAGTAAAAACTTTCAACAACGGATCTCTTGGTTCCAGCATCGATGAAGAACGCAGCGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACGCACATTGCGCCCCTCGGTATTCCGGGGGGCATGCCTGTTCGAGCGTCATTGCACCCCTCAAGCGTAGCTTGGTATTGGGTCCTCGCCCCCGCGGCGTGCCCGAAAATCAGTGGCGGTCCGGTGTGACTTTAAGCGTAGTAAATTTTCGTCCGCTTTGAAAGTTCGCGCCGTGCCCGGCCAGACAACCCCCCCCTATTTCAATAATTGACCTCGGATCANGTAGGGATACCCGCTGAACTTAA

5.	You can view these files using the less command or edit them further using nano.

6.	You may want to combine these files into one file. To do so use the cat command.
<!-- -->
    cat L_columbiana_ITS.fasta L_vulpina_ITS.fasta

You will notice that the output of this command ends up printing the concatenated file content to your console standard output.

7.	Now, if you want to concatenate them and keep the merged data in a new file you can use the same command, then redirect it to a new file using the following command. 
<!-- -->
    cat L_columbiana_ITS.fasta L_vulpina_ITS.fasta > Letharia.fasta

8.	Now, take a look at your new file using the less command.

9.	Sometimes you need to search for specific text within a file. A very handy command for doing this is grep. There are many options that you can use with grep to do more sophisticated searches. For now, we will keep it simple with the following command. 
<!-- -->
    grep ‘>’ Letharia.fasta

10.	We can string multiple commands together using a pipe, represented by this symbol: ‘|’. For instance, you could string together your previous two commands like so
<!-- -->
    cat L_columbiana_ITS.fasta L_vulpina_ITS.fasta | grep ‘>’


nano - a simple text editor that can be used in the console  
cat - concatenates (i.e., sticks together) the contents of multiple files  
ls = list files in a directory  
less = shows the contents of a filed one page at a time  
echo = prints text or string data in standard out  
cd = change directory  
mkdir = make a directory  
