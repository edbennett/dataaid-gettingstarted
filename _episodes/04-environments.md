---
title: "Environments and packages"
teaching: 10
exercises: 0
questions:
- "How do I set up Jupyter so I can use Python or R?"
- "How can I install packages to be accessible during the workshop?"
objectives:
- "Be able to create a Conda environment with Jupyter and Python or R installed"
- "Be able to install additional packages into this environment"
keypoints:
- "Use `conda create` to create a new Conda environment."
- "Make sure to include the `jupyter` package, and `irkernel` if you want to use R."
- "Packages can be installed using `conda install`, `pip install`, or `install.packages` in R."
---

Our aim today is that you should be able to work in a Jupyter notebook,
either using Python or R,
to perform your analyses.
Since Jupyter needs to be able to write to certain directories,
the global installation of Anaconda won't work for this,
so instead our first step will be to create our own local installation.

## Creating a Conda environment

We will use Conda to create an environment that holds both the Jupyter server,
and the packages we will install to enable our analyses.

We will create this environment in our home directory on SUNBIRD.
First off,
we need to load a module that will give us access to the `conda` command.
We will do this in the terminal where we connected to SUNBIRD.

~~~
$ module load anaconda/2021.05
$ source activate
~~~
{: .language-bash}

With this done,
we can now create a Conda environment called `dataaid`,
including Python 3.10 and Jupyter.

~~~
$ conda create -n dataaid python=3.10 jupyter
~~~
{: .language-bash}

This may take a minute or two as Conda works out what files it needs,
downloads them,
and puts them all into place.

## Installing packages

Once our environment is created,
we have a variety of ways we can install packages into it.

Since this is an entirely fresh environment,
it won't have any of the packages that you have installed elsewhere&mdash;for
example on your own machine,
or in other environments on SUNBIRD.
So if we want to use any packages outside of the standard library,
we will need to install them.

In all cases,
we will first need to activate this environment.

~~~
$ conda activate dataaid
~~~
{: .language-bash}

We can install packages using `conda`.
For example,
if we want to use R within Jupyter,
we will need to install `r` and `irkernel`.

~~~
$ conda install r irkernel
~~~
{: .language-bash}

If we are using Python,
we can also install packages using `pip`.

~~~
$ pip install numpy matplotlib torch
~~~
{: .language-bash}

If we are using R,
we can start an R command-line session and use `install.packages`.

~~~
$ R
~~~
{: .language-bash}

~~~
> install.packages("tidyverse")
~~~
{: .language-r}


## Adding more packages later

If you find as you are working that you need extra packages,
you might no longer have the terminal open that you used to create the environment.

To get back to where we were,
starting from a terminal on your local machine,
you can first reconnect to SUNBIRD:

~~~
$ ssh your.scw.username@sunbird.swansea.ac.uk
~~~
{: .language-bash}

Then to reactivate the environment:

~~~
$ module load anaconda/2021.05
$ source activate
$ conda activate dataaid
~~~
{: .language-bash}

From there we can install more packages with `conda`, `pip`, or `R`
as we did previously.

> ## Installing packages from within Jupyter
>
> Once we are using Sunpyter
> (see the next section)
> we can also open a terminal from the Jupyter main page,
> by going to `New` > `Terminal`.
> This will be running on the compute node on the cluster,
> so you will be able to install packages from there.
{: .callout}
