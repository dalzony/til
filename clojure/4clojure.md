# 4clojure

## nth 구현 (no.21)

- nth를 쓰지 않고 nth를 구현해보기, 우선 nnth를 구현해봤다.

```clj
(defn nnth [c n]
  (if (= n 0)
    (first c)
    (nnth (rest c) (dec n))))
```

- 익명함수로 수정, 재귀를 위해 recur를 사용

```clojure
(fn [c n]
  (if (= n 0)
    (first c)
    (recur (rest c) (dec n))))
```

- 다 풀고 다른 사람의 솔루션을 보았는데, 비슷하다.
