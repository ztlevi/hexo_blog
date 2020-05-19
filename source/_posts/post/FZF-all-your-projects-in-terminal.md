---
title: FZF all your projects in terminal
date: 2019-02-25 15:49:08
categories:
  - coding
tags:
  - terminal
cover: https://cdn-media-1.freecodecamp.org/images/1*TnsFDs-DEye722CrQXjv8w.png
preview: 300
---

How you navigate to your projects in terminal? `cd`? `ranger`? `nnn`? t a Well, these are not desinged for navigating
projects and they really do their jobs but not so efficient.

Let me introduce the `fzf_projects`.

First, you need to install fzf. Simply go through the tutorial here.

Second, put the following code in your shell configuration file.

> Note: `project_roots` is a list of directories that projects inside within depth 1 will be added as projects
> candidates. `developer_root` is a directory that project inside within depth 2 will be added.

<!--more-->

```sh
# Switch projects
function fzf_projects() {
  # Each root is consist of PATH:scan_depth
  project_scans=("${HOME}:1" "${HOME}/Dropbox:1" "${HOME}/go/src:1" "${HOME}/Developer:2")

  projects=()
  local project scan_depth
  for project_scan in ${project_scans[@]}; do
    IFS=: read -r project scan_depth <<<"${project_scan}"
    if [[ -d ${project} ]]; then
      for dir in $(find ${project} -maxdepth ${scan_depth} -type d); do
        if [[ -d ${dir}/.git ]]; then
          projects+=(${dir})
        fi
      done
    fi
  done

  local IFS=$'\n'
  selected_project=$(echo "${projects[*]}" | fzf)

  cd ${selected_project}
}
alias pp=fzf_projects
```

Third, source your shell configuration again or open a new terminal window. Trigger `fzf_projects` by input `pp`.
