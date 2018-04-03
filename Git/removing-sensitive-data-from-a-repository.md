# Git: Remove Sensitive Data

> [Github Remove Sensitive Data](https://help.github.com/articles/removing-sensitive-data-from-a-repository/)

## CMD

```
$ git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
$ cd YOUR-REPOSITORY
$ git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA' \
--prune-empty --tag-name-filter cat -- --all
$ echo "YOUR-FILE-WITH-SENSITIVE-DATA" >> .gitignore
$ git add .gitignore
$ git commit -m "Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore"
$ git push origin --force --all
$ git push origin --force --tags
$ git for-each-ref --format='delete %(refname)' refs/original | git update-ref --stdin
$ git reflog expire --expire=now --all
$ git gc --prune=now

$ git push -u origin master --force
```