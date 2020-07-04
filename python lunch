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
url = requests.get("http://www.jpo.ms.kr/lunch.view?date=" % time)
body = url.text
get = BeautifulSoup(body, "html.parser")

for tag in get.select("div[class=menuName] span"):
    print("%s\n\n%s\n" % (str(time), tag.text))
```
