- - - 
<!-- *********8************날짜****************************** -->
# 032118 Wed  

## <strong> 1. Today I learned </strong>




<!-- *********************첫번째 제목********************** -->
### <span style="color:#595EFF"> [GitHub] 1-1. GitHub 다른 사람의 Repo 가져오기(Clone) </span>    

GitHub 에서 다른 사람이 코딩한 레포를 불러와서 재가공 하고 싶은 경우, 

터미널을 켜고 clone을 원하는 파일 경로에서 ex) ../desktop/clone 
```
$ git clone "url"
```
을 입력하면 해당 파일 경로로 해당 repo를 다운로드 할 수 있다. 




<br></br>
<!-- ***********************두번째 제목******************** -->
### <span style="color:#595EFF"> 1-2. 상위 folder 전체의 파일 및 하위 폴더를 GitHub 에 push 하는 방법 </span>

1. 이렇게 순서를 매겨서
	* 안쪽으로 더 넣어서
	* 순서에 맞춰
2. 쓸 수도 있습니다
3. 다만 굳이 시간이 없으면 키워드





<br></br>
<!-- ***********************세번째 제목******************** -->
### <span style="color:#595EFF"> 1-3. "Putain" .gitignore 적용 및 업데이트 반영; 캐시 삭제 </span>

repo 등록된 최상위 폴더에서 GitHub에 업로드 하고 싶지 않은 파일이나 폴더가 있다면 이를 배제하고 업로드시킬 수 있다. 

> folderName/ 해당 폴더의 하위내용 모두를 제외하고 push. 

맨 처음 push 이후에 .gitignore 파일을 업데이트/반영 하려고 하는 경우, 캐시를 꼭 삭제해야 한다. 

``` 
$ git rm -r --cached .
$ git add . or "fileName"
```




## <strong> 2. Today I found out </strong>

배운 내용 외에 뭔가 깨달음이 왔거나 느낀 바가 있다면 일기처럼 간단하게 적어주시면 됩니다. 자신의 감정을 기록하고 새롭게 얻은 교훈을 되새김질하는 것만으로도 더 성장할 수 있으니까요!





## <strong> 3. 오늘 읽은 자료 (혹은 참고할 링크, 생략해도 됨) </strong>

what it is what it is
- <a href="www.wherewhere.com" style="text-decoration:none; color:#595EFF"> https://www.wherewhere.com </a>

what it is what it is
- <a href="www.wherewhere.com" style="text-decoration:none; color:#595EFF"> https://www.wherewhere.com </a>
- - - -
