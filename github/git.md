# git

## git과 github

* git 
  * 분산형 버전 관리 시스템
  * 여러명이 동시에 작업하는 병렬 개발이 가능
  * 일종의 사진첩이라고 생각하면 편하다
* github : 드라이브
  * git을 기반으로 소스코드를 호스팅, 협업 지원 기능들을 지원하는 웹서비스
  * 일종의 드라이브라고 생각하면 편하다

## git project PRE-TODO list

1. 프로젝트 폴더를 만든다
2. `.gitignore`와 `README.md` 파일을 생성한다
   1. `.gitignore`파일은 git의 파일관리에서 무시할 내용을,
   2. `README.md`는 프로젝트의 소개 및 정리 내용을 담는다
3. `$ git init`을 한다
4. **주의**
   1. `git/` 폴더와 `.gitignore` 파일과 `README.md` 파일이 같은 위치에 존재하는지 확인
5. 첫번째 커밋을 한다

## git을 시작하기 전에

* <strong>절대 홈디렉토리(c:/user/amps)에 git init 쓰지말것 (홈디렉토리를 마스터 폴더로 지정하지 말것)</strong>
* 혹시 했다면 홈폴더에서 `rm -rf .git` 사용해 git 삭제

## git 동작 순서

1. `git init` 명령어 사용해 master 디렉토리 지정
2. master디렉토리 내의 파일 수정 후 저장(working directory)
3. `git add` 명령어 통해 변경된 상태를 staging area에 올림
4. `commit` 명령어 통해 commit 수행 
