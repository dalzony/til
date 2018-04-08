# 4clojure

## nth 구현 (no.21)

- nth를 쓰지 않고 nth를 구현해보기, 우선 nnth를 구현해봤다.

```clojure
(defn nnth [c n]
  (if (= n 0)
    (first c)
    (nnth (rest c) (dec n))))
```

### 답


```clojure
(fn [c n]
  (if (= n 0)
    (first c)
    (recur (rest c) (dec n))))
```
- 익명함수로 수정, 재귀를 위해 recur를 사용
- 다 풀고 다른 사람의 솔루션을 보았는데, 비슷하다.

## count 구현 (ㅜno.22)

- count를 쓰지 않고 count를 구현해보기, 우선 countt를 구현해봤다.

```clojure
(defn countt
  ([c n]
  (if (empty? c)
    n
    (countt (rest c) (inc n))) )
  ([c]
    (countt c 0)))
```

- 문제는 fn 노테이션을 잘 구현하지 못하겠는데, `loop`과 `recur`, `꼬리재귀`를 이번 참에 잘 정리하고 가야겠다.
- argument에 `:or`노테이션이 있는데, 이것도 잘 정리해봐야겠다.

### 답

(아직)
