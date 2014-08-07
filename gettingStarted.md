---
layout: default
title: "Getting Started"
---

# First things first

Make sure you have the [Prerequisites](prereqs.html) installed.

These instructions assume you will be running the various CS Commons tools from a Unix shell (such as Terminal in Mac OS, Cygwin Terminal in Windows, etc.)

These instructions also assume some familiarity with [Git](http://git-scm.com).  The [Git Documentation](http://git-scm.com/documentation) page is a good place to start.  In addition, there are lots of other good online books and tutorials for learning about Git.

# Installing the cs-commons script

CS Commons provides a Ruby script, called `cs-commons`, which automates the creation and maintenance of CS Commons sites and artifacts.

To install this script, run the following commands:

    cd $HOME/bin
    wget https://raw.githubusercontent.com/cs-commons/cs-commons-scripts/master/cs-commons
    chmod a+x cs-commons

These commands assume that your $HOME/bin directory is on your executable PATH.

Once the script is installed, you can get an overview of its commands by running

    cs-commons help

# Creating a site

First: create a public Git repository for your site.  We highly recommend using [GitHub](https://github.com): hosting your repository on GitHub will allow you to automatically publish your site using [GitHub Pages](https://pages.github.com/).

<div class="callout">
<b>Important!</b> If you create your public repository using GitHub, make sure that the description of your repository contains the text <code>(cs commons)</code>.  Note that the parentheses should be included.  For example, a good description might be something like <blockquote><code>CS 101, Fall 2014 at Unseen University (cs commons)</code></blockquote>  Adding the text <code>(cs commons)</code> to the description tags the repository as being part of CS Commons, and enables your repository to be found in searches for CS Commons content.
</div>

Make a note of the Git URL of the repository you created.

In the example below, we'll assume that we've created a public Git repository called `cs101-fall2014` with the Git URL `git@github.com:pstibbons/cs101-fall2014`.

Run the commands:

<pre>
cd $HOME/git
cs-commons create-site <i>sitename</i>
</pre>

Replace *sitename* with the name of the repository you created.  For example:

    cd $HOME/git
    cs-commons create-site cs101-fall2014

The `create-site` command will prompt you to enter some information about the site you are creating, starting with the Git URL of your public Git repository.  Example run (user input in **bold**):

<pre>
Git repository URL: 
=> <b>git@github.com:pstibbons/cs101-fall2014</b>
You're using GitHub, excellent.  I can infer the website
and public repository URLs.
Public URL of Git repository (default: https://github.com/pstibbons/cs101-fall2014): 
=> 
URL where site will be hosted (default: http://pstibbons.github.io/cs101-fall2014): 
=> 
Title to display on index page
=> <b>CS 101, Fall 2014</b>
Copying js/cs-commons.js...done
Copying css/site.css...done
Copying &#95;layouts/default.html...done
Copying &#95;layouts/fragment.html...done
Creating &#95;config.yml...done
Creating index.md...done
Creating .gitignore...done
Creating cs-commons-site.json...done
</pre>

The public repository URL is the URL of a webpage containing an overview of your Git repository.  The website URL is the URL of the website where the site will be hosted.  If you are using GitHub, `cs-commons` will infer both of these automatically.

# Previewing your site

Once your site has been created, you can run Jekyll to preview it:

<pre>
cd $HOME/git/<i>sitename</i>
cs-commons preview
</pre>

replacing *sitename* with the name of the directory containing your site.

In your web browser, enter the URL `http://localhost:4000`.  You should see the home page of your site.  The `cs-commons preview` command runs Jekyll in server mode, and it will automatically regenerate your site as you edit files: just refresh the web browser to see your changes.

Type Control-C in the window where Jekyll is running to shut down Jekyll.

# Site checkin

The `cs-commons create-site` command only creates a local site that is not connected to a public Git repository.  To connect your local site to the public Git repository, run the following command from the local site directory:

    cs-commons checkin

The `cs-commons checkin` command will create a local Git repository, connect it to your public Git repository, and push the initial content of your local site to the public repository.  Example run (user input in **bold**):

<pre>
Finding files to check in...done
Creating empty git repository...done
Setting default branch to gh-pages...done
Adding files...done
Running git status to confirm files to be added:
# On branch gh-pages
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#	new file:   .gitignore
#	new file:   _config.yml
#	new file:   _layouts/default.html
#	new file:   _layouts/fragment.html
#	new file:   cs-commons-site.json
#	new file:   css/site.css
#	new file:   index.md
#	new file:   js/cs-commons.js
#
If you want to make adjustments to the files to be added,
I can run a shell for you.
Would you like to start a shell? (yes/no) 
=> <b>no</b>
Committing files...done
Setting origin...done
Pushing to origin...done
Checking repository description for (cs commons) tag...done
</pre>

At this point, if you are using GitHub, you should be able to do something very exciting: see your published site!  In your web browser, open the URL <code>http://<i>username</i>.github.io/<i>sitename</i></code>, where *username* is the GitHub user or organization which owns the public Git repository, and *sitename* is the repository name.  In the example above in the "Creating a site" section, the website URL would be `http://pstibbons.github.io/cs101-fall2014`.

Note that it might take a few minutes before the site appears.

# Adding content

A CS Commons site is just a Jekyll website.  Jekyll uses [Markdown](http://daringfireball.net/projects/markdown/) as its markup language.  For example, your site will have a file `index.md` that is the Markdown source from which your site's start page is generated.  Try editing this file, then preview it using the `cs-commons preview` command.

You can (and should!) add other pages to your site.  You can add graphics.  You can modify the site's CSS styles to customize its appearance.

A good way to get a sense of how you can customize your own site is to look at the [Example Site](http://cs-commons.github.io/example-site).  It is hosted in a public GitHub repository: `https://github.com/cs-commons/example-site`.  You can use git clone to make a local copy:

    cd $HOME/git
    git clone https://github.com/cs-commons/example-site

# Publishing updated content

As you change the content of your site, use `git` to commit and push changes to your public Git repository.  If you are using GitHub, then your changes will automatically be published to your repository's GitHub Pages site.


<!-- vim:set wrap: ­-->
<!-- vim:set linebreak: -->
<!-- vim:set nolist: -->
