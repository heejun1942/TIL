# CLI

커맨드 라인 인터페이스



## 터미널 명령어들

- `ls`: 폴더 내부의 파일&폴더를 나열
  - `ls -a`: 숨김폴더까지 보여줌
- `pwd`: 현재 폴더 경로 출력
- `mkdir [폴더명]`: 폴더 생성
- `cd [폴더명]`: (change directiory) 폴더 변경
  - `cd ..`: 상위 폴더로 나감
- `git init`: git으로 프로젝트 생성
- `git status`: git의 현재 상태 출력
- `touch [파일명]`: 파일 생성
- `rm [파일명]`: 파일 삭제

### 버전관리

- `git add [파일명]`: 
- `git commit -m [메세지]`: 
- `git log`: 기록 보기
  - `git log --oneline`: 기록 한줄로 보기
- `git checkout`: 과거 버전 보기
- `git checkout master`: 현재로 돌아오기
- `git remote add [저장소 별명] [주소]`: 원격저장소 추가
- `git remote rename [현재이름] [바꿀이름]`: 원격저장소 이름 변경
- `git remote`: 원격저장소 목록을 보여줌

### push_pull

- `git push [저장소 별명] master`: github에 올리기
- `git clone [origin] master`:  복제해서 받아오기 (처음 한번만 사용)
- `git pull [origin] master`: 수정사항만 받아오기

