---
title:  "[Python] 파이썬의 내장 함수 코드 보는 법"
excerpt: "파이썬의 내장 함수들의 코드는 어디서 볼 수 있을까?"

categories:
  - Python
tags:
  - [Python, 파이썬, 내장함수, 내장 함수, 내장 함수 보는법]

toc: true
toc_sticky: true

date: 2024-01-24
last_modified_at: 2024-01-24
---

가끔 코딩을 하다보면 '왜 이 함수는 이렇게 작동하지?' 라던가 '이 함수는 어떻게 이런 기능을 하는거지?'란 생각이 들곤 한다. 그런데 파이썬 내장함수를 직접적으로 보는 방법을 잘 모르겠어서 구글링을 통해 검색해보았다.

# 함수 내부 코드 가져오기
파이썬 내장 함수 뿐이 아니라, 특정 라이브러리의 함수 코드가 궁금해지는 개발자 분들도 있을 것이기에, 이것 또한 준비해보았다.
``inspect``라는 모듈을 사용해서 특정 함수의 내부 코드를 알아낼 수 있는데, ``inspect`` 모듈의 ``getsource``라는 함수를 이용해 알아낼 수 있다.

```py
import inspect
import numpy as np

print(inspect.getsource(np.argmax))

--------------------------------
    """
    Returns the indices of the maximum values along an axis.

    Parameters
    ----------
    a : array_like
        Input array.
    axis : int, optional
        By default, the index is into the flattened array, otherwise
        along the specified axis.
    out : array, optional
        If provided, the result will be inserted into this array. It should
        be of the appropriate shape and dtype.
    keepdims : bool, optional
        If this is set to True, the axes which are reduced are left
        in the result as dimensions with size one. With this option,
        the result will broadcast correctly against the array.

        .. versionadded:: 1.22.0

    Returns
    -------
    index_array : ndarray of ints
        Array of indices into the array. It has the same shape as `a.shape`
        with the dimension along `axis` removed. If `keepdims` is set to True,
        then the size of `axis` will be 1 with the resulting array having same
        shape as `a.shape`.

    See Also
    --------
    ndarray.argmax, argmin
    amax : The maximum value along a given axis.
    unravel_index : Convert a flat index into an index tuple.
    take_along_axis : Apply ``np.expand_dims(index_array, axis)``
                      from argmax to an array as if by calling max.

    Notes
    -----
    In case of multiple occurrences of the maximum values, the indices
    corresponding to the first occurrence are returned.

    Examples
    --------
    >>> a = np.arange(6).reshape(2,3) + 10
    >>> a
    array([[10, 11, 12],
           [13, 14, 15]])
    >>> np.argmax(a)
    5
    >>> np.argmax(a, axis=0)
    array([1, 1, 1])
    >>> np.argmax(a, axis=1)
    array([2, 2])

    Indexes of the maximal elements of a N-dimensional array:

    >>> ind = np.unravel_index(np.argmax(a, axis=None), a.shape)
    >>> ind
    (1, 2)
    >>> a[ind]
    15

    >>> b = np.arange(6)
    >>> b[1] = 5
    >>> b
    array([0, 5, 2, 3, 4, 5])
    >>> np.argmax(b)  # Only the first occurrence is returned.
    1

    >>> x = np.array([[4,2,3], [1,0,3]])
    >>> index_array = np.argmax(x, axis=-1)
    >>> # Same as np.amax(x, axis=-1, keepdims=True)
    >>> np.take_along_axis(x, np.expand_dims(index_array, axis=-1), axis=-1)
    array([[4],
           [3]])
    >>> # Same as np.amax(x, axis=-1)
    >>> np.take_along_axis(x, np.expand_dims(index_array, axis=-1), axis=-1).squeeze(axis=-1)
    array([4, 3])

    Setting `keepdims` to `True`,

    >>> x = np.arange(24).reshape((2, 3, 4))
    >>> res = np.argmax(x, axis=1, keepdims=True)
    >>> res.shape
    (2, 1, 4)
    """
    kwds = {'keepdims': keepdims} if keepdims is not np._NoValue else {}
    return _wrapfunc(a, 'argmax', a
```

# 파이썬 내장 함수 코드 확인
처음의 ``inspect`` 모듈만을 가지고는 파이썬의 내장 함수를 확인할 수 없는 경우가 있다. 이유는 파이썬은 C언어로 구현되어있고, 내장함수는 파이썬 내 함수 정의 형식으로 작성되지 않는 경우도 있기 때문이다. 이럴때는 [파이썬 내장 함수 Github](https://github.com/python/cpython) 사이트에서 확인할 수 있다. 이 깃허브 페이지에는 python을 구현한 소스 코드 목록이 업로드되어있고, 내장 함수를 비롯한 여러 object의 코드들 또한 작성되어 있다.