---
title: "Demo: Reading the content of Git objects"
keywords: [ git ]
author: Gábor Nyers <python-tuesday@trebut.nl>
date: 2023-04-19
---



# Introduction

Git uses compression to store the files in the `.git/objects/` directory. Reading the
content of these files is relatively easy. This demo showcases a small Python program to
read these object files

# Example repo

1. Show the commit history:

   ~~~bash
   % git log --oneline --graph --decorate --all
   * cc14dda (HEAD -> main) Commit nr.5: 452 to branch main
   * 9898918 Commit nr.4: 510 to branch main
   * 8585ba0 Commit nr.3: 837 to branch main
   * bf7b44b Commit nr.2: 305 to branch main
   * 6022f42 Commit nr.1: 623 to branch main
   ~~~

1. Show the content of a commit with Git

   ~~~bash
   git cat-file -p cc14dd 
   tree f1db95fb1efa6b01032ea101e3a9718f17e76aaa
   parent 9898918436e991d2546b49e2739aee55d59c7b45
   author Gábor Nyers <gabor@example.com> 1681931107 +0200
   committer Gábor Nyers <gabor@example.com> 1681931107 +0200

   Commit nr.5: 452 to branch main
   ~~~


# Show content of the same commit with a simple Python program

The following transcript of an interactive Python session shows the most simple solution:

~~~python
>>> import zlib                                  # Import the zlib module

>>> fname = '.git/objects/cc/14ddae65e4d5103746a9daceea86a0167e5928'

>>> content_z = open(fname, 'rb').read()         # Read the compressed content
                                                 # of object file

>>> content_plain = zlib.decompress(content_z)   # as type bytes

>>> print(content_plain.decode())                # show the content as str
commit 242tree f1db95fb1efa6b01032ea101e3a9718f17e76aaa
parent 9898918436e991d2546b49e2739aee55d59c7b45
author Gábor Nyers <gabor@example.com> 1681931107 +0200
committer Gábor Nyers <gabor@example.com> 1681931107 +0200

Commit nr.5: 452 to branch main
~~~




<!--
vim: filetype=markdown spelllang=en,nl spell foldmethod=marker lbr nolist ruler
vim: tw=90 wrap showbreak=… shiftwidth=3 tabstop=3 softtabstop=3 expandtab
-->
