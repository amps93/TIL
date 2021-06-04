# git 명령어

## unix 기본 명령어	

| 명령어                 | 실행 동작                        |
| ---------------------- | -------------------------------- |
| `cd`                   | 홈 디렉토리로 이동               |
| `cd + 경로`            | 경로 디렉토리로 이동             |
| `ctrl+l`               | 화면에 출력된 내용 삭제          |
| `ls`                   | 파일 목록 출력                   |
| `ls -a`                | 파일 목록 출력(숨김 파일까지)    |
| `mkdir`                | 폴더 생성                        |
| `touch`                | 파일 생성                        |
| `start` + 파일/폴더명  | 파일, 폴더 오픈(더블클릭과 동일) |
| `rm -r `+ 폴더명       | 폴더 삭제                        |
| `rm` + 파일명          | 파일 삭제                        |
| `mv` + 파일명 + 폴더명 | 해당 파일을 폴더로 이동          |

## git 명령어

| 명령어                                    | 실행 동작                                     |
| ----------------------------------------- | --------------------------------------------- |
| `git init`                                | 현재 위치의 폴더에서 깃 시작                  |
| `rm -r .git` or `rm -rf .git`             | 깃 종료 (삭제)                                |
| `git add` + 파일명                        | 해당 파일을 스테이지에 올림                   |
| `git add .`                               | 모든 파일을 스테이지에 올림                   |
| `git commit -m 'commit명'`                | 지정한 commit명으로 스테이징에 있는 파일 커밋 |
| `git status`                              | 상태 확인                                     |
| `git restore` + 파일명                    | commit한 상태의 파일로 복원                   |
| `git log`                                 | 커밋 내역 출력                                |
| `git log --oneline`                       | 간단히 커밋 내역 출력                         |
| `git config --global user.name '이름'`    | 사용자 이름 생성 또는 변경                    |
| `git config --global user.email '이메일'` | 사용자 이메일 생성 또는 변경                  |
| `git branch <branch명>`                   | branch 생성                                   |
| `git checkout <branch명>`                 | branch 이동                                   |
| `git switch <branch명>`                   | branch 이동                                   |
| `git switch -c <branch명>`                | branch 생성 후 이동                           |
| `git merge <branch명>`                    | branch 병합                                   |
| `git branch -v`                           | branch 목록                                   |
| `git push origin branch`                  | 데이터를 github에 올림                        |
| `git pull origin master`                  | github의 데이터를 가져옴                      |
| `git clone git_path`                      | 코드 가져오기                                 |
| `git branch -d <branch명>`                | branch 삭제                                   |

