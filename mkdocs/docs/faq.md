# FAQ

## General
**1) Where can I access the latest SCI-VCF source code?**

You can access the source code via Github <a href="https://github.com/HimanshuLab/SCI-VCF" target="_blank">link.</a>


**2) How can I report bugs and suggest improvements in SCI-VCF?**

You can post your bugs and suggestions <a href="https://github.com/HimanshuLab/SCI-VCF/issues" target="_blank">here.</a>

## Installation

### Conda

**3) How to install SCI-VCF in Windows OS using conda?**

Step 1. Install WSL. [Documentation](https://docs.microsoft.com/en-us/windows/wsl/install) <br>
Step 2. Install Miniconda inside WSL. [Reference](https://educe-ubc.github.io/conda.html) <br>
Step 3. Install MobaXterm Home edition. It is a free software that offers enhanced terminal for Windows with an X11 server. [Documentation](https://mobaxterm.mobatek.net/download.html) <br> 
Step 4. Open a WSL terminal inside MobaXterm (Open MobaXterm --> Click on Sessions --> New Sessions --> WSL --> Select Linux distribution --> OK)
Step 5. Follow the instructions in *Conda based installation* in the [installation](installation.md) page  


### Docker

**4) How to run Docker container as a detached backend job and keep SCI-VCF always active?**

Run the docker image in detached mode.
```
sudo docker run -d --rm -p 3000:3000 venkatk89/sci-vcf
```
Now, SCI-VCF will always be active at ```http://0.0.0.0:3000/```

**5) How to solve ‘docker: Got permission denied while trying to connect to the Docker daemon socket at unix’ error while installing SCI-VCF with Docker?**

Add your user to the ```docker``` group

```
sudo usermod -a -G docker username
```

If the issue still persist, the socket file can be made available to everyone instead of just the users in the ```docker``` group.

```
sudo chmod 666 /var/run/docker.sock
```


**6) How to solve ‘xhost: unable to open display “:0”’ while Docker installation of SCI-VCF?**
```
xhost local:docker
```


## Customization

**7) How to increase the default upload size?**

*Note: File upload size cannot be altered in the online version of SCI-VCF. It can only be done in the local/remote installation/deployments.*

Open ```R/global.R``` file in RStudio. Go to Line #20
```
#set maximum file upload size in shiny to 1 GB
options(shiny.maxRequestSize = 1 * 1024^3) 
```
Edit the upoad file size according to your requirement.

**8) How to change default file processing steps?**
Open ```R/summarize_vcf.R```. Go to Line #4
```
break_multiallelic_sites = TRUE, remove_duplicated_entries = TRUE
```
Disable the parameters according to your requirement.