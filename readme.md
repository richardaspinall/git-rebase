# git-rebase-test

## Branch: main

Commit 1 `m1`

- Added "main 1" >> main.txt

Commit 2 `m2`

- Added "main 2" >> main.txt

---

_main_

`--m1---m2`

---

## Branch: feature

Commit 1 `f1`

- Added "feature 1" >> feature.txt

Commit 2 `f2`

- Added "feature 2" >> feature.txt

Commit 3 `f3`

- Added "feature 3" >> feature.txt

---

_main_

`--m1---m2`

_feature_

`--m1---m2---f1---f2---f3`

---

## Branch: main

Commit 3 `m3`

- Added "main 3" >> main.txt

---

_main_

`--m1---m2---m3`

_feature_

`--m1---m2---f1---f2---f3`

---

## Branch: feature

If we merge main into feature we will end up with:

---

_main_

`--m1---m2---m3`

_feature_

`--m1---m2---f1---f2---f3---m3`

---

If we rebase we will end up with:

---

_main_

`--m1---m2---m3`

_feature_

`--m1---m2---m3---f1---f2---f3`

---

We can then squash f1, f2 and f3 into one commit:

`git rebase -i HEAD~3`

---

_main_

`--m1---m2---m3`

_feature_

`--m1---m2---m3---f1`

---

## Tidy up

I had also edited and commited the readme. Below I'm fixing up "Updated readme" and then squashing f3 and f2 into f1. The below commands show that "Updated readme" will be squashed into f1 but the commit message won't show unlike f3 and f2.

![Screen Shot 2021-08-05 at 8 48 31 pm](https://user-images.githubusercontent.com/15721687/128338455-351c3a5e-5443-4d35-a1fb-1aaca6364fcc.jpg)

## References 

https://levelup.gitconnected.com/how-to-squash-git-commits-9a095c1bc1fc

https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase
