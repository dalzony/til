# Util

## oh-my-zsh 설치

```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## mac 키 설정 관련

- 맥이 요즘(?) caps lock 대신 한/영 키를 지원하는데, 나는 caps lock을 ctrl로 쓰는 사람이라 매우 불편하다.
- 시스템 설정등에서 바꿀 수 있다.

### 한/영 키 설정 해제

<img width="265" alt="2018-08-27 5 19 52" src="https://user-images.githubusercontent.com/562341/44831564-15f5c180-ac62-11e8-99a8-e4f87f9500e6.png">


### caps lock을 control로 바꾸기

시스템 환경 설정 > 키보드 > (오른쪽 하위의) 보조키

<img width="419" alt="2018-08-30 2 44 15" src="https://user-images.githubusercontent.com/562341/44831824-307c6a80-ac63-11e8-929c-187c7f6206a4.png">

### 한/영키 변환은 cmd+space로

<img width="599" alt="2018-08-27 5 21 53" src="https://user-images.githubusercontent.com/562341/44831563-15f5c180-ac62-11e8-84b8-ca36de29be37.png">

- 덤: spotlight는 control + cmd + space 로 수정


## 리눅스: 한글 폰트 확인 및 설치하기

```
# 설치된 폰트 리스트 확인
fc-list

# 한글 폰트 리스트를 확인
fc-list :lang=ko
```

```
# 원하는 폰트를 다운로드 받아 다음 경로에 넣는다.
/usr/share/font

# 폰트 캐시 갱신
fc-cache -frv 

# 설치 폰트 리스트를 확인
fc-list
```

### 추가 설정이 필요할 경우

~~위 처럼 했는데도 뭔가 안될때~~

다음 내용의 출처: http://firehouse.tistory.com/24

```
# 설치
yum -y install kde-18in-Korean

# 설정 & 적용

>vim /etc/sysconfig/i18n

LANG="ko_KR.eucKR"
SUPPORTED="en_US.iso885915:en_US:en:ko_KR.eucKR:ko_KR:ko"
SYSFONT="latarcyrheb-sun16"
SYSFONTACM="8859-15"
>source /etc/sysconfig/i18n

# 설정 확인

>locale

# 별칭 확인, 없다면 추가

>vim /usr/share/locale/locae.alias
korean          ko_KR.eucKR
korean.euc      ko_KR.eucKR
ko_KR           ko_KR.eucKR

```
## 현재 listen하고 있는 port를 아는 방법

```text
sudo lsof -PiTCP -sTCP:LISTEN
```

## 터미널에 gg를 치면..

git ui가 나온다...~~굿게임~~

