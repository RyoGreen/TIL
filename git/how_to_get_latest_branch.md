# how to get latest branches
```
 git for-each-ref --sort=-committerdate refs/heads/ --format='%(committerdate:iso8601) %(refname:short)' | head -n 5
```
