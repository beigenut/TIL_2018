___
The last updated version v0.0.4      
___


## GIT control

### git initial setting 

```
Open Git Bash (/ternimal) on responding file location ...  

$ git init
$ git add . || $ git add (file name)
$ git commit -m "(Insert commit message)"
$ git remote add origin (URL)
$ git push -u origin master
```



### .gitignore file cach delete on Git Bash

```
$ git rm -r --cached . 
$ git add .gitignore
```

You can write..

- *.md 
- folderName/  
- folderName/fileName.js  
- */folderName



### how to change an uploaded file name

```
$ git mv "index.html" "index2.html"
$ git commit -m "Change the file name to..."
$ git push
``` 


### git branch control

`master` > hotfixes > release > `develop` > `feature`

Gonna use only master, develop, and feature(s) branch initial setting will be ...

```
git branch develop               // create new branch on local
git push -u origin develop       // push new branch to origin

git checkout -b some-feature develop  // create new branch off from develop
git push -u origin some-feature

... add, commit and push 

git pull origin develop          // to be up-to-date
git checkout develop             // window moves to develop branch
git merge --no-ff some-feature   // merge code from feature to develop
git push origin develop          // push to origin develop 

git branch -d some-feature       // to delete local branch
git push origin --delete some-feature // to delete origin 
```

* --no--ff : to avoid losing information about the historical existence of<br>a feature branch and groups together all commits that together added the feature.




<br></br>
### CSS Naming regualation

    (I will try to...)Follow BEM naming regualation on css

    .blockName__elementName--modifierName-modifierValue

    ex) .class-bnt{}
        .class-btn__btn{}
        .class-btn__btn--is-hidden{}





<br></br>
___
___
The lasted version updated on 05/21/19 by me	              

### version log <br>
v0.0.1 - [git] Deleting cach on .gitignore <br>
v0.0.2 - [naming regualation] BEM examples <br>
v0.0.3 - [git] How to push the first commit to a new repository <br>
v0.0.4 - [git] How to change an uploaded file name, git flow <br>