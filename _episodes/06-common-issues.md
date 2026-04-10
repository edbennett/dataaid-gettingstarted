---
title: "Common issues"
teaching: 5
exercises: 0
questions:
- "What issues do people frequently encounter?"
objectives:
- "Be able to identify if a problem they are having has been seen before, and resolve it themselves if so"
keypoints:
- "There are some issues that other people have seen. Their resolutions are listed here."
---

## I don't have a home directory on `/cdt_storage`

This is created automatically when you log in to the storage gateway server.

Follow the steps at the bottom of [the episode on SSH keys](02-ssh-keys) to log in to that server.

## I get a "socket creation failed" error

There are a couple of possible reasons for this:

* If you're running on windows, then your scripts contain Windows line endings that Bash doesn't understand. From inside the Sunpyter directory, try running

      dos2unix *.sh
      
  and then re-running Sunpyter.

* If you're running on Windows, then your Sunpyter directory may be on a directory that doesn't have Unix permissions available. To check this, from inside the Sunbird directory, try running

      ls -ld .

  If you see `rwxrwxrwx`, then you are most likely running on a non-Unix filesystem. Try cloning Sunpyter into your home directory instead.

## Sunpyter is stuck at "Waiting..." forever

Many errors can cause this, mostly in `remote_script.sh`.

Use `Ctrl+C` to break out of Sunpyter, and use

    cat jupyter_log.txt

to get more details on the specific error.

Another thing to check is to log in to SUNBIRD and run `squeue --me`.
If you see multiple jobs labeled `SUNPYTER`,
then the problem is that you have a dangling Sunpyter instance.
To avoid accidentally consuming all the resources on the system,
only one Sunpyter job is allowed to run at a time.
Use `scancel [jobid]` to kill all `SUNPYTER` jobs in the queue
and restart Sunpyter.

## Sunpyter is breaking for me and want to create an SSH tunnel by hand

Providing a complete guide to this in an FAQ is hard
(which is why we try to use Sunpyter
rather than walking you through the length tunnel process),
but the basic steps that you need to do:

- Start a job on SUNBIRD on one of the CDT nodes
- Start Jupyter inside this job,
  on the compute node
- Note the node name the job is running on
  (e.g. `scs0151`),
  and the port that Jupyter says it is listening on
  (e.g. `8892`)
- Create a `LocalForward` SSH tunnel between a free port on your machine
  (e.g. 8895)
  and the Jupyter port on the compute node.
  This will look something like:

  ```
  ssh -J z.your.username@sa2c-backup.swansea.ac.uk -J z.your.username@sunbird.swansea.ac.uk -L8895:localhost:8892 scs0151
  ```
- Point your browser at e.g. `https://localhost:8895`
- Once you are finished,
  terminate the job running on SUNBIRD.

All of these steps are done automatically by Sunpyter,
so you might try reading through the source code to see exactly how it does each.
