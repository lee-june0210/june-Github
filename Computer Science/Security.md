# <PART. 보안> 
## Security



### 대칭키(=비밀키) vs 공개키 

대칭키
--------
* 암호화와 복호화에 사용하는 키가 같은 암호화 알고리즘
* 암호화 시스템 중 가장 오래된 방법
* 보내는 사람과 받는 사람이 같은 키를 가지고 있다.
* 암호문이 만들어지고 전송된 후에 암호문은 암호화할 때 사용한 키와 같은 키로 해독되어 원래의 평문으로 바뀔 수 있다. 
<img scr = "https://user-images.githubusercontent.com/76678910/106417626-e3d29480-6497-11eb-8a08-8a51297d9962.PNG" height = 55% width = 55%> </img>


공개키
---------
* 암호화할 때의 키는 공개키(public key), 복호화할 때의 키는 개인키(private key)
* RSA가 대표적
* 부인방지 가능
* 암호화의 처리속도가 비밀키 기법에 비해 느림.
*

<img src = "https://user-images.githubusercontent.com/76678910/106417494-8b9b9280-6497-11eb-9a93-c75d224e249c.PNG" height = 55% width = 55%></img>
