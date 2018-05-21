# 보안 알고리즘

암호화 Algorithm은 크게 3가지로 나뉜다.

1. Hashing : 복호화 불가능. 단방향. 속도가 빠름
2. Symmetric : 복호화 가능 (private key 사용)
3. Asymmetric : 복호화 가능 (private, public key 사용)

출처: http://js2prince.tistory.com/entry/암호화-MD5-vs-SHA256 [개발은 전투다]

1. Hashing Algorithm

종류 : MD5, SHA1, SHA256, SHA384, SHA512 등 Hash 를 계산할 때 쓰이는 종류이다.
숫자가 클 수록 Hash 값이 복잡해지므로, 더 안전한 암호화 방법이 된다.
예전에는 MD5, SHA1 등 16byte 크기의 Hash 값을 사용했지만, 요즘은 SHA512 등 Hash 값 크기가 큰 알고리즘을 추천한다.

비밀번호등 일치 여부만을 확인하기 위해서 (복호화 불필요) 사용한다.
전에도 밝혔지만 아주 큰 Data의 Identity 를 나타내는 값으로 쓸 수 있다.


요즘은 PBKDF2 이것인듯

2. Symmetric Algorithm

종류 : DES, TripleDES, Rijndael, RC2
대칭형 암호화를 수행하고, 비밀번호 (private key)를 추가할 수 있다.
비밀번호를 사용하면 복호화가 가능하므로, 내부통신 또는 같은 도메인에서 사용한다.
Rijndael이나 RC2를 추천한다.

3. Asymmetric Algorithm

종류 : DSA, RSA (요즘은 RSA가 대세)
공인인증서에서 사용하는 Algorithm으로, private key 뿐 아니라 public key도 있어야 한다. 외부 통신 등에 사용한다.

출처: http://js2prince.tistory.com/entry/암호화-MD5-vs-SHA256 [개발은 전투다]

# 축약 알고리즘

## md5

MD5(Message-Digest algorithm 5)는 말그대로 메시지 축약 알고리즘으로서 128비트의 해쉬를 제공한다. RFC-1321에 정의되어 있으며, 현재는 파일 무결성 검사용으로 많이 쓰이고 있다. 보안 관련 용도로 사용하기도 했지만, 현재 암호화 결함이 별견되어서 SHA1같은 다른 알고리즘을 사용하는것을 권장하고 있다. (MD5의 결함을 이용해서 SSL 인증서를 변조가능하다는것이, 2008년 12월에 발표되기도 했다. http://www.win.tue.nl/hashclash/rogue-ca/)


## sha1

SHA(Secure Hash Standard)는 암호학적 해쉬 함수들을 모아놓은것으로서 SHA-0, SHA-1, SHA-2(SHA-224, SHA-256, SHA-384, SHA-512)등 있다. SHA-1은 160비트의 해쉬를 제공하고, 보안 관련 용도로 많이 사용되고 있다.




# 출처
-[오늘은 어디로 갈까...](http://kangwoo.tistory.com/46)
