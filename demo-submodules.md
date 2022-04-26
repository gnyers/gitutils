---
title: Demo: Git submodule
keywords: [ git, devops ]
author:
- Gábor Nyers <gnyers@trebut.nl>
date: 2022-04-25 
---

# Steps

| project                              | submodule                             |
| :----------------------------------- | :------------------------------------ |
|                                      |                                       |
| 1a. git init projA                   | 1b. git init projB                    |
|                                      |                                       |
| 2a. cd projA                         | 2b. cd projB                          |
|                                      |                                       |
| 3a. gitgencommits 2                  | 3b. gitgencommits 3                   |
|                                      |                                       |
| 4. git submodule add ../projB        |                                       |
|                                      |                                       |
| 5a. ls -1 ./projB                    | 5b. ls -1                             |
|     (output same as 5b!)             |     (output same as 5a!)              |
|                                      |                                       |
| 6a. git status                       | 6b. git status                        |
|     (new files: .gitmodules,         |     (clean!)                          |
|                 projB)               |                                       |
|                                      |                                       |
| 7. git commit \                      |                                       |
|        -m 'add projB as submodule'   |                                       |
|                                      |                                       |
|                                      | 8. gitgencommits 2                    |
|                                      |                                       |
| 9a. ls -1 ./projB                    | 9b. ls -1                             |
|     (no change against 5a)           |     (2x new files)                    |
|                                      |                                       |
| 10. cd ./projB                       |                                       |
|                                      |                                       |
| 11. git pull                         |                                       |
|     (fast-forward merge! of projB)   |                                       |
|                                      |                                       |
| 12. cd ..                            |                                       |
| 13. git status                       |                                       |
|     (modified: projB)                |                                       |
|                                      |                                       |
| 14. git add && \                     |                                       |
|     git commit -m 'updated projB'    |                                       |
|                                      |                                       |
|                                      |                                       |
|                                      |                                       |

<!--
vim: filetype=markdown spelllang=en,nl spell foldmethod=marker lbr nolist ruler
vim: tw=90 wrap showbreak=… shiftwidth=2 tabstop=2 softtabstop=2 expandtab
-->
