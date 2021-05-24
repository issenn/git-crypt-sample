# test-crypt

## Usage

```sh
$ git-crypt init
Generating key...

$ cat .git/config
...
[filter "git-crypt"]
    smudge = \"git-crypt\" smudge
    clean = \"git-crypt\" clean
    required = true
[diff "git-crypt"]
    textconv = \"git-crypt\" diff

$ git-crypt add-gpg-user --trusted BCE6E1D2A509156191BA016FDF0B5C535207EF1E!
[master 45dbfbb] Add 1 git-crypt collaborator
 2 files changed, 4 insertions(+)
 create mode 100644 .git-crypt/.gitattributes
 create mode 100644 .git-crypt/keys/default/0/23D08DE0580658B88D87F84E90654051BA902E1B.gpg

$ vim .gitattributes
secretfile filter=git-crypt diff=git-crypt
*.key filter=git-crypt diff=git-crypt
secretdir/** filter=git-crypt diff=git-crypt
.gitattributes !filter !diff

$ echo "test" > secretdir/secretfile
$ git-crypt status
$ git rm -r --cached secretdir
$ git add .gitattributes secretdir/secretfile
$ git commit -m "Add: Add git-crypt init file"
$ git push
```
