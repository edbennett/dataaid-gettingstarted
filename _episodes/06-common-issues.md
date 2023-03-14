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

