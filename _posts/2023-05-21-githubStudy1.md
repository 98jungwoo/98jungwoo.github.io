---
layout: monthly
title:  "[GitHub] 깃허브 contribution 기록 관련 해결중 1"
categories: GitHub
permalink: /month-archive/
toc: true
author_profile: true
---

깃허브를 생성하고, 

블로그 글을 작성한지가 벌써 2달이 넘어간다 3월달에 생성해서 그동안 열심히 작성하였는데, 늘 마음이 불편했던건 깃허브 홈페이지에 contribution이 기록되지 않는 문제였다. 

3월 초반에는 문제를 해결하려고 이것저것 많이 시도해보았지만 안되었다. 

그래도 일단 내가 배운걸 기록하는게 더 중요하다고 생각되어서 우선 순위를 뒤로 보냈지만 이제는 문제를 해결 해야하지 않을까 해서 다시 시도해보기로 한다. 


보통 기록이 되지 않으면 사용자 이메일과, 사용자 이름을 확인하라는데 나는 깃허브 이름 이메일과 컴퓨터에 기록되는 이름이 동일했다. 







그래서 생각한 방법 = 새로운 브랜치를 생성해서 연결하면 기록이 될까?




# 새로운 브랜치 생성 

![GitHubStudy1](https:/images/2023-05-21-githubStudy/githubStudy1.png)


git remote add origin 내 깃허브 주소

치명적 : "C:github_projects/98jungwoo-github-blog/git" 저장소에서 의심스러운 소유권 감지

"c:/hithub_projects/98jungwoo-github-blog/git" 소유자: "s-1-5-32-544" 그러나 현재 사용자: "s-1-5-21-49355773-4198796519-1997974794- 1001"

이 디렉토리에 대한 예외를 추가하려면 다음을 호출하십시오.

 git config --global --add safe.directory c:/github_projects/98jungwoo-github-blog/git

---------------------------------------------------------

![GitHubStudy2](https:/images/2023-05-21-githubStudy/githubStudy2.png)

git : "추가"는 git 명령이 아닙니다. 'git --help' 참조

---------------------------------------------------------

![GitHubStudy3](https:/images/2023-05-21-githubStudy/githubStudy3.png)


아무것도 지정되지 않았고 추가된 것도 없습니다.

힌트: "git add . "라고 말하고 싶습니까?

힌트: 다음을 실행하여 이 메시지를 끄십시오.

힌트: "git config advice.addEmptyPathspec falsd“



이건 내가 명령어를 잘못 입력하였음.


---------------------------------------------------------

여기서 git config advice. addEmptypathspec false를 작성하고 나서 
git add .을 작성하였더니 내용이 나열되어 나왔고 

----------------------------------------------------------

![GitHubStudy4](https:/images/2023-05-21-githubStudy/githubStudy4.png)

origin이 없다고 하니까 다시 생성해줘야한다더라 

그래서 

---------------------------------------------------------

![GitHubStudy5](https:/images/2023-05-21-githubStudy/githubStudy5.png)

git remote –v 명령어를 실행하여, 현재 로컬 리포지토리와 연결된 리모트 리포지토리가 없다고 해서 git add .을 해줬음 

---------------------------------------------------------

![GitHubStudy6](https:/images/2023-05-21-githubStudy/githubStudy6.png)

그러고 

1. git commit –m “커밋 내용을 넣어주고” 


on branch main nothing to commit, working tree clean = 분기 메인에서 커밋할 항목 없음, 작업 트리 청소
이런 말이 나왔는데 그냥 무시하고 다름 명령어를 쳐줬음


2. git remote add origin https://github.com/98jungwoo/98jungwoo.github.io.git을 해줫더니 아무 말도 안나오길래


3. git push –u origin main 명령어를 넣어줬더니, 
깃허브에서 로그인하라고 떠서 로그인을 했다. 
그러고 무슨 화면이 나오더니 연결하라고 떠서 하겠다고 했더니

---------------------------------------------------------

countion objects 00% 가 점점 올라가면서 동작했다.

![GitHubStudy7](https:/images/2023-05-21-githubStudy/githubStudy7.png)

이렇게 새로운 브랜치가 생성되었다.



---------------------------------------------------------


# 기존 브랜치에서 새로운 브렌치로 변경


일단 새로운 브랜치를 생성하였기 때문에 내가 사용하고자 하는 main브랜치를 디폴트값으로 설정해주고자 한다.

![GitHubStudy8](https:/images/2023-05-21-githubStudy/githubStudy8.png)

이제 기존(maset) 브랜치에서 main브렌치로 변경하는 작업을 해준다. (기존 블로그 글을 새로운 main으로 이동시키는 작업이다.)



---------------------------------------------------------

기존 main에서 작성한 내용들을 master와 공유하기 위해서 내용을 병합하기로 한다. 

![GitHubStudy9](https:/images/2023-05-21-githubStudy/githubStudy9.png)

이미 병합 되었다고 한다. 그럼 이제내용이 공유는 된다는 건데... 





---------------------------------------------------------


문제는 브랜치를 변경하니 블로그에 기본적으로 들어가는 내용들이 내 컴퓨터 c드라이브에서 안보인다.

그래서 main으로 변경해서 값을 복사한 다음 master로 변경해서 복사 붙여넣기를 해주었다. 


그런 다음 새로운 글을 작성해서 기록이 되는지 확인해봐야겠다........







