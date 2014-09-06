---
layout: default
title: "Specifications"
---

# Introduction

This page has specifications for CS Commons sites and repositories.

The sections titled "Discussion" are not part of the specifications, but are intended to clarify the intent of the specifications.

# File types

In CS Commons sites and artifacts, files with a `.md` file extension are Markdown files.  We recommend the use of [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown).  Because CS Commons sites and artifacts use [Jekyll](http://jekyllrb.com/), all Markdown files must contain YAML front matter.  All Markdown files that are intended to render as web pages must use the `default` layout.

JSON objects are defined by RFC 4627, [The application/json Media Type for JavaScript Object Notation (JSON)](http://www.ietf.org/rfc/rfc4627.txt).

# Sites

A CS Commons site is a Git repository containing a Jekyll website.

We strongly recommend hosting CS Commons sites at GitHub.  A GitHub repository for a CS Commons site must have the string `(cs commons)` in its description.

A CS Commons site must have, in its root directory, a file called `cs-commons-site.json` containing a single JSON object.  The structure of the JSON object is as follows:

> Key | Required? | Type | Description
> --- | --------- | ---- | -----------
> repo\_git\_url | yes | string | Git URL of the site's Git repository
> site\_url | yes | string | URL where the site is hosted
> repo\_pub\_url | no | string | URL of webpage for the site's Git repository
> title | yes | string | The title of the site

A CS Commons site can include any number of CS Commons artifacts as Git submodules.  A site must reference each artifact repository using a public Git URL.  (In other words, it must be possible to gain read access to an artifact repository without providing any credentials.)

A CS Commons site must use JavaScript/ECMAScript to transform HTML elements with the `csc-subst` and `csc-fragment` CSS clases as described in the Artifacts section.  (The [CS Commons template site](https://github.com/cs-commons/template-site) includes code that does this.)

## Discussion

A CS Commons site must be public, but does not need to be published using a permissive license.  Files that are part of a CS Commons site, but are not part of any artifact included in the site, are not necessarily freely redistributable.  However, we strongly encourage creators of CS Commons sites to license the site's files using a permissive license (such as a Creative Commons license).

# Artifacts

A CS Commons artifact is a Git repository containing (at a minimum) three files:

* `index.md`
* `README.md`
* `cs-commons-artifact.json`

All of the above files must be located in the root directory of the artifact.

We strongly recommend hosting CS Commons artifacts at GitHub.  A GitHub repository for a CS Commons artifact must have the string `(cs commons)` in its description.

It may also include any number of additional files.  The additional files may be (but are not required to be) located in subdirectories.

All files that are part of a CS Commons artifact must be made available using a permissive license.  We strongly recommend using one of the [Creative Commons](http://creativecommons.org/) licenses.  We strongly discourage the use of any license that does not allow the creation of derived works.  (For example, do not use any of the "NoDerivatives" Creative Commons licenses.)

A CS Commons artifact is a partial Jekyll site.

## Required files

The `index.md` file is the home page.  All of the artifact's content must be reachable from this file.

The `README.md` file must contain the following information:

* The author or authors of the artifact
* The license under which the artifact is distributed
* A brief description of the artifact
* A list of all substitutions and fragments the artifact provides, and their intended purpose

The `cs-commons-artifact.json` file contains a single JSON object.  The structure of the JSON object is as follows:

> Key | Required? | Type | Description
> --- | --------- | ---- | -----------
> title | yes | string | The artifact's title
> type | yes | string | Artifact type: suggested values are "notes", "slides", "lab", and "assignment"
> authors | yes | array of author objects | The artifact's authors (who are also the artifact's copyright holders)
> license | yes | license object | The license under which the artifact is made available
> keywords | yes | array of strings | Free-form keywords used to describe the artifact: we recommend that keywords do not contain spaces
> repo\_git\_url | yes | string | Git URL of the site's Git repository
> repo\_pub\_url | no | string | URL of webpage for the site's Git repository

The structure of an author object is as follows:

> Key | Required? | Type | Description
> --- | --------- | ---- | -----------
> name | yes | string | Author's full name
> email | yes | string | Author's email address
> website | no | string | Author's website

The structure of a license object is as follows:

> Key | Required? | Type | Description
> --- | --------- | ---- | -----------
> shortname | yes | string | Short license name, e.g., "CC BY-SA 4.0"
> fullname | yes | string | Full license name, e.g., "Creative Commons Attribution-ShareAlike 4.0"
> website | yes | string | URL of website containing complete license terms

## Substitutions and fragments

The YAML front matter of all Markdown files in an artifact must specify a key called `artifact-name`.  The value of this key is the *artifact name*.  The artifact name must consist only of alphabetic characters.  For example, the YAML front matter of the `index.md` file in an artifact whose artifact name is "breakout" might be defined this way:

    ---
    layout: default
    title: "Breakout"
    artifact-name: breakout
    ---

Markdown files in an artifact may contain *substitution* and *fragment* elements.  The content of these elements is not specified by the artifact, but instead is specified by the site when it imports the artifact.

A *substitution* element has the following form:

<pre>&lt;span class="csc-subst" id="<i>identifier</i>"&gt;&lt;/span&gt;</pre>

A *fragment* element has the following form:

<pre>&lt;div class="csc-fragment" id="<i>identifier</i>"&gt;&lt;/div&gt;</pre>

The *identifier* is a unique element id.  It must be a single word consisting of only alphabetic characters.

When a web page generated from an artifact Markdown file, all substitution and fragment elements must be transformed as follows.

For substitution elements, a JSON object must be loaded from the URL (relative to the root of the site)

<pre>subst/<i>artifact-name</i>.json</pre>

where *artifact-name* is the artifact name.  This JSON object has keys corresponding to the identifiers of the substitution elements.  Each substitution element's text is replaced by the value found in the JSON object (by using the element's identifier as a key).

For fragment elements, a document is loaded from the URL (relative to the root of the site)

<pre>subst/<i>artifact-name</i>/<i>identifier</i>.html</pre>

where *artifact-name* is the artifact name and *identifier* is the fragment element's identifier.  The body of the fragment element is replaced with the HTML elements found in the loaded document.

## Discussion

Authors of artifacts should try to choose artifact names that are unlikely to conflict with the names of other artifacts.

It is the responsibility of the site (and specifically, the site's `default` layout template) to transform substitution and fragment elements.
