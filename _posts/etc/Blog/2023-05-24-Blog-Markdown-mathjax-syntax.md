---
title:  "[Blog] 마크다운 수식 문법 정리 - Mathjax Syntax"
excerpt: "마크다운에서 수학 수식 사용하기, Mathjax Syntax Summary"

//현재 카테고리: Comptuer, Blog, Python
categories:
  - Blog
tags:
  - [blog, markdown, mathjax, 마크다운, 마크다운 수학 수식, 수학 수식 적는법]

toc: true
toc_sticky: true

date: 2023-05-23
last_modified_at: 2023-05-23
---

# minimal-mistakes 에서 사용하기

1. ``_include/scripts.html``에서 다음과 같은 코드를 추가한다.

```html
{% if page.mathjax %}
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" defer
        src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>
{% endif %}
```

2. ``_config.yml`` 폴더에 ``mathjax:true``를 추가해준다.
\# defaults 에 넣어주면 됨.

# Mathjax Syntax
기본적으로 $$$$ 안에 넣어주면 된다.

## 사칙연산

```
$$1+2$$ // 덧셈
$$3-4$$ // 뺄셈
$$5 \times 6$$ // 곱셈
$$7 \div 8$$ // 나눗셈
```
$$1+2$$
$$3-4$$
$$5 \times 6$$
$$7 \div 8$$

## 분수 (fraction)

```
$$\frac{1}{2}$$
$$^1 / _2$$
```
$$\frac{1}{2}$$
$$^1 / _2$$

## 로그 (log)

```
$$\log_b a$$
```
$$\log_b a$$

## 루트 (root)

```
$$\sqrt{2}$$
```
$$\sqrt{2}$$

## 팩토리얼 (factorial)

```
$$n!$$
```
$$n!$$

## 첨자 (superscript)

```
$$2^2$$ // 윗 첨자
$$a_1$$ // 아랫 첨자
```
$$2^2$$
$$a_1$$

## 괄호 (parentheses)

```
$$(1+2)$$ // 소괄호
$$(\lbrace 1+2 \rbrace)$$ // 중괄호
$$[1+2]$$ // 대괄호
```
$$(1+2)$$ 
$$\lbrace 1+2 \rbrace$$ 
$$[1+2]$$ 

## 집합 (set)
```
// { - \lbrace, } - \rbrace

$$\lbracea, b\rbrace \cup \lbrace c, d\rbrace = \lbrace a,b,c,d \rbrace$$ // 합집합

$$\lbracea, b, c\rbrace \cap \lbrace a, d, e\rbrace = \lbrace a \rbrace$$ // 교집합

$$x \in [1, 2]$$ // 포함된 원소

$$ \emptyset $$ // 공집합
```

$$\lbrace a, b \rbrace \cup \lbrace c, d\rbrace = \lbrace a,b,c,d \rbrace$$

$$\lbrace a, b, c \rbrace \cap \lbrace a, d, e\rbrace = \lbrace a \rbrace$$

$$x \in [1, 2]$$

$$ \emptyset $$

## 극한 (limit)

```
$$\lim_{x \to \infty} f(x) = 0$$
```

$$\lim_{x \to \infty} f(x) = 0$$

## 시그마 (sigma)

```
$$\sum_{i=1}^{10} t_i$$
```

$$\sum_{i=1}^{10} t_i$$

## 줄임표 (elipsis)

```
$$1, 2, \dots, 100$$ // 바닥
$$1, 2, \cdots, 100$$ // 가운데
$$\vdots$$ // 세로
$$\ddots$$ // 대각선
```

$$1, 2, \dots, 100$$
$$1, 2, \cdots, 100$$ 
$$\vdots$$
$$\ddots$$ 

## 직선, 방향

```
$$\overleftrightarrow{AB}$$ //직선
$$\overrightarrow{AB}$$ //반직선
$$\overleftarrow{AB}$$ 
$$\overline{AB}$$ // 선분
```

$$\overleftrightarrow{AB}$$
$$\overrightarrow{AB}$$ 
$$\overleftarrow{AB}$$ 
$$\overline{AB}$$ 