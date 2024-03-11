# Deploy SCI-VCF for communal use

SCI-VCF can be deployed using Shiny-Server for communal use. Sudo access might be required for this purpose. Such a deployment would make SCI-VCF accessible to everyone connected to the institute's intranet.

**Step 1: Install R**

```
sudo apt-get install r-base
```

For installation guidelines, the [documentation](https://cran.r-project.org/) can be followed. 


**Step 2: Install dependencies of SCI-VCF**

```
sudo su - -c "R -e \"install.packages('shiny', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('rmarkdown', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('vcfR', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('here', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('ggplot2', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('scales', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('eulerr', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('dplyr', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('tidyr', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('reshape2', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('shiny', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('shinycustomloader', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('colourpicker', repos='https://cran.rstudio.com/')\""
```
```
sudo su - -c "R -e \"install.packages('plotly', repos='https://cran.rstudio.com/')\""

```

```
sudo su - -c "R -e \"install.packages('htmltools', repos='https://cran.rstudio.com/')\""

```

```
sudo su - -c "R -e \"install.packages('reactable', repos='https://cran.rstudio.com/')\""

```

**Step 3: Install shiny-server**

**Get gdebi to install .deb files**
```
sudo apt-get install gdebi-core
```

**Get the .deb file for shiny-server**
```
wget https://download3.rstudio.org/ubuntu-18.04/x86_64/shiny-server-1.5.20.1002-amd64.deb
```

**Install shiny-server with gdebi**
```
sudo gdebi shiny-server-1.5.20.1002-amd64.deb
```

**Check the status of the shiny-server**
```
systemctl status shiny-server.service
```


**Verify that Shiny has been installed correctly**

Attempt a connection from a different machine on the same network by visiting: ```your.server.ip_address:3838```

<br><br>
**Step 4: Get SCI-VCF from GitHub and alter it**

**Go to the shiny-server location**
```
cd /srv/shiny-server/ 
```


**Get SCI-VCF**
```
sudo git clone https://github.com/HimanshuLab/SCI-VCF
```


**Alter the file structure**
```
sudo rm Dockerfile
sudo rm README.md
sudo rm -r conda/
```


**Move all R files to the main directory**
```
sudo mv R/* ./
```

Delete the empty R directory

```
sudo rm -r R
```

**Change the global.R file**
```
sudo vim global.R
```

Change relative paths of all utilities. 

Change the below code block 
```
source(here("./R/summarize_vcf.R"))
source(here("./R/compare_vcf.R"))
source(here("./R/plot_vcf.R"))
source(here("./R/server.R"))
source(here("./R/ui.R"))
```

to

```
source(here("./summarize_vcf.R"))
source(here("./compare_vcf.R"))
source(here("./plot_vcf.R"))
source(here("./server.R"))
source(here("./ui.R"))
```

<br><br>
**Step 5: Check the deployment**

SCI-VCF will now be available at ```your.server.ip_address/SCI-VCF/```


*Note: For better user experience, the hyperlinks in the tool can also be made to open in a new browser tab*