---
layout : post
comments : true
title : "R Shiny로 포트폴리오 만드는 삽질기 (1)"
date : 2018-07-21
category : 'R'
---

#### Motivation
얼마 전부터 R Shiny로 뭔가를 만들어보고 있다. 데이터 분석가로 커리어체인지를 준비하고 있는데, 현엽에서 다루는 고객조사 데이터는 크기도 작고 성질이 많이 달라 포트폴리오가 꼭 필요해서다.

사실 전처리 과정이라던가 탐색적 분석, 거기서 얻은 인사이트 등은 보고서로 정리하는게 가장 좋다. 그래서 Rmarkdown 문서나 Python Notebook을 사용한 보고서 형식의 포폴을 만들 생각이었다. 그런데 Public으로 공개된 Bigquery dataset을 둘러보다가 웹 애플리케이션으로 만들어보고 싶은 데이터를 발견했다. US names 라는 데이터셋이다.

마침 내가 겪고 있는, 해결하고픈 문제는 이런 것이었다.

* 요즘은 회사에서 영어이름을 쓰는 경우도 늘고 있고, 글로벌 업무를 하려면 영어이름이 있는 게 편하다.
* 그런데 전에 쓰던 영어이름은 왠지 너무 올드한 것 같다.(마치 Mary나 John같은 느낌?...)
* 지금 쓰는 Jessy라는 이름은 한글로 부르기 불편하다.
* 영미권에서 내 나이대에 지었을 법한 영어 이름을 새로 짓고 싶다.

<br>
이런 니즈가 있었다 보니, 저 데이터셋을 봤을 때 구미가 당겼다. 그런데 데이터를 보다 보니 좀 더 욕심을 부리게 되었다.
<br>

* 이름에도 지역색의 느낌이 있을까? 개인적 취향은 서부 > 동부 > 중부 > 남부 순이다. 가급적 서부/동부적 이름을 짓고 싶다.
* 유대계 이름이 영/미인에게 어떤 이미지를 주는지 정확히는 모르지만, 내 이미지에 불필요한 왜곡이 끼지 않도록 피하고 싶다.


그래서 나뿐만 아니라 나와 비슷한 필요를 가진 사람도 사용할 수 있게 웹애플리케이션으로 만들어 보기로 했다.
<br>

### 무엇을 만들까?

내가 만들려는 애플리케이션은 다음과 같은 기능을 가진 것이다.

* **출생연도와 성별**을 선택하면, 해당년도에 많이 지어진 **Rank 순으로** 이름을 보여준다.
* 뜨고 있는 이름인지 옛날 느낌을 주는 이름인지, 앞뒤연도를 고려해 **추세**를 보여준다.
  * 각 이름을 클릭하면 1970년~최근까지의 추이를 보여준다.
  * 랭킹을 테이블에서 요약값을 어떻게 보여줄지 고민이다.
    (단순히 n년 전과 Rank 변화를 비교할지, 선형회귀를 써서 모델링을 해볼지)
* **지역별 선호도**에 유의미한 차이가 있는지 보여준다.
* **유대계 이름**에 표시해준다.

작업을 하다 보니 자꾸 아이디어가 떠올라서, 기능 리스트는 더 늘어날 수도 있을 듯하다. 위에 적은 건 구현하고 싶은 가장 기본적인 기능이다.
그 외에도 추가로 하고 싶은 작업은 Christine, Christina, Kristina, Kristen 등 발음이 유사하지만 철자만 조금 다른 이름들을 고려해서 결과값을 보여주는 것이다.

<br>
### 어떻게 만들 것인가?

Shiny는 웹 애플리케이션을 만들 수 있는 R 패키지다. 이걸로 대시보드를 만들 수도 있지만, 나처럼 Job을 구하는 입장에서 포트폴리오를 만들때도 좋은 듯하다. 내 서버를 따로 구축하지 않고도 Rstudio의 호스팅 서비스를 이용해 쉽게 퍼블리시할 수 있기 때문이다.
http://www.shinyapps.io/

<br>


### 삽질 항목

지금까지 진도는 정말이지 미미하다. R Shiny와의 삽질 때문이다. R 자체를 공부할 때는 Stackoverflow에서 왠만한 건 해결할 수 있었지만, Shiny는 체감상 자료가 많이 적은 편이다.
그래서 너무 기초적이고 부끄러운 삽질기이지만 기록으로 남겨보려 한다.


* 로컬 데이터를 읽어들일 수 있게 셋팅했다.
(도대체 이런데서 왜 삽질했는지 다음 글에서 다루기로 한다)
<br>

* 출생연도를 선택하면 해당 연도의 이름만 보여주도록 구현했다.
(간단한 Rows filtering이지만, Shiny의 Reactive 함수를 제대로 이해하지 못해서 많이 헤맴)



단순히 R Shiny 튜토리얼만 보고 구현할 수 있는 부분은 제외하고, 그 외에 수많은 구글링과 삽질이 필요했던 부분만 다뤄볼 생각이다.

<br>

다음글 : R Shiny 삽질기(2) : 로컬 데이터 분석하기