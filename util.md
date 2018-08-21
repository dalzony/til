# Util

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

