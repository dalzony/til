# 4clojure

## nth 구현 \(no.21\)

* nth를 쓰지 않고 nth를 구현해보기, 우선 nnth를 구현해봤다.

```text
(defn nnth [c n]
  (if (= n 0)
    (first c)
    (nnth (rest c) (dec n))))
```

### 답

```text
(fn [c n]
  (if (= n 0)
    (first c)
    (recur (rest c) (dec n))))
```

* 익명함수로 수정, 재귀를 위해 recur를 사용
* 다 풀고 다른 사람의 솔루션을 보았는데, 비슷하다.

## count 구현 \(no.22\)

* count를 쓰지 않고 count를 구현해보기, 우선 countt를 구현해봤다.

```text
(defn countt
  ([c n]
  (if (empty? c)
    n
    (countt (rest c) (inc n))) )
  ([c]
    (countt c 0)))
```

* 문제는 fn 노테이션을 잘 구현하지 못하겠는데, `loop`과 `recur`, `꼬리재귀`를 이번 참에 잘 정리하고 가야겠다.
* argument에 `:or`노테이션이 있는데, 이것도 잘 정리해봐야겠다.

### 답 \(loop, recur 활용\)

* `loop`과 `recur` 사용
* 다중 인자는 받지 않음 \(fn 구문에서는 defn과 같은 노테이션이 지원되지도 않음\)

```text
(fn [c]
  (loop [cc c
         n 0]
    (if (empty? cc)
      n
      (recur (rest cc) (inc n)))))
```

* loop, recur, 꼬리재귀 내용은 =&gt; [Clojure-usage](https://dalzony.gitbooks.io/til/content/clojure/usage.html)
* 모범답안 풀이는 약간 충격적이었다. ~~아 이렇게해도 되는구나 ㅜㅜ~~

```text
#(reduce + (map (constantly 1) %))
```

## reverse 구현 \(no.23\)

reverse, rseq쓰지 않고 reverse 구현하기. 역시나 재귀를 쓰지 않고 간단히 할 방법을 찾고 있었는데... 그냥 into자체가 거꾸로 내뱉네;; 뭐지 into..?

```text
;; 내가 푼 재귀

(fn [c]
  (loop [nl []
         cc c]
    (if (empty? cc)
      nl
      (recur (cons (first cc) nl) (rest cc)))))
```

```text
;; into를 사용한 것
#(into () %)

예:
(#(into () %) [1 2 3 4 5])
(5 4 3 2 1)
```

* into는 최대 3개의 인자를 받는데, 그 때마다 동작이 조금씩 다르니 참고하자.
  * [http://clojuredocs.org/clojure.core/into](http://clojuredocs.org/clojure.core/into)

