---
title: A kio slave and daemon to stash discontinuous file selections 
tags: [programming,kio,files,manager]
layout: article
mode: normal
type: article
sharing: true
author: Arnav Dhamija
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/A kio slave and daemon to stash discontinuous file selections.png
---
## Aim
To create a kio slave and daemon to stash discontinuous file selections.
<!--more-->

## Project Description
Selecting multiple files in any file manager for copying and pasting has never been a pleasant experience, especially if the files are in a non-continuous order. Often, when selecting files using Ctrl+A or the selection tool, we find that we need to select only a subset of the required files we have selected. This leads to the unwieldy operation of removing files from our selection. Of course, the common workaround is to create a new folder and to put all the items in this folder prior to copying, but this is a very inefficient and very slow process if large files need to be copied. Moreover Ctrl+Click requires fine motor skills to not lose the entire selection of files.

This is an original project with a novel solution to this problem. His solution is to add a virtual folder in all KIO applications, where the links to files and folders can be temporarily saved for a session. The files and folders are “staged” on this virtual folder. Files can be added to this by using all the regular file management operations such as Move, Copy and Paste, or by drag and drop. Hence, complex file operations such as moving files across many devices can be made easy by staging the operation before performing it.

Checkout whole code used in this project and know more about his project [here](https://technopediabphc.wordpress.com/2016/09/29/a-kio-slave-and-daemon-to-stash-discontinuous-file-selections/).
