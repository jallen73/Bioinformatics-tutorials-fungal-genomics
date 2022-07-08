## Tutorial #4 Setting up a virtual machine and installing conda

Virtual machines (VMs) are software-based compute resources that are configured and run independently of the physical machine on which they are running. The VM is the 'guest' and the physical machine is the 'host.' VMs are flexible and effecient for completing specific compute tasks independent of the hardware to which the user has access. A user can design and launch a VM with the exact specifications that they need to accomplish a specific task, thene shut it down once the task is complete. As each new compute task arises a different VM can be built to best serve their needs for each task. 

In this tutorial we will configure a VM on Google Cloud and install conda, a very useful package management system, on it.

#### Build the VM

1. From the main console select ‘Create a VM’

<img src="https://user-images.githubusercontent.com/17323363/176699762-05ead4a1-d8d7-42cc-b23e-29104e4354ec.png" width="400">

2. Then select ‘ENABLE’ when the prompt regarding the Compute Engine API comes up.
                                                                                                                        
<img src="https://user-images.githubusercontent.com/17323363/176699884-326d1165-ffeb-4f2b-a6a1-aafdfb6c140f.png" width="400">

3. Next, we will change a few settings from the default to create a slightly more powerful VM with more storage.
First give your VM a name and select a region from which the VM will be hosted. 
Under ‘Machine Type’ select e2-standard-4

<img src="https://user-images.githubusercontent.com/17323363/176699993-fb779702-80b6-4ef5-956c-96402197bba1.png" width="400">

4. Select boot disk, then change the boot disk size to 15 GB to give yourself plenty of space to work with. Then click ‘Select.’

<img src="https://user-images.githubusercontent.com/17323363/176700065-fbceab34-5807-4e7a-9762-9855a9ae2b6b.png" width="400">

5. Finally, under firewall select Allow HTTP traffic and allow HTTPS traffic. Then click Create.

<img src="https://user-images.githubusercontent.com/17323363/176700118-8af15de6-6b57-4ee8-bec9-5e924fc36d83.png" width="400">

6. You will be automatically redirected to a screen with a list of VMs that you have built. At this point there should just be the one VM. Once the symbol under 'Status' turns into a green circle with a white checkmark the VM is ready to be used. To open a shell for this VM click 'SSH' under connect.

<img src="https://user-images.githubusercontent.com/17323363/176700404-d26c9321-169e-4347-93c8-935b07124182.png" width="400">

#### Install mininconda

1. Navigate to the documentation for conda installation: https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html

2. Click 'Miniconda installer for Linux. 

<img src="https://user-images.githubusercontent.com/17323363/176700792-94dd8c18-aa3d-4f99-acfd-5f8ec38017e3.png" width="400">

3. Then, click 'Miniconda3 Linux 64-bit,' thus initiating the download of file called: Miniconda3-py39_4.12.0-Linux-x86_64.sh

<img src="https://user-images.githubusercontent.com/17323363/176700880-fabdde66-245a-4c85-9fde-ce3720342c1c.png" width="400">

4. Once the file download is complete, upload it to your cloud shell using the up arrow symbol. Choose file and select Miniconda3-py39_4.12.0-Linux-x86_64.sh, which you just downloaded. 

<img src="https://user-images.githubusercontent.com/17323363/176701242-739aa521-0614-422f-9e03-0973733f8bcc.png" width="400">

5. Once the upload is complete run the following command and follow the prompts on the screen through the installation process. 
<!-- -->
        bash Miniconda3-py39_4.12.0-Linux-x86_64.sh
        
 6. Once the installation is complete close and reopen the shell. Check if the installation worked by running the following command.
<!-- -->
        conda list
        
 If conda is correctly installed a list of packages will show up and look like the following screen.
 
 ![image](https://user-images.githubusercontent.com/17323363/176701759-46f776f1-50a1-40fd-853d-61a9ddb544d6.png)
 
 7. Before leaving your computer, **be sure to stop this VM instance so you are not charged for it while nothing is running**. Close the shell and return to the webpage with your VM instance. Click the three vertical dots to the right of the VM instance, then select stop. To confirm that the VM has stopped look for the red circle with a square under status.
 
 ![image](https://user-images.githubusercontent.com/17323363/177423216-9e8c1529-4189-46ee-a978-06db1cad8473.png)

