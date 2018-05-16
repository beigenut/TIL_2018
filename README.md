___
The last updated version v0.0.3      
___


## GIT control

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


<br></br>
### git initial setting 

```
Open Git Bash (/ternimal) on responding file location ...  

$ git init
$ git add . || $ git add (file name)
$ git commit -m "(Insert commit message)"
$ git remote add origin (URL)
$ git push -u origin master
```


<br></br>
## CSS Naming regualation

    (I will try to...)Follow BEM naming regualation on css

    .blockName__elementName--modifierName-modifierValue

    ex) .class-bnt{}
        .class-btn__btn{}
        .class-btn__btn--is-hidden{}





<br></br>
___
___
The lasted version updated on 05/16/18 by me	              

### version log <br>
v0.0.1 - [git] Deleting cach on .gitignore <br>
v0.0.2 - [naming regualation] BEM examples <br>
v0.0.3 - [git] How to push the first commit to a new repository <br>