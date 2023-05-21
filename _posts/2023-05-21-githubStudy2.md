---
layout: single
title:  "[GitHub] 깃허브 contribution 기록 관련 해결중 2"
categories: GitHub
toc: true
permalink: /month-archive/
author_profile: true
---


<!--

---
layout: monthly
permalink: /month-archive/
title:  "[GitHub] 깃허브 contribution 기록 관련 해결중 2"
categories: GitHub
author_profile: true  // author_profile: true'는 블로그의 사이드바에 저자 프로필을 표시하도록 설정합니다
---


---
<%-- layout: single
title:  "[GitHub] 깃허브 contribution 기록 관련 해결중 2"
categories: GitHub
toc: true  // 'toc: true'는 블로그 게시물의 헤더(제목)에서 목차(Table of Contents)를 생성하도록 허용합니다. 
---
-->


지난번에는 브랜치를 새로 생성해서 연결해준 다음 contribution이 기록이 되는지를 확인해 봤지만 역시나 문제는 해결 되지 않았다.





구글로 찾아보니까 기존에 작성했던 커밋 내용을 pick 에서 edit로 변경해주는 작업을 해주면 지나간 기록들을 contribution로 남길수 있다고 했다. 그래서 다시 시도를 해보자!

---------------------------------------------------------

# commit 정보 수정

이번에는 카톡의 AskUp에게 도움을 요청하였음.


---------------------------------------------------------

```
해당 방법은 작성한 포스트의 commit 정보를 수정하는 것입니다. 이를 위해서는 다음과 같은 절차를 따르면 됩니다. 

1. 수정해야 할 부분은 이미 작성한 포스트의 commit 정보입니다. 즉, commit 정보를 수정하여 contribution에 포함되도록 해야 합니다.

해당 브랜치에서 `git log` 명령어를 입력하여 commit history를 확인합니다.
수정하고자 하는 commit의 해시 값을 확인합니다.


2. 
```
git rebase -i <commit 해시값>
```


3. 
위 명령어를 실행하면, 해당 commit을 수정하는 창이 열립니다. 이때, 수정하고자 하는 commit의 pick을 edit로 변경합니다. 그리고 `:wq`로 저장하고 창을 닫습니다.


4.  `git commit --amend` 명령어를 입력하여 commit을 수정합니다.


5. `git rebase --continue` 명령어를 입력하여 rebase 작업을 마무리합니다.


6.  `git push --force` 명령어를 이용하여 수정된 commit을 push 합니다.


다만, `--force` 옵션을 사용하여 강제로 push하기 때문에, 수정한 내용이 다른 사람들과 충돌하거나 이전 commit을 덮어쓸 가능성이 있으니 주의하시기 바랍니다.

```

라고 알려주었기 때문에 실행하였다.

---------------------------------------------------------


일단 커밋 기록을 확인해보았다.

![GitHubStudy10](https:/images/2023-05-21-githubStudy/githubStudy10.png)


log가 1개밖에 없다. 내가 main으로 바꾸고 커밋한 내용밖에 없다. 일단 이거라도 바꿔보자

![GitHubStudy11](https:/images/2023-05-21-githubStudy/githubStudy11.png)

---------------------------------------------------------


바꿀 필요가 없다고 한다...

![GitHubStudy12](https:/images/2023-05-21-githubStudy/githubStudy12.png)



그럼 이건 실패. 





일단, master 브랜치 목록을 확인해서 로컬 컴퓨터의 브랜치를 다시 변경해서 거기에 있는 커밋한 내용들을 edit로 바꿔보기로 한다.

---------------------------------------------------------


# 브랜치 목록 확인

근데

![GitHubStudy13](https:/images/2023-05-21-githubStudy/githubStudy13.png)


현재 사용하는 브랜치는 main이고,   현재 작업중인 브랜치를 master로 변경하겟다고 했는데
master브랜치가 없다고 뜬다... 이게 무슨,,,,


---------------------------------------------------------


그래서 혹시 삭제한건가 싶어서 로컬과 리모트에 있는 모든 브랜치의 목록을 확인해보았다.

![GitHubStudy14](https:/images/2023-05-21-githubStudy/githubStudy14.png)

그런데 master는 없고 main만 남아있다. 


---------------------------------------------------------


혹시 삭제 했는지 확인해보려고  로컬 저장소에서 발생한 모든 작업들의 로그를 확인하였는데. master에 대한 내용이 없다.

![GitHubStudy15](https:/images/2023-05-21-githubStudy/githubStudy15.png)



내가 사용하고 있는 브랜치는 main, 전에 사용하던 브랜치는 master.



아우 어려워... 다음에 다시 시도해보자....















