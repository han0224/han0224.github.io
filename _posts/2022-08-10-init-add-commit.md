---
layout: single
title: "[Git] Git 정리 - git init, git add, git commit"
categories:
  - Git
tag: [git, github]
toc: true
---

## git init

현재 작업하고 있는 디렉토리에 Git 저장소를 생성하기위해 사용하는 명령어

해당 명령어를 사용하면 .git 디렉토리가 생성됨

![init](https://user-images.githubusercontent.com/70616579/183893108-d4ba72ca-0542-4cde-8ca2-eb5e10b7de2f.png){: width="60%" height="60%"}

### .git 디렉토리

- git을 사용한 모든 정보가 담겨져 있는 디렉토리
- 모든 정보가 담겨져 있으므로 매우 중요함

## git add

> git add 명령어는 working directory 상의 변경 내용을 staging area에 추가하기 위해 사용하는 명령어

- working directory: 단어 뜻 그대로 작업 디렉토리로 현재 작업하고 있는 내용들을 뜻한다.
- staging area
  - commit할 준비가 된 변경내용이 Git 저장소에 기록되기 전에 대기하는 장소
  - git add 명령어를 사용하면 현재 working directory에 있는 변경 내용을 staging area에 이동시킬 수 있음

### f1.txt라는 파일을 만들고 해당 파일을 git add를 해보자

> git status: 저장소 상태확인 명령어

![add1](https://user-images.githubusercontent.com/70616579/183905170-5404e8b5-1d38-496d-9d74-5c9c0c3cfed8.png){: width="60%" height="60%"}

"Changes to be committed"에 들어있는 파일은 **Staged 상태**라는 것을 의미한다.

> working directory의 파일은 크기 **Tracked**, **Untracked**로 나뉨.<br/>Tracked파일은 관리대상들을 의미하며, **Unmodefied**와 **Modefied**와 **Staged**상태 중 하나.<br/>**Unmodefied**: 수정하지 않은 파일<br/>**Modefied**: 수정한 파일<br/>**Staged**: 커밋으로 저장소에 기록할 파일(staging area영역에 있는 파일)

#### ❗warining: LF will be replaced by CRLF in [file].

- 유닉스에서 한줄 끝이 LF(Fine Feed)
- 윈도우에서 한줄 끝이 CR(Carriage Return)
- 즉, 한줄 끝이 CRLF로 이로어져 있어 어느쪽을 따라야 할지 git에 혼란을 주어 생긴 경고
- 보통 윈도우에서 core.autocrlf 기능을 킴
  - 코드를 추가할 때 LF로 코드를 조회할때 CRLF로 변환

### git add를 하지 않는다면?

![add2](https://user-images.githubusercontent.com/70616579/183908235-c50b9afb-cb4a-4f29-9e20-9567ca726cba.png){: width="60%" height="60%"}

f2.txt 파일의 경우 git add를 하지 않아 Untracked 상태라는 것을 의미한다.

Untracked 파일은 아직 스냅샷에 넣지않은 파일이다.

<U>파일이 Tracked 상태가 되기전까지는 Git은 절대 그 파일을 커밋하지 않는다.</U>

### tracked 상태파일을 수정하면?

![add3](https://user-images.githubusercontent.com/70616579/183912481-722534a7-7959-408d-9bcf-05000d2ca37d.png){: width="60%" height="60%"}

"changes not staged for commit"에 들어있는 파일은 수정한 파일이 Tracked 상태이지만 아직 Staged 상태가 아니라는 것이다.

Staged 상태로 만들기 위해서는 git add명령어를 사용해야 한다.

### git add 옵션

이제 모든 파일은 add하자

![add4](https://user-images.githubusercontent.com/70616579/183913484-b4d9e2e7-1712-43a9-b256-99e30c3ebe98.png){: width="60%" height="60%"}

`git add . ` 명령어를 이용해 모든 파일을 Staged 상태로 만들어 주었다.

`.`을 인자로 넘기면 현재 디렉토리의 모든 변경 내용을 Staged상태로 바꾸어준다.

`-A`옵션을 사용하면 working directory상의 모든 변경 내용을 모두 staging area영역으로 옮긴다.

`git add .`을 최상위 디렉토리에서 실행한다면 `git add -A`와 동일한 효과를 얻을 수 있다.

## git commit

> 의미있는 변화(버전)에 대해 기록

### staging area의 파일들을 commit하기

![commit1](https://user-images.githubusercontent.com/70616579/183918736-e829b80b-beeb-4322-aca7-f1bea29bb5fa.png){: width="60%" height="60%"}

`git commit -m 1`의 -m을 생략할시 편집기가 켜지며 편집기에서 커밋 메세지를 작성해야한다. 그런 번거로움을 방지하기 위한 옵션

커밋을 하고나서 `git status`명령어로

"nothing to commit, working tree clean"가 출력되면 현재 커밋할 파일이 더 이상 없다는 것을 의미한다.

`git log`명령어를 통해 commit 기록을 확인할 수 있다.

## git add가 필요한 이유

한가지 의문이 들 수 있다. 굳이 `git add`를 할필요가 있을까?

바로 `git commit`을 입력하면 되지 굳이 staging area 영역이 있어 귀찮게 staging area영역에 올리고 올린 파일을 하는 걸까?

> git commit -am [message] 으로 사용하면 git add를 한번에 실행시킬 수 있다.<br/>하지만 최소한 한번은 git add가 필요함(Tracked상태로 변경이 필요하기에)

`commit`을 버전에 대한 기록이라고 한다.

우리는 실수로 commit하는 시키를 놓칠수도 있다. 그럼 2개 이상의 기능이 하나의 commit으로 묶이게 된다.

하지만 `add` 명령어를 사용하면 우리가 여러 기능을 묶어서 올리게 되는 불상사를 막을 수 있게 된다.

그렇기에 `git add` 명령어가 필요한 것이다.

> 참고자료<br/>[생활코딩-지옥에서 온 Git](https://www.youtube.com/playlist?list=PLuHgQVnccGMA8iwZwrGyNXCGy2LAAsTXk), [Git공식 가이드북](https://git-scm.com/book/ko/v2)
