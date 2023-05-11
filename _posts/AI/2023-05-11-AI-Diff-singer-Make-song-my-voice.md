---
title:  "[AI] 내 목소리로 노래하는 AI"
excerpt: "Diff-SVC를 활용해 내 목소리로 노래하는 AI를 만들어보자."

//현재 카테고리: Computer, Blog, Python, License
categories:
  - AI
tags:
  - [AI, TTS, DiffSinger, Diff-SVC]

toc: true
toc_sticky: true

date: 2023-05-11
last_modified_at: 2023-05-11
---

# Diffusion Model
디퓨전 모델이란 이미지를 생성하는 딥러닝 모델이다. AI로 그린 소설의 표지나, 실제 사람과 같아보이는 하지만 AI가 만들어낸 이미지등이 이에 해당된다. 개발자들은 **디퓨전 모델을 이미지말고 음성에 적용할 수는 없을까?**라는 생각을 하게되었고, **Diff-Singer**라는 걸 만들어내었다. 음성은 컴퓨터같은 작곡 프로그램에서 나타낼 때 이러한 파형이 나타내는 걸 볼 수 있는데, 이 때 **근데 저렇게 생긴 파형도 이미지로 치면 이미지 아닌가?**라는 발상으로 디퓨전 모델을 음성의 이미지에 적용시켜서 딥러닝을 시켜서 그 파형을 따라하게 되는 것이다.

![image](https://github.com/98tech-savvy/98tech-savvy.github.io/assets/128434645/9aceb174-ab67-4d0a-9c6a-882da9fbdd22)

예전에는 GAN을 사용해 음성AI를 만들었지만 요새에는 Diff-Singer를 만들어 새롭고 뛰어난 음성AI를 만들어내기 시작했다.

# Diff-SVC
다른 사람이 말하고 있는 음성을 내 목소리를 덮어씌워서 바꿔주는 프로그램이다.

[DIFF-SVC 가이드북](https://docs.google.com/document/d/1nA3PfQ-BooUpjCYErU-BHYvg2_NazAYJ0mvvmcjG40o/edit)
[학습용 COLAB](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa09LSTZ3dXRzNXkydWNlb0ZnbkhXaFUxNHprd3xBQ3Jtc0tuT2FPLXpTV0FUSWF2bTVFakhRTUlqNmViUGY5ekNQYk5SbDBHSWdkYVdvazBlMXk0cUsweE9WWWx3NHQ2eGxXM2FxRVNWbzhGamdvT1JSX2JxeGhSdHA5VUhKcGh0OGwwWW50V1ZUeUFrdG1yT2dYNA&q=https%3A%2F%2Fcolab.research.google.com%2Fdrive%2F1kiUvz1TrNJa_MOfOld7DHanv4gZsl7MN&v=JMCxsc-kJ24)
[결과용 COLAB](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbkJ3bTY4b2pyN1hJa1RqMW12SlBSc3RpbFlVQXxBQ3Jtc0ttZzd2Zy10cTI4X3IweTBKYVNyNU03cTVfd1owMnBSMkRtZjlMc2g3UlhPazhxZ1Y2bERqSU5XNWprdThJaUFjdXhwVTktUXh1bWlJZGlBQnJlV1Z5a1ZESThheXZzRGdpZTlrTkRKd0RvRmlsazJLdw&q=https%3A%2F%2Fcolab.research.google.com%2Fdrive%2F1zGPrh-qxscYU2mvhiv8rrjqEn0WHnOOF%3Fusp%3Dsharing&v=JMCxsc-kJ24)

내 목소리의 샘플을 준비한다음(길면 길수록 좋다) 그 음성파일을 15초 단위로 나누어준다.

{% include video id="q9JuYLRUsUM" provider="youtube" %}

위 영상은 음성파일을 나누어주는 툴에 대한 설명이다.

파일을 준비했다면, 가이드북의 절차에 따라 테스트 해본다.


