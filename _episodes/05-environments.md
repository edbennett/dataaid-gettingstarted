---
title: "Environments and packages"
teaching: 5
exercises: 0
questions:
- "How can I install packages to be accessible during the workshop?"
objectives:
- "Be aware of the various available environments and able to install packages to them"
keypoints:
- "In addition to the base Supercomputing Wales environment, and the shared environment that Sunpyter defaults to using, there are specific environments available for the three teams that you have the ability to make changes to."
- "You can also create new environments and make them available in the Jupyter server that Sunpyter creates."
---

The default "Python 3" notebook Sunpyter creates uses the environment that it is launched from, which is shared between everyone at the workshop. In order to prevent changes that break other users' workflows, this environment is read-only. Of course, during the workshop you may need to install additional packages needed for the work you're trying to do.

## Team kernels

However, you can also see separate notebook kernels for each team. These make use of separate Conda environments that have write access enabled, so you can install (and remove) packages in them.

Because installing packages requires an internet connection, and there is no internet connection on any of Sunbird's compute nodes, you will need to log in to Sunbird in order to make changes. To activate the environment to make changes, in a new terminal on your own machine:

~~~
$ ssh your.scw.username@sunbird.swansea.ac.uk
$ module load anaconda/2020.07
$ source activate /scratch/s.michele.mesiti/DataAidCondaEnvs/ENVNAME
~~~
{: .language-bash}

Replace `ENVNAME` with the name of the environment you want to use&mdash;either `ChanceToShine`, `DianaAward`, or `Fairtrade`.

Now, you can use `conda install`, or `pip install`, as you prefer, to manage the packages in this environment. (Note that `conda` and `pip` don't always interact well, so stick with one or the other if possible.)

## Private kernels

If you want, you can also create your own Conda environments and make use of them within Sunpyter.

To create a Conda environment, follow the instructions at the [Supercomputing Wales tutorial](https://supercomputingwales.github.io/SCW-tutorial). Then, with this environment active, install the `ipykernel` package, and then run

~~~
$ python -m ipykernel install --user --name=myEnv
~~~
{: .language-bash}

This will create a new kernel visible in the notebook server that will run in the environment that you've just created for yourself.
