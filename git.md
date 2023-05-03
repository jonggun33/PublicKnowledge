## Merging two repositories
```bash
git remote add [new branch/repository name] [url]
git fetch [new branch name]
git merge remotes/[new branch name]/master
```
## Conflict Resolution
Conflicts can occur during a pull or merge: but the procedures to resolve them are essentially the same.

### Conflict during a pull
If same files locally revised are also revised on the remote, it will tell you that a conflict has arisen and the file(s) will be decorated with conspicuous markings incorporating changes from both commits.
You will have to manually edit the file to satisfy both intentions of editings, and then commit it.
```bash
git pull
//edit the conflicted file
git commit -a -m "conflict resolved"
git push
```
### Conflict during a merge
The Pull Request from the Github page will warn you of conflicts if any.
If the conflicts are trivial, Github page will let you resolve them on the web, otherwise, you will:

. pull the master on the command prompt
. Pull the feature branch on the command prompt
. In the master branch, perform merge
. Manually de-conflict
. Commit
. Push -- this will dismantle the conflcit on the Pull Request Page and also close the Pull request.
```bash
git checkout feature
git pull
git checkout master
git pull
git merge
//edit the conflicted files
git commit -a -m "conflict resolved"
git push
```