# FAQ

## General
**1) Where can I access the latest SCI-VCF source code?**

You can access the source code via the GitHub <a href="https://github.com/HimanshuLab/SCI-VCF" target="_blank">link.</a>


**2) How can I report bugs and suggest improvements in SCI-VCF?**

You can post your bugs and suggestions <a href="https://github.com/HimanshuLab/SCI-VCF/issues" target="_blank">here.</a>


**3) How do I site SCI-VCF?**

Venkatesh Kamaraj, and Himanshu Sinha. "SCI-VCF: A cross-platform GUI solution to Summarise, Compare, Inspect, and Visualise the Variant Call Format," 2024. https://doi.org/10.1101/2023.08.09.552664

## Installation

### Conda

**4) How to install SCI-VCF in Windows OS using conda?**

Step 1. Install WSL. [Documentation](https://docs.microsoft.com/en-us/windows/wsl/install) <br>
Step 2. Install Miniconda inside WSL. [Reference](https://educe-ubc.github.io/conda.html) <br>
Step 3. Install MobaXterm Home edition. It is a free software that offers an enhanced terminal for Windows with an X11 server. [Documentation](https://mobaxterm.mobatek.net/download.html) <br> 
Step 4. Open a WSL terminal inside MobaXterm (Open MobaXterm --> Click on Sessions --> New Sessions --> WSL --> Select Linux distribution --> OK)
Step 5. Follow the instructions for *Conda-based installation* on the [installation](installation.md) page  


### Docker

**5) How to run the Docker container as a detached backend job and keep SCI-VCF always active?**

Run the docker image in detached mode.
```
sudo docker run -d --rm -p 3000:3000 venkatk89/sci-vcf
```
Now, SCI-VCF will always be active at ```http://0.0.0.0:3000/```

**6) How to solve ‘docker: Got permission denied while trying to connect to the Docker daemon socket at unix’ error while installing SCI-VCF with Docker?**

Add your user to the ```docker``` group

```
sudo usermod -a -G docker username
```

If the issue persists, the socket file can be made available to everyone instead of just the users in the ```docker``` group.

```
sudo chmod 666 /var/run/docker.sock
```


**7) How to solve ‘xhost: unable to open display “:0”’ while Docker installation of SCI-VCF?**
```
xhost local:docker
```


## Customization

**8) How to increase the default upload size?**

*Note: File upload size cannot be altered in the online version of SCI-VCF. It can only be done in the local/remote installation/deployments.*

Open ```R/global.R``` file in RStudio. Go to Line #27
```
#set maximum file upload size in Shiny to 1 GB
options(shiny.maxRequestSize = 1 * 1024^3) 
```
Edit the upload file size according to your requirements.

**9) How to change the default file processing steps?**
Open ```R/summarize_vcf.R```. Go to Line #4
```
break_multiallelic_sites = TRUE, remove_duplicated_entries = TRUE
```
Disable the parameters according to your requirements.


## Output VCF files
**10) Issues with SCI-VCF outputted VCF files?**

While the VCF format is conserved in the output file, the compression algorithm used is parallelized and is not gzip-based. Recent VCF processing software requires their input VCF files to be gzipped. To overcome this, decompress and recompress the SCI-VCF output VCFs using a gzip-based compressing algorithm:

```
gunzip sci-vcf_output.vcf.gz
```

```
gzip sci-vcf_output.vcf
```