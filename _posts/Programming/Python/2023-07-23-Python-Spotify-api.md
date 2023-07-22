---
title:  "Spotify API, Spotipy 사용하기"
excerpt: "스포티파이 API를 사용해보자."

categories:
  - Python
tags:
  - [Python, Spotify, Spotipy]

toc: true
toc_sticky: true

date: 2023-07-23
last_modified_at: 2023-07-23
---


# [Spotify API](https://spotipy.readthedocs.io/en/2.16.0/#spotipy.client.Spotify.__init__)

위의 링크를 클릭하면 영어로 설명된 Spotify API Document로 이동한다.

Spotify API를 사용하려면 Spotify for Developers 에서 DASHBOARD > CREATE AN APP으로 발급된 ID, Secret 코드를 활용해주면 된다.

이후 파이썬에서

```python
import spotipy
from spotipy.oauth2 import SpotifyClientCredentials

secret = "부여받은 코드"
cid = '부여받은 ID'

# Authorization : ID와 Password(Secret)을 설정한다. 
clinet_credentials = SpotifyClientCredentials(client_id=cid, client_secret=secret)

sp = spotipy.Spotipy(client_credentials_manager=client_credentials_manager)
```

이후 추가한 객체로 Spotify Document에 있는 기능들을 활용해주면 된다.
