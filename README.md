<!-- badges: start -->
[![R build status](https://github.com/ratkovic/PLCE/workflows/R-CMD-check/badge.svg)](https://github.com/ratkovic/PLCE/actions)
<!-- badges: end -->

# PLCE: Software for Estimating the Partially Linear Causal Effect Model

This software is used to estimate the average effect of a treatment variable on an outcome, after controlling for background covariates.  Unlike the standard regression model, the proposed method combines a machine learning method to control for the background covariates while using a regression on the treatment variable of interest.  

The method, the Partially Linear Causal Effect (PLCE) model, models both the treatment and the outcome variable, returning a causal effect of the treatment on the outcome under the assumption that there are no omitted confounders and the treatment is random. The method handles random effects, incorporates a set of sensitivity analyses and, as shown in the accompanying manuscript, outperforms several existing method that use machine learning for causal inference.

For more details, see  [Ratkovic (2021)](https://scholar.princeton.edu/sites/default/files/plce_round3.pdf).

## Docker Image

Running the Docker image of an Rstudio server with the package already installed is the recommended way to use this package. If you have not yet installed Docker Desktop, do so [here](https://www.docker.com/products/docker-desktop/). After installing Docker, the image can be pulled from Docker hub in a terminal with:

```
docker pull mannheimsds/plce
```

Then, after ensuring to replace the `plce_data_path/` with your own path to your data that you would like to work with, run a container of the Docker image:

```
docker run -d -p 8787:8787 --mount type=bind,source="plce_data_path/",target=/home/rstudio/plce_data -e PASSWORD=rstudio mannheimsds/plce
```

The Rstudio server will then be run locally at http://localhost:8787/, with the default user and password both being `rstudio`.

## Installation 

The latest version can also be installed in R by:
```R
devtools::install_github('ratkovic/PLCE')
```


## Troubleshooting installation

The software relies on `C++` code integrated into the `R` code through the `Rcpp` package.  If the software does not run on your machine, it may be fixed by ensuring that your compilers are set up properly.

This advice below comes from `KRLS` by Hazlet and Sonnet [(link)](https://github.com/lukesonnet/KRLS).

#### Windows
If you are on Windows, you will need to install [RTools](https://cran.r-project.org/bin/windows/Rtools/) if you haven't already. If you still are having difficulty with installing and it says that the compilation failed, try installing it without support for multiple architectures:
```R
devtools::install_github('ratkovic/PLCE', args=c('--no-multiarch'))
```

#### Mac OSX

In order to compile the `C++` in this package, `RcppArmadillo` will require you to have compilers installed on your machine. You may already have these, but you can install them by running:

```bash
xcode-select --install
```

If you are having problems with this install on Mac OSX, specifically if you are getting errors with either `lgfortran` or `lquadmath`, then try open your Terminal and try the following:

```bash
curl -O http://r.research.att.com/libs/gfortran-4.8.2-darwin13.tar.bz2
sudo tar fvxz gfortran-4.8.2-darwin13.tar.bz2 -C /
```

Also see section 2.16 [here](http://dirk.eddelbuettel.com/code/rcpp/Rcpp-FAQ.pdf)
