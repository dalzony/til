# usage

## loop & recur \[미완\]

* `loop`은 `recur`의 대상점\(기준점\)이 됨, recur를 만나면 loop으로 가거나 현재 함수를 재귀로 부르거나.
* `loop`은 `let`과 같은 형태로 인자를 받음

## 꼬리재귀

## defn argument or 노테이션

## schema 라이브러리

* [https://github.com/plumatic/schema](https://github.com/plumatic/schema)
* swagger와 함께 schema를 사용할 때, 정해지지 않은 맵을 내려주고 싶으면 다음과 같이 하면 된다.

```text
(defschema body
  {s/Keyword s/Any})

  ...
  :return Body
  ...
```

## file이 있는지 확인하기

```text
> (require '[clojure.java.io :as io] )
> (.exists (io/as-file "test.txt"))
```

## 어제 날짜 구하기 \(clj-time사용\)

```text
(:require [clj-time.core :as t])
;;어제
(t/minus (t/now) (t/days 1))

;;그제
(t/minus (t/now) (t/days 2))
```

