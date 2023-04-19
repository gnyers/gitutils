---
title: "Demo: Git tags"
keywords: [ git ]
author: Gábor Nyers <gabor@example.com>
date: 2023-04-19
---


# Introduction


# Prep Git repo:


1. Initialize repo and change to new directory:

   ~~~bash
   git init demo-annotations
   cd demo-annotation
   ~~~

1. Generate 5 commits:

   ~~~bash
   gitgencommits 5
   ~~~

1. Show commit history

   ~~~bash
   % git log --oneline --graph --decorate --all
   * cc14dda (HEAD -> main) Commit nr.5: 452 to branch main
   * 9898918 Commit nr.4: 510 to branch main
   * 8585ba0 Commit nr.3: 837 to branch main
   * bf7b44b Commit nr.2: 305 to branch main
   * 6022f42 Commit nr.1: 623 to branch main
   ~~~

1. Create annotated tag:

   ~~~bash
   git tag -a v0.1   bf7b44b          # will start configured editor to 
                                      # compose the annotation message
   ~~~

   or alternatively use the `-m` switch to provide a sigle-line message:

   ~~~bash
   git tag -a -m 'This is a annotate message of a single line' v0.1   bf7b44b
   ~~~

1. Create a "lightweight" tag:

   ~~~bash
   git tag    v0.12  9898918
   ~~~

1. Show commit history;

   ~~~bash
   * cc14dda (HEAD -> main) Commit nr.5: 452 to branch main
   * 9898918 (tag: v0.12) Commit nr.4: 510 to branch main
   * 8585ba0 Commit nr.3: 837 to branch main
   * bf7b44b (tag: v0.1) Commit nr.2: 305 to branch main
   * 6022f42 Commit nr.1: 623 to branch main
   ~~~

   **NOTE**: the tags:

   - `v0.1` (annotated tag) and 
   - `v0.12` (lightweight)

# Find out more about the tags

1. Get an overview of tags: 

   ~~~bash
   git tag
   v0.1
   v0.12
   ~~~

1. Get details of the annotated tag `v0.1`:

   ~~~bash
   git cat-file -p v0.1

   object bf7b44b7fb8b7c1d535391a2b7558a485ce0c0ec
   type commit
   tag v0.1
   tagger Gábor Nyers <gabor@example.com> 1681931304 +0200
   
   This is the "commit message" for the annotated tag
   
   This message is the content of an annotated tag. It may long.
   ~~~

   **NOTE**:

   1. this is the content of the tag annotation message
   1. **`tagger`** field is mentioned with the name/email of the person who
      created the annotated tag
   1. the timestamp `1681931304 +0200`; using the comman `date -d @1681931304`
      returns the date `Wed Apr 19 21:08:24 CEST 2023`

      
1. Get details of a *lightweight* (i.e.: non-annotated) tag `v0.12`:

   ~~~bash
   git cat-file -p v0.12
   % git cat-file -p v0.12
   tree d5a263586bbec80fb3df7d0774ecf64dcbb03035
   parent 8585ba0d5b0c1d8c0637ed5f435ac18e6c569539
   author Gábor Nyers <gabor@example.com> 1681931107 +0200
   committer Gábor Nyers <gabor@example.com> 1681931107 +0200
  
   Commit nr.4: 510 to branch main
   ~~~

   **NOTE**:

   1. this is the content of the commit object

## Conclusions

1. Annotated tags have an commit-like message, that may contain an (arbitrary)
   long text

1. Lightweight tags **may NOT** contain a message, they point to a specific
   commit object.



# Low-level details of tags


1. Tags are stored on the `.git/refs/tags/` directory:

   ~~~bash
   ls -1 .git/refs/tags/
   v0.1
   v0.12
   ~~~

1. View the raw content of these files:

   1. Annotated tag `v0.1`:

      ~~~bash
      cat .git/refs/tags/v0.1
      a99f71af2832d74121074742cdcd62f62e3873a1
      ~~~
   
   1. Lightweight tag `v.12`:

      ~~~bash
      cat .git/refs/tags/v0.12
      9898918436e991d2546b49e2739aee55d59c7b45
      ~~~

1. Consider the commit history:

   ~~~bash
   * cc14dda (HEAD -> main) Commit nr.5: 452 to branch main
   * 9898918 (tag: v0.12) Commit nr.4: 510 to branch main
   * 8585ba0 Commit nr.3: 837 to branch main
   * bf7b44b (tag: v0.1) Commit nr.2: 305 to branch main
   * 6022f42 Commit nr.1: 623 to branch main
   ~~~

   **NOTE**:

   1. the "content" of the **lightweight tag** points to Git object ID
      `989891...`, which is a commit object (see above commit history)
   1. the content of the **annotated tag** points to a Git object (ID
      `a99f71...`), which is not a commit, i.e.: there is no matching ID in the
      commit history

1. Let's find out more about the object representing the annotated tag:

   ~~~bash
   git cat-file -p a99f71af2832d74121074742cdcd62f62e3873a1
   object bf7b44b7fb8b7c1d535391a2b7558a485ce0c0ec
   type commit
   tag v0.1
   tagger Gábor Nyers <gabor@example.com> 1681931304 +0200

   This is the "commit message" for the annotated tag

   This message is the content of an annotated tag. It may long.
   ~~~

   **NOTE**:

   1. this is the exact content that we've seen earlier when executing the
      command: `git cat-file -p v0.1`


## Conclusions

1. Git stores tag information in the form of files in the directory
   `.git/refs/tags`
1. Each file in this directory points to a single Git object
1. Lightweight tags point to a commit object
1. Annotated tags point to an "annotate" object, which is somewhat similar to
   commit objects: they contain several pieces of information about the tag:
   1. which commit objects it refers to:
      `bf7b44b7fb8b7c1d535391a2b7558a485ce0c0ec`
   1. name of the tag: `v0.1`
   1. who created it: Gábor Nyers <gabor@example.com>
   1. when: `1681931304` (Unix style Epoc timestamp) and 
   1. the message






<!--
vim: filetype=markdown spelllang=en,nl spell foldmethod=marker lbr nolist ruler
vim: tw=90 wrap showbreak=… shiftwidth=3 tabstop=3 softtabstop=3 expandtab
-->
