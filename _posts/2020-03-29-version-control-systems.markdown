---
layout: post
title:  Version Control Systems
description: Introduction about version control systems used in software development
date:   2020-03-29 18:00:00 +0200
categories: Version-Control VCS
tags: vcs version control systems file git svn mercurial bazaar versioning local centralized distributed decentralized software development
permalink: /article/:title
comments: true
uuid: 7ca6cd36-1cb2-4825-93af-3c8e291b9960
---
**Version Control Systems** (VCS) is a category of software that records changes to a file or set of files over time so that you can recall specific versions later. We are going to talk about the need for VCS, its types and available tools

### Why do I need something like that?

- **Scenario 1**
	 - You are asked to do a software project with a team and you will split the project into tasks to work on it in parallel
	 - After finishing part of the project, you will test what you achieved through integrating parts
	 - Usually, the project does not work
	 - You will solve issues to be able to test their project, then update your local copies of code
	 
 - **Scenario 2**
	 -  You have a file changes frequently and at some point you want to get back to a specific version
	 - You will create a numbered versions of same file

### Let's disccuss these scenarios,
- **First  scenario**, when project getting larger, or expanding team, it will be difficult to maintain project (cases like, you forget to share fix, when you add fix a file contains a new code you added is overwritten, etc.)
- **Second scenario**, you will have a directory for each file contains all versions of that file and this will make structure of files complex in technical and non-technical projects


**Let's think what we need to solve these kind of issues. We need a solution that**
- Keeps the code or file
- Keeps a history of the code or file
- Merges files and handle conflicts (e.g. integrating project for testing)

That's what **Version Control System (VCS)** does :tada:

### Version Control System Types

- Local VCS
- Centralized VCS
- Distributed VCS

***Let's discuss each type of these types***
#### Local VCS
<img  alt="Local Version Control System"  src="/assets/articles/vcs/local-vcs.png" align="center"  class="Screenshot"  width="350"  />

Here, this focused about the second scenario. It keeps a snapshot for each version in a linear history of your files, so when you change file, it creates a new version of it.

#### Centralized VCS
<img  alt="Centralized Version Control System"  src="/assets/articles/vcs/centralized-vcs.png" class="Screenshot"  width="400"  />

Here, this focused about the first scenario. Files are saved in a server containing all versions history. To make edits, you need to get a local copy of latest version and then update server with your edits to create a new version. Server will maintain a linear history of your files. This type will guarantee that there is no conflicts could happen since there is one maintainer (the server) and it makes sure that will not happen

#### Distributed / Decentralized VCS
<img  alt="Distributed Version Control System"  src="/assets/articles/vcs/distributed-vcs.png" class="Screenshot"  width="350"  />

Here, this focused about the first scenario too. Each one holds local copy of files with its versions history (each one could be a server). To make edits, just update files and create a new version on your local copy. You can then update server with new versions you added. Also, you can get only new versions from server if there are

#### Centralized Vs Distributed VCSs

#### Centralized
- Easier to understand
- Everything is controlled from one place
- You need to be connected to server to work on files
- Performance is worse since you need connection to server to get latest version before each edit

#### Distributed
 - Could be confusing in certain cases
 - You can edit directly on your local copy without connection
 - Performance is better as you already have a local copy

#### This is a list of VCSs
 - [Subversion(SVN)](https://subversion.apache.org)
	 - Centralized VCS
	 - **Not** widely used due to its cons
 - [Git](https://git-scm.com)
	 - Distributed VCS
	 - Widely used in software development
	 - Used in Linux Kernel development
 - [Mercurial](https://www.mercurial-scm.org)
	 - Distributed VCS
	 - Currently, used by [Mozilla](https://mozilla.org)
 - [Bazaar](https://bazaar.canonical.com/en/)
	 - Distributed VCS
 - [BitKeeper](http://www.bitkeeper.org)
	 - Distributed VCS

***Later I'll add more articles about distributed VCSs specially ([Git](https://git-scm.com)) and its core concepts.***

**Finally**, Thank you for reading this :heart:! I hope this article is helpful for you. 
If you have any questions, you're welcome to ask through comments here. 

### References

-  [Git Pro](https://git-scm.com/book/en/v2)