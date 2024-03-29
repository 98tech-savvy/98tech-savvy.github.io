---
title:  "자바스크립트(JavaScript) - 소수 구하기"
excerpt: "자바스크립트로 소수를 구해보자"

categories:
  - Javascript
tags:
  - [자바스크립트, Javascript, 소수 구하기, 소수 구하는 방법]

toc: true
toc_sticky: true

date: 2023-10-09
last_modified_at: 2023-10-09
---

# 첫번째 방법

```js
function getResult(n){
    for(var i = 2; i <= Math.sqrt(n); i++){
        if(n % i == 0){
            return false;
        }
    }
    return true;
}

getResult(9);
```
 

위 코드는 소수를 판별하는 방법 중 하나인 **에라토스테네스의 체**라는 알고리즘을 사용하여 소수 여부를 확인하는 코드이다. 매개변수 9를 받고, 숫자 9가 소수인지 아닌지 구별하기 위해서 2부터 9의 제곱근까지 수로 나눠보고, 0으로 나눠떨어지는 수가 있다면 소수가 아니라고 판단한다.

자바스크립트에선 Math.sqrt(n) 함수를 사용하면 숫자의 제곱근을 구할 수 있다. 1은 소수가 아니기 때문에 2부터 시작해서 나누게 된다. 

만약 9가 소수가 아니라면, 9를 나누는 가장 작은 수는 2부터 9의 제곱근인 3까지의 사이의 값이기 때문에 그 이상의 수로 나누는 것은 의미가 없다. 2부터 3까지 반복문을 돌면서 9를 나누게 되고, 9는 3으로 나눴을 때 0으로 나눠떨어지기 때문에 소수가 아니다.

따라서, 위 코드는 true를 반환하면 n이 소수라고 판단하고, false를 반환하면 n이 소수가 아니라고 판단한다. 

Math.sqrt(n)을 사용하는 것은 효율성을 높이기 위해서이다. 주어진 숫자의 제곱근까지만 반복하여 나눗셈을 하므로, 효율적이다. 제곱근까지만 반복하면 되기 때문에 시간 복잡도는 O(sqrt(n))으로 상대적으로 시간이 적게 걸린다. 

# 두번째 방법

```js
function getResult(n){
    let check = 0;
    for(var i = 1; i <= n; i++){
        if(n % i === 0){
            check++;
        }
    }
    if(check === 2) return true;
    else return false;
}

getResult(9);
```

두번째 코드는 간단한 소수 판별 방법으로, 주어진 숫자 n이 소수라고 판단하면 true를 반환하고, 소수가 아니면 false를 반환한다.

위 코드에서 check 변수는 숫자 9를 나누어떨어지게 하는 수의 개수를 세는 역할을 한다. 1부터 9까지의 수로 숫자 9를 나눠보고, 나눠떨어지는 경우 check 변수를 증가시킨다. 그리고 마지막에 check 값이 2인지 확인하여 2라면 소수라고 판단한다. 위 코드에서 9를 매개변수로 받으면 check 값이 3이 나오기 때문에, 9는 소수가 아니니 false가 반환된다.

소수는 1과 자기 자신으로만 나누어떨어지는 수이므로, check 값이 2라면 숫자 n은 소수이다. 

위 코드는 숫자 n까지 모든 수에 대해 반복문을 수행하고, 나눠떨어지는지를 확인하여 소수인지 판단한다. 이 방법은 주어진 숫자의 크기에 비례하여 반복 횟수가 증가하기 때문에 상대적으로 더 많은 연산을 수행해야 한다. 따라서, 첫번째 방법에 비해 효율성이 낮다.


따라서 소수를 판별하기 위해선 **에라토스테네스의 체 알고리즘을 사용하는 것이 더 효율적이다.**