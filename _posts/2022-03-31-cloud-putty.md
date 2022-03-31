---
layout: single
title: "[AWS EC2] Putty 사용"
categories:
  - Colud Computing
tag: [cloud computing, putty, ubuntu]
toc: true
---

## 🎃 Putty 화면
Putty 를 처음 들어가면
```
ubuntu@ip-000-00-0-000:~$
```
위와 같은 글이 마지막에 써있을 것이다.
하나씩 확인하자면
- ubuntu :  사용자 이름(id)
- ip-000-00-0-000 : 우분투 서버 주소
- ~ : 사용자 홈 디렉토리
- $ : 일반 사용자 프롬포트


한가지 의문이 들 수 있다. 우린 분명 id pw 를 치지 않고 들어왔는데 왜 사용자 id 가 있을까?
> AWS 에서는 리눅스 우분트를 설치하면 자동으로 우분트라는 일반 사용자를 할당 받는다!

AWS 는 일반 사용자를 할당 해준다. 하지만 일반 사용자는 사용에 제한이 있다.    그렇기에 어느정도 권한이 필요한 것들은 사용하지 못한다.

루트 사용자일 경우에는 $ 이 아닌 #으로 표시된다.

## 📂 우분투(리눅스) 계층 구조
우분투는 리눅스 커널을 기반으로 운영체제가 만들어 진 것이다.

그렇기에 리눅스와 계층 구조가 같다.

리눅스의 최상단에는 root 디렉토리가 있고, 아래에 bin, etc, usr, home, boot 같은 디렉토리가 있다.
### 📃 작업디렉토리
사용하다보면 디렉토리를 이동하게 된다. 이때 현재 사용중인 디렉토리를 작업 디렉토리라고 한다.

작업디렉토리의 위치를 확인하려면 pwd 명령으로 확인할 수 있다.
### 🏠 홈 디렉토리
각 사용자에게 할당된 디렉토리로 처음 사용자 계정을 만들 때 지정된다.

Putty 에 ~로 표시된다.

## ✨ 명령어


| 명령어 | 의미 | 사용법|옵션|
|---|:--:-|---|---|
| pwd| 현재 작업 디렉토리 확인 | ubuntu@ip-000-00-0-000:~$ **pwd** <br/>/home/ubuntu|
|ls|파일확인|ubuntu@ip-000-00-0-000:~$ **ls** <br/>cloud  new_test2  son  test2  tmp| `-a`: 숨긴파일도 보임<br/>`-F`: 파일 형식을 알리는 문자를 각 파일 뒤에 추가 <br/> `-l`: 자세히 보기|
|mkdir|디렉토리 만들기|ubuntu@ip-000-00-0-000:~$ **mkdir** test|
|touch|파일 만들기|ubuntu@ip-000-00-0-000:~$ **touch** testfile|
|nano|텍스트 에디터|ubuntu@ip-000-00-0-000:~$ **nano** testfile|새로운 파일 생성도 가능 <br/>가장 기본적인 편집기로 최소한의 기능만 있음|
|vi|텍스트 에디터|ubuntu@ip-000-00-0-000:~$ **vi** testfile|nano 보다 좀 더 다양한 기능이 있음|
|vim|텍스트 에디터|ubuntu@ip-000-00-0-000:~$ **vim** testfile|vi 의 업그레이드 버전|
|cat|파일 속 데이터 출력|ubuntu@ip-000-00-0-000:~$ **cat** testfile<br/>hi|출력할 방향을 바꿀 수 있음<br/> `>new_test2`: new_test2 에 똑같은 내용의 파일이 생성.|
|man|해당 명령어의 사용법을 보여줌|ubuntu@ip-000-00-0-000:~$ **man** ls|
|cd|디렉토리 이동|ubuntu@ip-000-00-0-000:~$ **cd** test<br/>ubuntu@ip-000-00-0-000:~/test$|`cd ..`: 상위 디렉토리로 이동<br/> `cd`: 홈 디렉토리로 이동|
|rm|해당 파일을 지움|ubuntu@ip-000-00-0-000:~$ **rm** testfile|`-i`: 삭제 여부 몰어봄<br/>`-r`: 비어있지 않은 디렉토리 지움|
|rmdir|해당 디렉토리 지움 (단, 디렉토리가 비어있어야 함)|ubuntu@ip-000-00-0-000:~$ **rmdir** test|
|mv|파일이나 디렉토리를 이동시킴<br/>이름 변경 목적으로도 사용 가능|`test2 -> new_test`:<br/> ubuntu@ip-000-00-0-000:~$ mv test2 new_test<br/>`test파일을 new_foler로 옮김`:<br/>ubuntu@ip-000-00-0-000:~$ mv test new_folder|

+ 숨긴파일은 '.'으로 시작