#Large-scale Bayesian variable selection for R and MATLAB
 
###Introduction

We introduce *varbvs*, a suite of functions writen in R and MATLAB for
analysis of large-scale data sets using Bayesian variable selection
methods. To facilitate application of Bayesian variable selection to a
range of problems, the *varbvs* interface hides most of the
complexities of modeling and optimization, while also providing many
options for adaptation to range of applications. The *varbvs* software
has been used to implement Bayesian variable selection for large
problems with over a million variables and thousands of samples,
including analysis of massive genome-wide data sets.

The MATLAB interface has been tested in version 8.6.0 (2015b). The R
package has been tested in version R versions 3.3.1 and 3.3.2.

If you find that this software is useful for your research project,
please cite our paper:

Carbonetto, P., and Stephens, M. (2012). Scalable variational
inference for Bayesian variable selection in regression, and its
accuracy in genetic association studies. *Bayesian Analysis* **7**,
73--108.

###License

Copyright (c) 2012-2016, Peter Carbonetto.

The *varbvs* source code repository by
[Peter Carbonetto](http://github.com/pcarbo) is free software: you can
redistribute it under the terms of the
[GNU General Public License](http://www.gnu.org/licenses/gpl.html). All
the files in this project are part of *varbvs*. This project is
distributed in the hope that it will be useful, but **without any
warranty**; without even the implied warranty of **merchantability or
fitness for a particular purpose**. See file [LICENSE](LICENSE) for
the full text of the license.

###Quick start for R

Begin by downloading the github repository for this project. The
simplest way to do this is to [download the repository as a ZIP
archive](http://github.com/pcarbo/varbvs/archive/master.zip). Once
you have extracted the files from the compressed archive, you will see
that the main directory has two subdirectories, one containing the
MATLAB code, and the other containing the files for the R package.

Subdirectory [varbvs-R](varbvs-R) has all the necessary files to build
and install a package for R. To install this package, follow the
[standard instructions](http://cran.r-project.org/doc/manuals/R-admin.html)
for installing an R package from source. On a Unix or Unix-like
platform (e.g., Mac OS X), the following steps will install the R
package:

    mv varbvs-R varbvs
	R CMD build varbvs
	R CMD INSTALL varbvs_2.0.0.tar.gz

Once you have installed the package, load the package in R by typing
<code>library(varbvs)</code>. To get an overview of the package, type
<code>help(package="varbvs")</code>. The most important function you
will use is the varbvs function, and type <code>help(varbvs)</code> to
get more information about this function.

We have provided several R scripts in the
[vignettes](varbvs-R/vignettes) folder that illustrate application of
*varbvs* to small and large data sets.

Script [demo.qtl.R](varbvs-R/vignettes/demo.qtl.R) demonstrates how to
use the varbvs function for mapping a quantitative trait in a small,
simulated data set. Script [demo.cc.R](varbvs-R/vignettes/demo.cc.R)
demonstrates mapping of a binary trait in a simulated data set.

Script [demo.leukemia.R](varbvs-R/vignettes/demo.leukemia.R)
application of *glmnet* and *varbvs* to the Leukemia data set. The
main aim of this script is to illustrate some of the different
properties of varbvs (Bayesian variable selection) and glmnet
(penalized sparse regression). This script also reproduces the results
and graphs presented in the first example of Carbonetto et al (2016).

Script [demo.cfw.R](varbvs-R/vignettes/demo.cfw.R) demonstrates varbvs
for mapping quantitative trait loci in a large data set outbred mice.

phenotypes measured in CFW (Carworth Farms White) #
outbred mice. Phenotypes include muscle weights (EDL and soleus #
muscle) and testis weight measured at sacrifice.

Scripts [demo.cd.R](varbvs-R/vignettes/demo.cd.R) and
[demo.cytokine.R](varbvs-R/vignettes/demo.cytokine.R) show how the
*varbvs* package can be applied to a very large data set to map
genetic loci contributing to human disease risk. Although these
scripts cannot be executed because we cannot share the data, we have
included them in the R package since it is useful to follow the steps
presented in these scripts.  These scripts reproduce some of the
results and figures presented in Carbonetto et al (2016).

Once you have installed and loaded the **varbvs** package, start by
running the demonstration script with **demo(example1)**. This script
demonstrates how the variational inference algorithm is used to
compute posterior probabilities for a small linear regression example
in which only a small subset of the variables (single nucleotide
polymorphisms, or SNPs) has affects the outcome (a simulated
quantitative trait). 

###Quick start for MATLAB

Begin by downloading the github repository for this project. The
simplest way to do this is to [download the repository as a ZIP
archive](http://github.com/pcarbo/varbvs/archive/master.zip). Once
you have extracted the files from the compressed archive, you will see
that the main directory contains two subdirectories, one for the
MATLAB functions, and one for the R code.

Next you will need to compile the C code into MATLAB executable
("MEX") files. To do this, you will need to have a [C compiler
supported by
MATLAB](http://www.mathworks.com/support/compilers/current_release/),
and you will need to configure MATLAB to build MEX files. See [this
webpage](http://www.mathworks.com/support/tech-notes/1600/1605.html)
for details. When you follow this step, it is important that you
configure MATLAB so that it uses the version of the C compiler that is
compatible with your version of MATLAB. Otherwise, you will encounter
errors when building the MEX files, or MATLAB may crash when
attempting to run the examples. If you run into these problems, you
may have to run the mex command with the -v flag to check what
compiler is being used, and you may have to edit the MEX configuration
file manually.

To build the necessary MEX files, run the
[install.m](MATLAB/install.m) script in MATLAB.

Note that the beginning of this script sets some compiler and linker
flags. These flags tell the GCC compiler to use the ISO C99 standard,
and to optimize the code as much as possible. However, these flags may
not be relevant to your setup, especially if you are not using
[gcc](http://gcc.gnu.org). To avoid errors during installation, if you
are using a compiler other than GCC, it may be best to set variables
**cflags** and **ldflags** to empty strings before running the
[install.m](MATLAB/install.m) script.

If you modify the installation procedure to fit your compiler setup,
it is important that you define macro MATLAB_MEX_FILE, akin to the
\#define MATLAB_MEX_FILE directive in C. In GCC, this is accomplished
by including flag -DMATLAB_MEX_FILE when issuing the commands to build
MEX files.

Once you have built the MEX files, start by running the script
[example1.m](MATLAB/example1.m). This script demonstrates how the
variational inference algorithm is used to compute posterior
probabilities for a small linear regression example in which only a
small subset of the variables (single nucleotide polymorphisms, or
SNPs) has affects the outcome (a simulated quantitative trait). In
this small example, the variational estimates of the posterior
probabilities are compared with estimates obtained by MCMC
simulation. Notice that it takes a considerable amount of time to
simulate the Markov chain.

###Credits

The *varbvs* software package was developed by:<br>
[Peter Carbonetto](http://www.cs.ubc.ca/spider/pcarbo)<br>
Dept. of Human Genetics, University of Chicago<br>
and AncestryDNA, San Francisco, California<br>
2012-2016

Other major contributors to this software include Xiang Zhu and
Matthew Stephens.
