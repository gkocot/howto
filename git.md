Copy git repo1/dir1 to repo2/src/dir1 (rename) and preserve history.
```
repo1
|-dir1
|-dir2

repo2
|-src
  |-dir1
```
https://github.com/newren/git-filter-repo  
https://htmlpreview.github.io/?https://github.com/newren/git-filter-repo/blob/docs/html/git-filter-repo.html  

Clone 'repo1' and filter out everything but 'dir1', rename 'dir1' to 'src/dir1'
```
cd ~
git clone repo1
cd repo1
git filter-repo --path Onvif/ --path-rename dir1:src/dir1
```

Temporaryli add remote to 'repo1' and merge it.
```
cd ~
git clone repo2
cd repo2
git remote add tmp ~/repo1/
git fetch tmp main
git merge remotes/tmp/main --allow-unrelated-histories
git remote remove tmp
git push
```
