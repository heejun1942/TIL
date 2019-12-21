# git-flow / github-flow

Git을 이용하여 협업하기 (**브랜칭 기법**)



## git flow

collaborators로 등록된 팀원들의 협업 방법으로, master가 아닌 새로운 branch에서 작업하여 push함

- collaborators만 `push` 가능함

#### [step]

1. repository 생성 >  collaborators 등록

2.  `clone`으로 복제

3. 새로운 branch _(ex. neo)_ 생성 후 작업

4. 작업 후 _neo_를 `push`함

   ```shell
   $ git push origin neo
   ```

5. `push`한 branch 병합을 요청 (**pull request**) 
6. 팀장은 github에서 코드를 확인하고 **merge**함

 



## github flow

github의 오픈소스에 자유롭게 참여할 수 있는 협업방법

#### [step]

1. 참여하고자 하는 repository를 **Fork**하여 나의 github로 복제

2. Fork한 repository를 `clone`하여 컴퓨터로 내려받음

3. 작업 후 내 github 저장소로 `push`

4. 브랜치 왼쪽에 있는 **compare**버튼 클릭

   ![](https://miro.medium.com/max/620/1*QfYdqZoEhtj-tf-QeaHROg.png)

5. **Create pull request** 버튼 클릭하여 메시지와 함께 전송!