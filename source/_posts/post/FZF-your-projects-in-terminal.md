---
title: FZF all your projects in terminal
date: 2019-02-24 12:04:43
categories:
tags: terminal
---

How you navigate to your projects in terminal? `cd`? `ranger`? `nnn`? t a Well, these are not
desinged for navigating projects and they really do their jobs but not so efficient.

Let me introduce the `fzf_projects`.

First, you need to install fzf. Simply go through the tutorial here.

Second, put the following code in your shell configuration file.

> Note: `project_roots` is a list of directories that projects inside within depth 1 will be added
> as projects candidates. `developer_root` is a directory that project inside within depth 2 will be
> added.

<!--more-->

```sh
# Switch projects
function fzf_projects(){
    projects=()

    # Scan roots with depth 1
    project_roots=("$HOME" "$HOME/Dropbox")
    for root in $project_roots; do
        for dir in $(find $root -maxdepth 1 -type d); do
            if [ -d $dir/.git ]; then
                projects+=($dir)
            fi
        done
    done

    # Scan Developer directory with depth 2
    developer_root=$HOME/Developer
    for dir in $(find $developer_root -maxdepth 2 -type d); do
        if [ -d $dir/.git ]; then
            projects+=($dir)
        fi
    done

    fzf_projects=""
    for project in $projects; do
        fzf_projects=$fzf_projects\\n$project;
    done
    # Trim first \n
    fzf_projects=${fzf_projects:2:${#fzf_projects}-1}

    selected_project=$(echo $fzf_projects | fzf)
    cd $selected_project
}
alias pp=fzf_projects

```

Third, source your shell configuration again or open a new terminal window. Trigger `fzf_projects`
by input `pp`.
