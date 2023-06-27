# git-extract
Use fzf to extract files into clean commits from WIP branches

## usage

```
git extract <source_branch> <target_branch> [<main_branch>]
```
### example

```
$ git extract origin/wip-feature-dirty feature-clean origin/main
```

### demo



https://github.com/aerosol/git-extract/assets/173738/09ed7731-f5f3-4069-9376-b59ad3b59513



## motivation

I often work on long-living dirty feature branches, saving garbage "wip"
checkpoints, before I fully understand what am I even doing.
                                                                                      
When the feature is finished and tested, I end up with the garbage log that's
mostly meaningless, but not quite. I find it hard to separate sensible commit
messages from those that served only as a snapshot of some intermittent state.
                                                                                      
Usually the main units I can reason about are files/directories/namespaces etc.
So before submitting a proper PR, I need to, not only rebase against the main branch,
but also tidy up the log.
                                                                                      
This script aims to help with that, provided I know which _paths_ should
eventually end up in the clean, public branch annotated with descriptive commits
others could then review.
                                                                                      
The script will open a new fzf multi picker window with all the files
changed between `<source_branch>` and `<main_branch>`.
After selecting one or more files, it will switch to `<target_branch>`,
creating it, if necessary, and then restore selected file(s) into it.
                                                                                      
The commit message will be pre-populated with a comment containing all
the commit messages associated with selected file(s), as seen in `<source_branch>`.
                                                                                      
In case multiple authors were involved, the `Co-authored-by` header(s) will be
automatically added.

