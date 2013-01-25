
<link href="http://kevinburke.bitbucket.org/markdowncss/markdown.css" rel="stylesheet"></link>

Installing the phyloseq package
========================================================
The following tutorial contains information for installing the phyloseq package for R. It includes details for navigating the various versions of the package that are available, and how to tackle some of the challenges that may come up depending on your operating system and familiarity with R.

# Quick Install
If one of these two methods works with no errors, you're done. The phyloseq package has been installed and you can move on to [the phyloseq tutorials](http://joey711.github.com/phyloseq/). If not, see some of the additional troubleshooting recommendations below. Some of the issues might depend on your system. See if you can install all of the required packages ahead of time before attempting to install phyloseq.

### Bioconductor Release Version
This will not necessarily have the very latest features and fixes, but the installation should work easily using the `biocLite` tool. It should install all the necessary dependencies automatically, so these two lines should be all you need to enter in your R session to install the phyloseq package.


```r
source("http://bioconductor.org/biocLite.R")
biocLite("phyloseq")
```


### GitHub Development Version
This version is updated often, sometimes daily, and includes the latest fixes, documentation, and features. If you've requested a fix or feature on [the phyloseq Issue Tracker](https://github.com/joey711/phyloseq/issues), it will show up in this version first, and might be a while before the changes migrate to the official release version. This delay is for stability, testing, and because Bioconductor is on [a semi-annual release schedule](http://bioconductor.org/about/release-announcements/). This version is a "live" incrementally updated version of the package that we use to save, share, and collaboratively develop the package. For unstable code there are no guarantees. However, we try very hard not to push any changes to the "master" branch (the one that you see by default) that do not meet the same standards as the Bioconductor repository itself. Typically, changes that have not been fully tested will be pushed to a secondary branch or fork, and then merged into "master" only after they have passed the full suite of checks. Thus, in the vast majority of cases you should be able to install from GitHub and get the latest fixes and functionality that will eventually make its way into the Bioconductor release version.

