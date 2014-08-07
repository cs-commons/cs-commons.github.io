---
layout: default
title: "CS Commons Prerequisites"
---

# Required software

To work with CS Commons sites and artifacts, you need the following software installed:

* [Ruby](https://www.ruby-lang.org/en/)
* [Jekyll](http://jekyllrb.com/)
* [Git](http://git-scm.com/)

Ruby, Jekyll, and Git should be available from whatever software package manager you're using.  Here are some examples for specific systems:

## Debian and Ubuntu Linux

Run the following command:

    sudo apt-get install ruby jekyll git

(If you are running Debian and you don't have `sudo` installed, run the above command without `sudo` in a root shell.)

## Other flavors of Linux

Use your package manager to install Ruby, Jekyll, and Git.

## Windows

See the Jekyll on Windows page:

* <http://jekyllrb.com/docs/windows/>

The best option is probably [Cygwin](http://cygwin.com).  From the Cygwin setup program, install the `git` package from the Devel category, and the `ruby` package from the `Ruby` category.

Some web pages for installing Jekyll on Cygwin:

* <http://matt.scharley.me/2012/03/10/windows-cygwin-and-jekyll.html>
* <http://www.4thinker.com/ruby-on-cygwin.html>

## MacOS X

The generic Jekyll installation instructions should work fine:

* <http://jekyllrb.com/docs/installation/>

# Configuring Git

If you have just installed Git for the first time, you should configure it with your identity:

<pre>
git config --global user.name '<i>your name</i>'
git config --global user.email '<i>your email address</i>'
</pre>

Replace *your name* and *your email address* as appropriate.

# Adding an SSH key

If you are using GitHub (you should be!), make sure you have SSH authentication set up.

If you already have an SSH keypair, upload your public key to your GitHub account.  (From your GitHub account page, choose `Account settings` and then `SSH keys`, and upload your public key.

If you need to create an SSH keypair, run the command:

    ssh-keygen -t rsa -b 2048

Upload the file `$HOME/.ssh/id_rsa.pub` to your GitHub account as described above.
