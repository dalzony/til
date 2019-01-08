---
description: 요즘은 주로 spacemacs를 쓰고 있습니다.
---

# Emacs-spacemacs

- dotfiles :https://github.com/dalzony/dotfiles/blob/master/spacemacs
- spacemacs 동영상 많은 곳 (설명이 친절한 편)
 - https://www.youtube.com/user/Seorenn
- clojure+spacemacs 설명이 잘된 곳: https://practicalli.github.io/spacemacs/

## 설치

### emacs 설치

- 참고: https://github.com/syl20bnr/spacemacs#macos 에서 잘 가이드 하고 있다


맥 기본 emacs는 버젼이 낮으니까

```sh
brew install emacs

```

그리고 나서

```
$ brew cask install emacs // gui 로 띄우기 위함


$ brew tap d12frosted/emacs-plus
$ brew install emacs-plus
# $ brew linkapps emacs-plus => (linkapp 명령어는 더이상 먹히지 않아서 다음과 같이 수정)
$ ln -s /usr/local/Cellar/emacs-plus/26.1/Emacs.app /Applications 

```

잘되면 spacemacs를 설치한다

```
git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d
```

## `SPC`키는 `M-m`으로 대체

설명들에서 `SPC`키로 하는 커맨드들은 `M-m`으로 대체할 수 있다.

## clojure (mode)

`dotspacemacs-configuration-layers`에 clojure를 추가하면,
별도로 cider를 설치하지 않아도 cider를 쓸 수 있다.

## buffer list 볼 때

```
C-x b buffer <RET>
Select or create a buffer named buffer (switch-to-buffer). 
```

- cider error의 결과가 하단에 뜨는 데 짤려서 안보일 때, *messages* 버퍼를 확인해볼것!