There are many different ways to obtain and install the GitHub version of the phyloseq package. The easiest way is to use the `install_github` function now included in the R development tools package, called [devtools](http://cran.r-project.org/web/packages/devtools/index.html).

First make sure that you have the devtools package installed,


```r
install.packages("devtools")
```


then go ahead and load the devtools package and attempt to install phyloseq with the `install_github` function.


```r
library("devtools")
install_github("phyloseq", "joey711")
```



---
# Core R version number
We are aware of a transient, but recurring error:

	-----------------------------------
	ERROR: dependency 'multtest' is not available for package 'phyloseq'
	-----------------------------------
	In addition: Warning message:
	package 'multtest' is not available (for R version 2.*.*)

This recurring problem arises when a new version of core R is released -- for example [version 2.15.2 was released](http://cran.r-project.org/) on 2012-10-26 -- and any dependencies (see below) have not yet been built under that new version. This will typically create warnings or errors when you attempt to install phyloseq. In most cases this is not the result of the latest R version "breaking" a particular package (that kind of problem is rare); rather, it is most likely an overly cautious versioning check to ensure that the discrepancy does not go unnoticed (or so we guess). Most importantly, it is a *transient* problem that will fix itself as new "pre-built" versions of the packages are re-built with the latest release version of your core R installation. However, if you do not or cannot wait for that to happen, you will need to install those dependencies from source. Not to fear, it is hopefully not as scary as it sounds, and has the exact same challenges as those discussed in the following sections for installing the phyloseq package from source.

For example, the above warning/error is probably solved by first installing the multtest package from source with the following code (note: it is a Bioconductor package, and you must have an active internet connection)


```r
source("http://bioconductor.org/biocLite.R")
biocLite("multtest", type = "source")
```


Similarly, an offending dependency hosted by the CRAN repository could be installed from source with the following code (in this example, the ggplot2 package)


```r
install.packages("ggplot2", type = "source")
```


Note that this assumes that you have the necessary system requirements for building a package from source. This is mainly only an issue for Windows users. If the previous install code failed in your R session, do a google search of the error message that you got back. If that doesn't reveal the solution and you are using Windows, see the section below entitled "Windows Users".

---
# Dependencies
Dependencies are other R packages that are required for proper functioning of phyloseq. They must be installed with at least a minimum version number specified by phyloseq for installation to work. If something went wrong in your installation of phyloseq, making sure you can actually install the dependencies is probably the best place to start. The following dependency installation code will usually attempt to upgrade your packages to the latest versions as well, potentially fixing a dependency version that is too old to work with the latest phyloseq version.

### Bioconductor Dependencies
Installing Bioconductor dependencies is supposed to be painless, and to work the same way as for the "Quick Install" of the release-version of phyloseq above:


```r
source("http://bioconductor.org/biocLite.R")
biocLite("multtest")
```


An explicit way to upgrade your packages using the new Bioconductor package upgrader:


```r
source("http://bioconductor.org/biocLite.R")
biocLite("BiocUpgrade")
```



### CRAN Dependencies
The Comprehensive R Archive Network (CRAN) is the main repository for publicly available R packages. Most installation procedures will install these dependencies automagicaly from [the CRAN repository](http://cran.r-project.org/web/packages/). However, if you want to install them ahead of time, update, or help identify a troublesome dependency, the following section contains the code to install them directly using the core `install.packages` function


```r
install.packages("ape")
install.packages("ade4")
install.packages("doParallel")
install.packages("foreach")
install.packages("ggplot2")
install.packages("igraph0")
install.packages("picante")
install.packages("plyr")
install.packages("RJSONIO")
install.packages("scales")
install.packages("testthat")
install.packages("vegan")
```



---
# Windows Users
There is no way for us to guarantee or troubleshoot all the possible issues that might arise for Windows users, but here is a short list of key recommendations and resources that might help you get going with phyloseq as soon as possible.

- Windows Users may first need to install [the Rtools application](http://cran.rproject.org/bin/windows/Rtools/), depending on how phyloseq is being installed, as Rtools is necessary to build anything from source on Windows. 

- Make sure the R and Rtools [paths are added](http://geekswithblogs.net/renso/archive/2009/10/21/how-to-set-the-windows-path-in-windows-7.aspx) in the environment variable.

- Here are the [official instructions from CRAN for installing R packages on Windows](http://cran.r-project.org/doc/manuals/R-admin.html#Windows-packages).

- For more detailed troubleshooting or system setup for Windows see [Appendix D The Windows toolset](http://cran.r-project.org/doc/manuals/R-admin.html#The-Windows-toolset) published by CRAN.


---
# Manual Download and Local Install
Depending on the problem that you're having, it might help to download a compressed version of the phyloseq package, and then attempt to install it locally with standard R commands/tools.


## Manual [Download from GitHub](https://github.com/joey711/phyloseq/tarball/master)
The `tar.gz` "tarball" of the latest package build can be downloaded by clicking this [phyloseq tarball](https://github.com/joey711/phyloseq/tarball/master) link. Both zipball and tarball versions of the repository are also linked from [the phyloseq front page](joey711.github.com/phyloseq/).

*Note:* The file name will have the form `joey711-phyloseq-*.tar.gz`


## Manual [Download from Bioconductor](http://bioconductor.org/packages/devel/bioc/html/phyloseq.html)
The latest [stable release of phyloseq on Bioconductor](http://bioconductor.org/packages/release/bioc/html/phyloseq.html) and the latest [development release of phyloseq on Bioconductor](http://bioconductor.org/packages/devel/bioc/html/phyloseq.html) can be found at these respective links, as well as some [interesting phyloseq use data](http://bioconductor.org/packages/stats/bioc/phyloseq.html) in the form of the number of downloads of the respective versions each month from Bioconductor.

*Note:* The file name will have the form `phyloseq_1.*.tar.gz`


## Manual [Download from Bioconductor - Devel](http://bioconductor.org/packages/devel/bioc/html/phyloseq.html)
[The development branch of phyloseq on Bioconductor](http://bioconductor.org/packages/devel/bioc/html/phyloseq.html) is updated less often than the GitHub branch, but might contain recently-developed features in phyloseq that have not yet migrated to the release version. This is a good option if you are having problems installing the GitHub version, or have some other reason to use the slower-moving code. 

Download the BioC devel branch of phyloseq [the devel page for phyloseq on Bioconductor](http://bioconductor.org/packages/devel/bioc/html/phyloseq.html). It should be a link to download a file called something like `phyloseq_1.*.*.tar.gz`. Alternatively, you can download package binaries for Windows or Mac OS. These might install easier because you won't need to install "from source".	


## Local Installation

(Assumes you have already downloaded the version of phyloseq that you want to install.)

### Local Install on Mac OS X and Linux/Unix

From a ([BASH](http://en.wikipedia.org/wiki/Bash_(Unix_shell))) command line, unpack and install (assuming you downloaded the package to the `~/Downloads` directory, as an example):

```
cd ~/Downloads
tar -xvf joey711-phyloseq-*.tar.gz
R CMD install joey711-phyloseq-*
```
(You need to replace the `*` or complete file name to match what you actually downloaded and unpacked. The final line refers to the directory you just unpacked, not the compressed file.)

Alternatively, you might be able to build from source from within an R session, as mentioned above


```r
install.packages("~/Downloads/joey711-phyloseq-*", repos = NULL, type = "source")
```



### Local Install on Windows
Make sure you have [Rtools](http://cran.r-project.org/bin/windows/Rtools/) installed.

#### Windows Install Option 1: R command-line (recommended)
From within an R session, enter:

```r
install.packages("C:/Desktop/joey711-phyloseq-*", repos = NULL, type = "source")
```

Where `C:/Temp/` represents the full directory path to where you have saved the `joey711-phyloseq-*.tar.gz` file containing phyloseq.  


#### Windows Install Option 2: Dos
Command-line (dos) installation (only try if Option 1 fails):
- Make sure the R and [Rtools](http://cran.r-project.org/bin/windows/Rtools/) [paths are added](http://geekswithblogs.net/renso/archive/2009/10/21/how-to-set-the-windows-path-in-windows-7.aspx) in the environment variable.
- Open a dos command prompt and enter the following

```
R CMD INSTALL joey711-phyloseq-*.tar.gz`.
```


---
# Install BioC devel branch, automated
The previous options for installation are recommended

There are [official instructions for using development versions of Bioconductor packages](http://bioconductor.org/developers/useDevel/), and these will apply to phyloseq as well as any other package in the BioC-devel repository. However, using their tool, especially the `useDevel()` command, appears to force you to use development versions of all your Bioconductor packages. There are more complicated ways around this requirement described on their page, but the "manual download and local install" instructions above will allow you to get around it. 


---
# Customization

If you want to make modifications to phyloseq on your own fork, and then install from your modified repository, just change the `"joey711"` argument to your GitHub username (and if you named the repository something other than `"phyloseq"`, change that too).
Otherwise, you can follow the instructions above for using the `install_github` command.