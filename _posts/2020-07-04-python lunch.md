---
layout: post
title: 증포중 급식 코드
---

일단 코드 먼저 보여드리고 설명하겠습니다.

```python
#학교 급식

from bs4 import BeautifulSoup
import requests
import time

time = time.strftime("%Y%m%d", time.localtime(time.time())) #오늘날짜
url = requests.get("http://www.jpo.ms.kr/lunch.view?date=%s" % time)
body = url.text
get = BeautifulSoup(body, "html.parser")

for tag in get.select("div[class=menuName] span"):
    print("%s\n\n%s\n" % (str(time), tag.text))
```

모듈

```python

from bs4 import BeautifulSoup
import requests
import time

```

이 부분부터 설명드리겠습니다.

먼저 requests라는 친구는 get 함수를 이용해서 주소의 html을 들고오는 역할입니다.
그 후에 Bs4에서 들고온 BeautifulSoup라는 친구는 request에서 들고온 정보를 파이썬이 알아볼수 있는 형식으로 바꿔줍니다.
마지막으로 time은 이름에서 보이듯이 시간에 관한 모듈이며 이 코드에서는 프로그램을 실행하는 날의 날짜정보를 가져오기위해 사용되었습니다.

변수

```python
time = time.strftime("%Y%m%d", time.localtime(time.time())) #오늘날짜
url = requests.get("http://www.jpo.ms.kr/lunch.view?date=" % time)
body = url.text
get = BeautifulSoup(body, "html.parser")
```

이 부분에서 time변수는 주석에 나와있듯이 프로그램을 실행하는 날의 날짜를 문자열 형태로 가집니다.
예를 들어 오늘이 2020년 8월 3일 이라면 "20200803"이라는 값이 저장됩니다.

url변수는 get함수의 매개변수인 "http://www.jpo.ms.kr/lunch.view?date=%s" % time 의 html을 가져옵니다.
이때 date는 날짜를 나타내기 떄문에 time값을 넣어주었습니다.

body변수에는 url변수에 들어있는 html을 str(문자열) 형태로 바꾼 값이 들어갑니다.
html을 굳이 문자열로 바꾸는 이유는 파이썬이 get함수로 얻어온 값을 써먹지 못하기 때문에 BeautifulSoup의 매개변수로 넘겨주기 위함입니다.

마지막으로 get변수는 BeautifulSoup함수를 이용해서 파이썬이 알아볼 수 있는 자료형으로 바꿔준 값을 저장합니다.

본문

```python

for tag in get.select("div[class=menuName] span"):
    print("%s\n\n%s\n" % (str(time), tag.text))

```

여기서부터는 정보를 골라내서 출력하는 부분입니다.

for문 안에 있는 get.select("div[class=manuName] span") 은 
"http://www.jpo.ms.kr/lunch.view?date=%s" % time <- 이 주소의 html에서 menuName 클래스에 있는 <span> 태그 속의 값을 리스트 형태로 가져옵니다.

그 값을 tag라는 변수에 하나하나 저장해서 시간과 함께 출력합니다.

-끝-
