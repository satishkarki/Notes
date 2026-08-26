# Useful git commands

```bash
git stash              # save current changes, clean working dir
git stash list          # show all stashed entries
git stash pop           # re-apply the most recent stash AND remove it from the stack
git stash apply          # re-apply the most recent stash but KEEP it on the stack
git stash drop           # delete a stash without applying it
git stash show -p         # preview what's in the most recent stash
```

By default, git stash does NOT include untracked (new) files. If you want those stashed too:
```bash
git stash -u
```

