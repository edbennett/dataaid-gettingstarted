---
title: "Sunpyter"
teaching: 10
exercises: 5
questions:
- "How can I get a Jupyter notebook on Sunbird?"
objectives:
- "Be able to launch a Jupyter notebook via Sunpyter"
keypoints:
- "Use Sunpyter to launch a Jupyter notebook server on the CDT compute nodes"
- "Sunpyter is available from [GitHub][sunpyter], where there is also a README with more troubleshooting information"
---

A common way to use Python to interact with data is via a Jupyter notebook. This combines documentation, code, and output into a single document, viewable via a web browser.

In general, supercomputing centres like their machines to be busy 100% of the time&mdash;otherwise, they could have bought a smaller machine and spent less money. However, the Jupyter notebook method of doing research is interactive, and so spends significant amounts of time idle, doing nothing, and also needs to be available on demand whenever a user wants to use it, meaning that a pool of nodes would need to be kept idle, rather than helping to make progress on the queue of jobs waiting for resources. This tension between what some researchers need and what the most efficient way to use the hardware resource is, is a tension that many supercomputing centres are trying to resolve.

While a final solution is still yet to arrive,
for the time being we have developed a workaround called Sunpyter.
Sunpyter automatically requests that the Sunbird queue manager allocates some compute resources,
launches the Jupyter notebook server on these resources,
creates a tunnel allowing your computer to connect to the notebook server running on the compute node,
and then releases the resources when you terminate the process.

Sunpyter is available from [GitHub][sunpyter].
Clone the repository to your local computer (not to the CDT gateway node).

~~~
$ git clone https://github.com/sa2c/sunpyter
~~~
{: .language-bash}

By default,
Sunpyter is set up to work with the standard Sunbird queues,
not the CDT-specific one we need today.
To fix this,
we need to update the settings in the file `remote_script.sh`.
Using your favourite text editor,
replace the first 19 lines of `remote_script.sh` with the following:

~~~
#!/bin/bash
# Please specify your SCW project account (for example, scwXXXX).
ACCOUNT=scw1738 # Use the Data Aid project account
# Please specify the partition for running Sunpyter.
PARTITION=s_highmem_cdt # Use the CDT nodes

# This lists all the available GPU partitions on Sunbird.
# accel_ai, accel_ai_dev, accel_ai_mig, gpu, s_gpu_eng
# If you don't specify a GPU partition, Sunpyter will run on CPU only.

# Use the conda environment created in the previous episode
CONDA_ENV_PATH=${HOME}/.conda/envs/dataaid

# Ensure the working directory is on the CDT storage.
WORKDIR=/cdt_storage/$USER

# For CPU only.
# Please specify the number of CPU cores you need.
NUM_CPU=1
~~~
{: .language-bash}

Now the settings are set,
we can test that Sunpyter is able to connect to Sunbird without a key
and do what it needs to:

~~~
$ cd sunpyter
$ git pull
$ ./test.sh
~~~
{: .language-bash}

This will spin up its own `ssh-agent` and add your `id_rsa` to it, so you will need to type the password for your key. As the program tells you, if you need to type in your Sunbird password then something has gone wrong, and you should raise a hand and talk to a helper.

Once you know that Sunpyter is able to connect correctly, you can use it to launch a Jupyter notebook server on the CDT nodes.

~~~
$ bash ./sunpyter.sh your.scw.username
~~~
{: .language-bash}

(As always, replace `your.scw.username` with your actual Supercomputing Wales username.) Again, when prompted, enter the passphrase for your private key. At this point, Sunpyter will either open a new browser window pointing at the notebook server, or will present you with a link that you can copy and paste into your browser. Leave the terminal window running&mdash;this is what is maintaining your connection to the notebook server.

> ## Quick checks
>
> Check the following in a Jupyter notebook running through Sunpyter to see that you're running in the right place. You'll need to import the relevant libraries.
>
> 1. What does `socket.gethostname()` return?
> 2. What does `os.cpu_count()` return?
> 3. What does `len(os.sched_getaffinity(0))` return?
> 4. What does `os.getcwd()` return?
>
>> ## Solution
>>
>> 1. This should either be `scs0151` or `scs0152`.
>> 2. This should be 40. Since we only allocate one core for this job, this shows that you can't use `os.cpu_count()` to work out how many CPU cores you can run on when you're on a cluster, since Slurm won't allow you to use that many cores. (If you tried to use 40 separate threads simultaneously, they would all be very slow as they fought for resources.)
>> 3. This, on the other hand, is 1. This unfortunately is not portable, only working on Linux-based systems, but correctly returns the number of cores that the process can actually use.
>> 4. This should start with `/cdt_storage`.
> {: .solution}
{: .challenge}

Once you're finished with Jupyter, then you can return to the terminal and press Ctrl+C to stop the server. It's important to do this, as otherwise the server stays running, and so the resources on Sunbird aren't released for other users.

> ## More power
>
> By default, Sunpyter only allocates 1 CPU for the notebook server. This is because we only have 80 CPU cores across the two CDT nodes, which need to be shared between everyone at the event. If you find during the event that your software is not running quickly enough and would be able to take advantage of multiple cores, then speak to one of the RSEs and we will help identify the best way to scale your resources up without adversely impacting your teammates and the other teams. 
{: .callout}

## Troubleshooting

If you encounter difficulties with Sunpyter, first of all, try a `git pull` of the repository to ensure that you are running the most recent version&mdash;we are regularly updating Sunpyter as we identify areas for improvement, and may have already fixed the issue you are encountering. The next place to check for information is the README, which can be viewed [at the GitHub repository][sunpyter], and is also included in the repository when downloaded. In particular, the "Troubleshooting" section at the bottom has answers to some commonly-encountered issues, and is regularly updated with new issues and fixes as we become aware of them. If your issue is not listed there, then please ask on Slack and the RSE team will help you get things working correctly.

[sunpyter]: https://github.com/sa2c/sunpyter
