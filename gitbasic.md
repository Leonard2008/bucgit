git remote -v
git remote set-url orgin https://github.com/Leonard2008/git-usage.git

mkdir mydir
git add *
git commit -m "message"
git remote add gitusage git@github.com:Leonard2008/git-usage.git>
git push gitusage master


git checkout -b feature_x //create a branch and switch to it
git checkout master       //switch back to master
git branch -d feature_x   //delete the branch
git push gitusage <branch>

git pull //update your local repo to the latest version
git merge <branch> //merge <branch> to master
git diff <source_branch> <target_branch> //check difference
 
git log //to get ID
git tag 1.0.0 <first_10_chars_of_ID>

git checkout -- <filename> //use the latest file of HEAD to replace your local file
git fetch origin // discard all local changes and fetch files from server
git reset --hard origin/master //reset local master branch to server's master branch


------

svnadmin create  ------------------------------> git init
svn co           ------------------------------> git clone
svn update       ------------------------------> git pull
svn add          ------------------------------> git add
svn commit       ------------------------------>  git add, git commit
svn status       ------------------------------>  git status
svn switch <branch>  ------------------------>  git checkout <branch>
svn merge <branch>   ------------------------>  git merge <branch>
svn revert <file>  ------------------------------> git checkout <file>
