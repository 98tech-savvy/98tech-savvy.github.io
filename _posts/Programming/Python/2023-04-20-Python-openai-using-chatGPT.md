---
title:  "[Python] ChatGPT를 Python(파이썬)으로 사용해보기"
excerpt: "ChatGPT를 openai 모듈로 불러와서 Python으로 코딩해서 대화해보자"

//현재 카테고리: Computer, Blog, Python, License
categories:
  - Python
tags:
  - [Python, ChatGPT, OpenAI, 인공지능]

toc: true
toc_sticky: true

date: 2023-04-20
last_modified_at: 2023-04-20
---

# ChatGPT
우리들이 흔히 알고있는 인공지능 채팅의 친구들을 생각하면, 이 녀석은 특이점이라고 할 수 있을정도로 엄청난 발전과 테크닉으로 이루어져있는 인공지능 챗봇이다. 대형 언어 모델 **GPT-3**의 개선판인 **GPT-3.5**로 이루어져있고(이후 **GPT-4.0**) 지도학습&강화학습을 통해 파인튜닝된 인공지능 모델이다.

# API_KEY 발급받기
[OpenAI, API키 발급받기](https://platform.openai.com/account/api-keys)

위 링크를 클릭하면 OpenAI 공식 홈페이지가 나오는데, 여기서 OpenAI를 사용하기 위한 API_KEY를 발급받을 수 있다. 

1. 계정을 만든다

2. 로그인을 하고 우측상단 계정 프로필 사진 옆의 **Personal** 클릭.

3. **View API KEY**를 누른 후 **+ Create new secret key**를 누르면 발급완료.
이 때 창을 닫아버리면 다시 키를 볼 수 없기때문에 복사를 해서 파일로 저장해두는 것을 권함.

# Python 모듈 설치하기
API KEY도 발급받았겠다. 파이썬에서 모듈을 설치하고 대화해보자.

VSCode같은 텍스트 에디터의 터미널에서 다음 명령어로 OpenAI 모듈을 설치할 수 있다.

``pip install openai``

설치가 완료되면 파일.py에서 다음의 코드를 입력한다.

```python
import openai
import os

openai.api_key = os.environ["OPENAI_API_KEY"]
model_engine = "text-davinci-002"

def generate_text(prompt):
    response = openai.Completion.create(
        engine=model_engine,
        prompt=prompt,
        max_tokens=2048,
        n=1,
        stop=None,
        temperature=0.5,
    )
    message = response.choices[0].text.strip()
    return message

while True:
    user_input = input("You: ")
    if user_input.lower() in ["bye", "goodbye"]:
        print("ChatGPT: Goodbye!")
        break
    prompt = f"You: {user_input}\nChatGPT:"
    message = generate_text(prompt)
    print(message)
```

``openai.api_key = os.environ["OPENAI_API_KEY"]`` 이 부분의 ``OPENAI_API_KEY``에 자신이 발급받은 API_KEY를 넣어주자. 만약 API_KEY_ERROR가 발생한다면 자신이 사용하고 있는 운영체제의 환경변수에 OPENAI_API_KEY를 만들어주고 그 값을 넣어준 후에 OPENAI_API_KEY로 사용해보자.

# 사용

*실제로 터미널에서 대화해본 내용*
![image](https://user-images.githubusercontent.com/128434645/232458918-b211e37e-eeed-42a6-83f2-f46de55dfabc.png)

OpenAI사이트에서 사용할 수 있는 ChatGPT와는 성능이 많이 떨어지는 것 같지만(번역이 안되서 나오는 부분, 짧은 대답 등) 그럼에도 저 짧은 코드로 인공지능과 대화할 수 있다는건 꽤나 매력적인 모듈이지 않을까 싶다.