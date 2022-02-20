--git installation and config

mkdir cd/opt/git
git init
ls -ltra >> we can see the .git file 
git config --list
git config --gloabl user.name<github account user name>
git config --global user.email<>
git remote set-url origin https://<githubtoken>@github.com/<username>/<repositoryname>.git
