---
layout: single
title:  "[GitHub] 깃허브에 프로젝트 올리기 & contributions기록"
categories: GitHub
toc: true
---

<br>

## 1. 깃허브에서 새로운 repository를 생성한 후 ##
<br><br>


## 2. git Bash Here를 열어주기 ##

![gitBashHere](https:/images/2023-06-13-githubUpload.md/gitBashHere.png)
<br><br>


## 3. 사용자이름, 사용자이메일 설정 ##

```
git config --global user.name "사용자 이름"

git config --global user.email "사용자 이메일“
```

![코드업로드이름이메일설정](https:/images/2023-06-13-githubUpload.md/코드업로드이름이메일설정.png)
<br><br>


## 4. 파일준비 ##

```
git init      #.git 파일 생성
```

![로컬저장소생성](https:/images/2023-06-13-githubUpload.md/로컬저장소생성.png)
<br><br>


```
git add .     #선택한 프로젝트 폴더 내의 모든 파일 관리
```

근데 내가 add+(공백)+. 이었던 것을 붙여서 사용해서 오류가 나왔음


![추가파일등록](https:/images/2023-06-13-githubUpload.md/추가파일등록.png)
<br><br>


```
git commit -m "주석"     #커밋
```

![커밋내용등록](https:/images/2023-06-13-githubUpload.md/커밋내용등록.png)
<br><br>


## 5. 업로드 ##

```
git remote add origin [새로만든 리포지토리 주소]

git push -u origin main       # 내가사용하는건 main이라서. master사용하면 바궈서 써주기
```

![업로드완료](https:/images/2023-06-13-githubUpload.md/업로드완료.png)
<br>

![업로드완료2](https:/images/2023-06-13-githubUpload.md/업로드완료2.png)
<br><br>


## 참고한 홈페이지 ##

[Tool/GitHub-깃허브에 프로젝트 올리기](https://soda-dev.tistory.com/12) 
<br>

[하얀문틈-깃허브(Github) 파일 업로드, 파일 올리기](https://shortcuts.tistory.com/8)
<br><br>


## ★contributions 기록성공★ ##
<br>

![contributions기록](https:/images/2023-06-13-githubUpload.md/contributions기록.png)