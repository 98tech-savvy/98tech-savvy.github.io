---
title:  "CPU, GPU, TPU, NPU의 차이"
excerpt: "CPU, GPU, TPU, NPU의 다른점"

categories:
  - CS
tags:
  - [CS, CPU, GPU, NPU, TPU]

toc: true
toc_sticky: true

date: 2023-09-01
last_modified_at: 2023-09-01
---

AI가 인기를 끌고 있는 지금, AI개발에 필수적인 학습능력을 결정짓는 데에는 GPU, TPU등의 프로세싱 칩이 사용된다. 이 들의 차이점은 무엇일까?

# CPU
CPU는 Central Processing Unit의 약자이다. PC에서 문서 작성, 은행 거래 처리 등 다양한 용도로 사용되고 있으나 기계 학습에 필요한 대량의 계산을 실행할 때에는 병목현상이 발생해 처리 속도가 느려진다.

# GPU
GPU는 Graphics Processing Unit의 약자이다. 게임이나 CG 처리등에서 활용되고 있는 범용 칩으로 기계 학습 전용으로 설계된 칩에 비해서는 효율이 떨어지지만 수천 개의 산술논리연산유닛(ALU)이 있어서 대량의 연산을 병렬로 처리하는 작업을 빠르게 할 수 있다.

# TPU
TPU는 Tensor Processing Unit의 약자이다. 구글이 개발한 NPU의 일종으로 클라우드 컴퓨팅 서비스를 통해 일반 사용자들에게 TPU의 처리능력을 제공하고 있고, 그러므로 사용자는 하드웨어를 사용할 필요 없이 기계 학습 관련 처리를 고효율로 진행할 수 있다.

# NPU
NPU는 Neural Processing Unit의 약자이다. GPU와 같이 대량의 작업을 병렬로 처리하는 데 특화되어있고 기계 학습 전용 설계 칩이기 때문에 GPU보다 나은 처리속도로 기계 학습을 진행 시킬 수 있다는 장점이 있다. 하지만 '전용' 이기 때문에 다른 용도로 범용적인 사용이 불가능하다는 단점이 있다.