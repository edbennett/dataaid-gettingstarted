---
title: "SSH keys"
teaching: 10
exercises: 0
questions:
- "How can I access a machine via SSH without a password?"
objectives:
- "Be able to create and use an SSH key pair"
keypoints:
- "SSH keys are files that authenticate you similarly to a password"
- "SSH keys have a public and a private part; the private key must be kept private"
- "SSH keys should be password-protected"
---

When connecting to a remote machine, we use the Secure SHell protocol (SSH) to do so without leaking our private details all over the Internet. If you've been on a Supercomputing Wales course previously, then you will have used this by typing your password to connect. However, there is another option that can be more convenient, and we will need to use in order to use the Sunpyter later this morning.

SSH keys allow you to authenticate to a service without needing to send a password over the network. Instead, you store a "public key" on any machine that you want to be able to connect to, and when you connect, the SSH server verifies that the private key that you hold matches the public key. It does this without the private key ever leaving your computer, making use of cryptographical techniques that are well beyond the scope of this session.

## Creating a key pair 

You may already have an SSH key on your machine.
To check this, open a shell (Git Bash if you are on Windows) and run:

~~~
$ ls ~/.ssh/id_rsa
~~~
{: .language-bash}

If this gives an error, then we need to create one. If it exists, then you can skip this step:

~~~
$ ssh-keygen
~~~
{: .language-bash}

When prompted, save the key in the default location by pressing Return, and then enter a password for the key. No characters will appear on the screen while you type the password; this is normal and avoids showing the number of characters in the password to anyone looking over your shoulder. You need to repeat the password when asked to, to verify that there are no typos.

> ## SSH key passwords
>
> While you may have previously used SSH keys without a password at all for maximal convenience, this creates security holes where anyone who can access a machine that has your private key can jump to any other machine you have access to. This led to the compromise of many UK supercomputers in 2020 to run Bitcoin mining software and potentially steal confidential research data. Supercomputing Wales requires that all private keys used to access the machine be protected by a password.
{: .callout}

You now have (at least) two files in your `~/.ssh` directory: `id_rsa` and `id_rsa.pub`. `id_rsa` is your private key, and should **never** be shared with anyone. Ideally you should never even view it on screen, or copy it to any other machines. Anyone with this key (and the password for it) can log in to any machines you have access to as if they were you.

`id_rsa.pub` is your public key. It acts kind of like a lock, that can be opened by your private key.

> ## GitHub
>
> You can use your SSH key to authenticate to GitHub as an alternative to using HTTPS and your password. To do this, display your **public** key with the command
>
> ~~~
> cat ~/.ssh/id_rsa.pub
> ~~~
> {: .language-bash}
>
> Then go to your [GitHub key settings](https://github.com/settings/keys) and click "New SSH key". Copy and paste the contents of your `id_rsa.pub` into they "Key" field and click "Add SSH key". You will then be able to clone, pull from, and push to repositories using the SSH option shown on repositories' home pages.
{: .callout}

## Logging in to Supercomputing Wales

Now we are ready to use SSH keys to authenticate with Supercomputing Wales. First off, we need to check our username. Visit the [My Supercomputing Wales](https://my.supercomputing.wales) service, and log in with your University credentials. (If you have more than one set, make sure to use the same ones you used in the Setup!)

At the top of the "Account Summary" box on the left is your "SCW username". Make a note of this&mdash;it is likely to be the first letter of your University, followed by your University username. However, that's not guaranteed, so it's good to double-check.

Now, if you have not previously set a password for Supercomputing Wales, you can do this with the "Reset SCW Password" button further down the left-hand side, in the Actions box. Supercomputing Wales machines have a separate password database to the Universities, so this can (and ideally should) be a different password. Since we're using SSH keys, we will not be using this password very much, but you will need to type it in again in a minute or so.

Now, we need to tell the Sunbird machine to let us in_using the key we just created. To do this, we can use the `ssh-copy-id` command.

~~~
$ ssh-copy-id -i ~/.ssh/id_rsa your.scw.username@sunbird.swansea.ac.uk
~~~
{: .language-bash}

Replace `your.scw.username` with the username you noted down from My Supercomputing Wales. You will be prompted for the password for the private key, then to confirm that you want to connect to the machine, and then the Supercomputing Wales password that you just set. You will be temporarily locked out if you enter the wrong password (or username) too many times in a row, so if you get an "Invalid password" message then stop and raise a hand/talk to a helper.

All being well, you will get a message saying that the public key has been copied. To test that this has worked, we can try using it to log in, but first we need to unlock our private key. We do this using an SSH Agent.

~~~
$ eval `ssh-agent`
$ ssh-add ~/.ssh/id_rsa
~~~
{: .language-bash}

When prompted, enter the password for your private key. This then stores the key in memory, so that you can use it without entering your password every time. To test that this has worked, try:

~~~
$ ssh your.scw.username@sunbird.swansea.ac.uk
~~~
{: .language-bash}

Again, replace `your.scw.username` with your username for the Supercomputing Wales services.
You should be let straight in.

> ## Multiple sessions
>
> Note that the way we have invoked it, `ssh-agent` is specific to the current shell session, so if you open a second terminal window you'll need to open a second agent and reload and reauthenticate your key. It is possible to make one agent work across all sessions, but the setup is slightly more involved so is left as an exercise.
{: .callout}

Now, we also need to be able to connect to the CDT gateway server, as the CDT storage is not accessible from the Sunbird login node.

~~~
$ ssh-copy-id -i ~/.ssh/id_rsa your.scw.username@sa2c-backup2.swansea.ac.uk
$ ssh your.scw.username@sa2c-backup2.swansea.ac.uk
~~~
{: .language-bash}
