---
title: "The filesystem"
teaching: 5
exercises: 0
questions:
- "What data are where?"
- "How can I get files to and from the machine?"
objectives:
- "Be able to find the data on the machine"
- "Be able to use FileZilla to copy files to or from the machine"
keypoints:
- "All files are in `/cdt_storage`, including a user directory, the charity data, and a shared project directory." 
- "Data can be copied to and from the machine with `scp` or FileZilla/WinSCP."
- "The raw charity data must not be copied off the machine." 
---

## Where is everything?

All the files we will work with for this event are located on the CDT storage, which is mounted as `/cdt_storage` on the CDT compute and gateway nodes.

Important places:

* `/cdt_storage/your.scw.username` &ndash;
  your home directory on the CDT gateway node,
  and a place for you to work privately during the event.
* `/cdt_storage/inkinddirect`,
  `/cdt_storage/magicbreakfast`,
  `/cdt_storage/sudep` &ndash;
  the data provided by the charities.
  These directories are read-only,
  to avoid accidentally modifying/deleting the data during the event&mdash;a
  general principle of data analysis is to not modify raw data.
  Under the confidentiality agreement we have signed with the charities,
  these directories (and their contents) **must not** be copied out of the `/CDT_storage` directory,
  either to other Sunbird storage (`/home`, `/scratch`) or to your own computer.
* `/cdt_storage/scw1738` &ndash;
  a shared directory for everyone attending the event to collaborate.
  This contains subdirectories for each of the charities.

## Getting stuff in and out

### git

git is the recommended way to manage your code, and to pull in existing repositories. To activate git on the CDT gateway node, use the command

~~~
$ source /cdt_storage/s.michele.mesiti/activate-git.sh
~~~
{: .language-bash}

You can then use git as normal, with one exception: `git push` is not allowed. Since it is possible that you may accidentally commit part or all of the private data, we request that you keep your work local to the CDT storage until the event is finished, and then we review the repositories before they get pushed anywhere public to ensure that there are no leaks.

### SCP, FileZilla, WinSCP

`scp` (Secure `cp`) is a protocol that lets the `cp` command work over an SSH connection. We won't cover its syntax today, but if you want to use it at some point and need help, then please ask.

FileZilla (Windows, Linux, Mac) and WinSCP (Windows only) are graphical interfaces to SCP. Instructions on how to use FileZilla can be found at the [Supercomputing Wales tutorial](https://supercomputingwales.github.io/SCW-tutorial). Again, the charity data must not be copied off the system, and we request you keep any code committed on the `/cdt_storage` local to that machine until after the event, but you may need to copy up the occasional script, or download an image file to put into a presentation.
