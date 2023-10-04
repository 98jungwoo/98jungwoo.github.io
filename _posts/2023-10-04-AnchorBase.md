---
layout: single
title:  "[RPA] 변화되는 UI에 입력하는 두가지 방법(Anchor Base, HTML속성사용)"
categories: UiPath
toc: true
---
<br><br>

# 랜덤으로 나오는 ui일 때 입력하는 두가지 방법 <br>
1. Anchor Base 사용
엑티브티를 사용해서 타겟을 지정해서 이용하는 방법 Find Element, Type Into을 사용한다.

2. HTML속성 사용
ui는 변경되더라고 F12를 눌러서 보면 html의 속성을 확인하여 name, id 등은 변화되지 않는 부분 있기 때문에 확인하여서 샐랙터에디터에서 수정하는 방법 <br><br>

## Anchor Base 사용
랜덤으로 나오는 ui에 엑셀파일에 있는 이름과 부가적인 내용을 입력하는 프로세스 <br>

### 화면

***화면1*** <br>
![화면1](https:/images/2023-10-04-AnchorBase.md/화면1.png) <br>

***화면2*** <br>
![화면2](https:/images/2023-10-04-AnchorBase.md/화면2.png) <br>

*** 엑셀 파일 *** <br>
![엑셀파일](https:/images/2023-10-04-AnchorBase.md/엑셀파일.png) <br><br>

### 프로세스 흐름

![프로세스흐름](https:/images/2023-10-04-AnchorBase.md/프로세스흐름.png)

![GetWorkbookSheet](https:/images/2023-10-04-AnchorBase.md/GetWorkbookSheet.png)

***Get Workbook Sheet***

시트이름을 인덱스로 가져와서 변수에 담아주는 역할
사용하는 이유는 시트이름이 변경 될 수 있는 경우가 있기 때문에 사용하는 것이 좋음 <br>
- _Index_ : 시트인덱스 번호를 적으면 됨 첫 번째 시트(=0), 두 번째 시트(=1) 등 <br>
- _Sheet_ : 내가 인덱스로 가져온 시트명을 strChalleng에 저장한다.<br>


***Read Range***

해당하는 시트의 내용을 dtChallenge에 저장한다.
<br>

![ForEachRowInDataTable](https:/images/2023-10-04-AnchorBase.md/ForEachRowInDataTable.png)

***For Each Row In Data Table***

엑셀의 내용을 저장한 dtChallenge 내용 요소하나하나 반복하기 위해서 For Each Row in Data Table를 사용한다.
<br>

![AnchorBase](https:/images/2023-10-04-AnchorBase.md/AnchorBase.png)

***Anchor Base***

변동되는 ui의 입력창을 uipath로 인식해서 입력하기 위해서는 Anchor Base를 사용하면 된다. 
특정 UI요소를 앵커로 사용하여 타겟으로 심은 UI요소를 검색하는 컨테이너이다. 불안정한 셀렉터가 잇는 요소와 상호작용하려는 경우에 사용한다. <br>
- _Find Element “LABEL”_ : 내가 찾아갈 요소를 선택한다. <br>
- _Type Into_ : 내가 입력할 내용을 입력한다. 엑셀에 있는 내용을 입력할것이기 때문에 CurrenRow.item를 사용한다. 

원하는 칸이 있는 만큼 엥커를 사용해준다.
<br><br>

![AnchorBase끝](https:/images/2023-10-04-AnchorBase.md/AnchorBase끝.png)


## html 속성 사용방법

### 수행해야할 내용

![과제](https:/images/2023-10-04-AnchorBase.md/과제.png)

### 입력해야할 엑셀 내용
해당 엑셀파일에서 ‘상가업소번호’, ‘도로명주소’, ‘신우편번호’를 추출해야한다. 

그리고 + ‘일치여부’ 컬럼 추가

![엑셀과제](https:/images/2023-10-04-AnchorBase.md/엑셀과제.png)

### 오류

![도로명주소화면1](https:/images/2023-10-04-AnchorBase.md/도로명주소화면1.png)
홈페이지 들어가자마자 화면에서 도로명 주소를 검색한 후 결과로 나오는 우편번호를 조사해야하는데

![도로명주소화면2](https:/images/2023-10-04-AnchorBase.md/도로명주소화면2.png)
첫 번째 검색 후 검색화면이 다르기 때문에 반복문 첫 번째 실행은 되지만 다음 값을 입력하기 위해서는 오류가 발생함 


### 해결방법

![도로명주소화면1의HTML](https:/images/2023-10-04-AnchorBase.md/도로명주소화면1의HTML.png)

![도로명주소화면2의HTML](https:/images/2023-10-04-AnchorBase.md/도로명주소화면2의HTML.png)

두 개의 name이 변동되지 않기 때문에 

![셀랙터에디터수정](https:/images/2023-10-04-AnchorBase.md/셀랙터에디터수정.png)

샐랙터 에디터에 name=’searchKeyword‘를 넣어줬음 

그 이유는 원래는
 
![셀랙터에디터수정전](https:/images/2023-10-04-AnchorBase.md/셀랙터에디터수정전.png)

샐랙터 선택을 하면 이런 색으로 간단하게 나오는데 id 값이 두 번째 화면의 검색창만 들어가는 것이기 때문에 안되는거였음 

그래서 실행하면 바로 두 번째 창으로 넘가서 바로 검색이 됨 



## ★이제 셀렉터로 영역을 잡거나 UI가 변동되는 사이트에 영역을 잡을 때 앵커 베이스와, html 속성을 사용하는 것 두가지를 사용하는 방법이 있다는 것을 알아두면 좋을 것 같음
