# Gitlab

### Project 생성

- Gitlab에서는 project라고 함
    
    Github에서는 repository라고 함
    
- project URL은 본인이 아이디로 설정하자 ⇒ 그룹 이름으로 하면, 내가 만든걸 그룹 사람들이 다 볼 수 있음…

### Clone 하기

- 바탕화면에 불러올 것이므로, 바탕화면에서 git bash 열기
- `git clone {깃랩 url}` 실행
- 로그인 창 뜨면 Gitlab 로그인하기

---

# Git revert

- 특정 commit을 없었던 일로 만드는 작업
- “재설정” ⇒ 단일 commit을 실행 취소 하는 것임
- 프로젝트 기록에서 commit을 없었던 일로 처리 후 그 결과를 새로운 commit으로 추가함
- `git revert {commit id}`
    - commit id : `git log --oneline`을 통해 볼 수 있는 난수 값! ⇒ revert 하고 싶은 버전의 commit id를 작성하면 됨
    - 실행하면 vim 창이 뜬다.
        - 맨 윗 줄 : commit 메시지
        - `insert` 또는 `i` 키 눌러서 수정 모드로 변환하여, 수정할 부분 수정하면 됨
        - 수정 완료 후에는 `esc`
        - `:wq` 로 저장 후 나오기
- 로그를 살펴보면, revert된 기록이 남음!
- *그런데 revert를 잘못해버렸다면???*
    - revert 했던 commit id를 가지고 revert를 다시 수행해주면 됨
    - git이 revert한 걸 다시 revert 했다고 판단하면 Reapply라고 뜨기도 함!
- 만약 A라는 파일이 생성된 로그가 있고, A라는 파일을 수정해서 commit한 경우라면,
    
    A 수정 로그와 이전에 A 생성 로그는 다른 로그이므로, A가 생성된 로그를 가지고 revert를 하면 수행이 되지 않음!
    
    - `git revert --continue` 하면 되긴 함

### git revert 정리

- 변경 사항을 안전하게 실행 취소할 수 있도록 도와주는 순방향 실행 취소 작업
- commit기록에서 commit을 삭제하거나 분리하는 대신, 지정된 변경 사항을 반전시키는 새 commit을 생성
- git에서 기록이 손실되는 것을 방지하며 기록의 무결성과 협업의 신뢰성을 높임

### revert 추가 명령어

- 공백 또는 ..을 사용해 여러 commit을 한꺼번에 실행 취소 가능
- `git revert --no-edit {commit id}`
    - vim을 켜지 않고 자동으로 commit 진행

---

# Git reset

- “되돌리기” ⇒ 시계를 마치 돌리는.. 아예 되돌렸다는 기록조차 없고 찐으로 되돌리는 것임
- `git reset [옵션] {commit id}`
- reset은 과거 commit으로 되돌아간 후 되돌아간 commit 이후 commit들이 삭제됨
- 특정 버전을 과거로 돌아가는 것임 ⇒ Staging Area에서 어디까지 돌아가는지
    - 삭제되는 commit들의 기록을 어떤 영역에 남겨둘 것인지는 옵션을 이용해 지정함
        
        ⇒ 어떤 상황에서 reset을 사용하는 것인지 잘 생각하고 옵션을 잘 사용하자!
        
- 아직 개발 단계에서 나 혼자 작업을 하고 있었던 상황에서 되돌려야 할 때 사용

### reset의 3가지 옵션

- `--soft`
    - 삭제된 commit 기록을 Staging Area에 남김
    - 내가 첫번째 것을 reset했다면, 두번째 세번째 것은 SA에 add 되어있는 상태가 됨
        
        ⇒ `git status`를 통해 확인해보면 됨
        
    - 만약 1일차 2일차 모두 로그인 기능을 수행했는데, 합치고 싶다면?
        - reset --soft를 하면 둘 다 SA로 갈 것이기 때문에, 그 상태에서 commit하면 하나로 합쳐서 commit 될 것임!
- `--mixed`
    - 삭제된 commit 기록을 Working Directory에 남김 ⇒ 가장 많이 사용함, 기본값 설정임
    - 내가 첫번째 것을 reset했다면, 두번째 세번째 것이 WD에 있는 상태(두번째 세번째 파일은 tracking 되지 않는 상태 == 단순히 로컬에 있는 상태)가 됨
        
        ⇒ `git status`를 통해 확인해보면 됨
        
- `--hard`
    - 삭제된 commit 기록을 남기지 않음 ⇒ 코드 작업했었던 사실을 아예 없애는 것임…!
    - 물론 버전 관리라서 삭제 기록이 남아 있긴하지만… 그래도 사용은 하지 말자!

---

# Git branch

- 나뭇가지처럼 여러 갈래로 작업 공간으로 나누어 독립적으로 작업할 수 있도록 도와주는 Git의 도구

### git branch 장점

1. 독립된 개발 환경을 형성하기 때문에 원본에 대해 안전
2. 하나의 작업은 하나의 브랜치로 나누어 진행되므로 체계적으로 협업과 개발이 가능
3. 손쉽게 브랜치를 생성하고 브랜치 사이를 이동할 수 있음

### branch를 꼭 사용해야 할까?

- 만약 상용 중인 서비스에 발생한 에러를 해결하려면?
    1. 브랜치를 통해 별도의 작업 공간을 만든다.
    2. 브랜치에서 에러가 발생한 버전을 이전 버전으로 되돌리거나 삭제한다.
    3. 브랜치는 완전하게 독립되어 있어서 작업 내용이 master 브랜치에 아무런 영향을 끼치지 못한다.
    4. 이후 에러가 해결됐다면? 그 내용을 master 브랜치에 반영할 수 있다.

### git branch 명령어

- `git branch` : 브랜치 목록 확인
- `git branch -r` : 원격 저장소의 브랜치 목록 확인
- `git branch {브랜치 이름}` : 새로운 브랜치 생성
- `git branch -d {브랜치 이름}` : 브랜치 삭제 (병합된 브랜치만 삭제 가능)
- 브랜치 이름 짓는 방법
    - 대주제/소주제 형식
    - e.g.) fe/auth/work ⇒ 프론트엔드 작업 중 인증 작업이라는 뜻.. 등등

### git switch 명령어

- 현재 브랜치에서 다른 브랜치로 HEAD를 이동시키는 명령어
- `git switch {다른 브랜치 이름}` : 해당 브랜치로 이동
- `git switch -c {다른 브랜치 이름}` : 해당 브랜치 생성하고 이동
- `git switch -c {다른 브랜치 이름} {commit id}` : 해당 commit을 기준으로 브랜치 생성 후 이동
    - commit id를 따로 기재하지 않으면, 내가 현재 있는 위치를 기준으로 함
- ***주의사항!! Working Directory 파일이 모두 버전 관리가 되고 있는지 반드시 확인해야함!!***
    - switch를 통해 브랜치를 이동 시켜야 하는데, 만약 WD 파일이 버전 관리가 되고 있지 않았다면, 브랜치 이동해도 WD에 파일이 여전히 존재함…
        
        ⇒ 이동한 브랜치도 같은 위치에 해당하게 됨…
        
        ⇒ commit이 없으니까, 브랜치가 나누어질 분기가 없는 것임
        

### git merge 명령어

- 두 브랜치를 하나로 병합
- `git merge {병합 브랜치 이름}`
    - master 브랜치와 dev 브랜치가 있다고 하자.
    - dev라는 개인 작업을 master라는 공동 작업 영역에 병합해야하는 상황
        
        ⇒ master 위치에서 `git merge dev` 를 수행하면 됨!
        
    - 병합 후에는 `git branch -d dev`를 통해 dev 브랜치를 삭제해도 됨

### 3-way merge

- 분기되어서 나간 브랜치에 다른 버전이 있는 경우
- 서로의 변경 사항을 모두 사용할 수 있도록 새 commit을 만들어야 함
- vim으로 이동해서 새 commit 메시지를 작성해서 합치면 됨

### Fast-forward

특정 브랜치에서 분기해나간 또 다른 브랜치에서 작업을 진행하다가 병합을 진행하는데

내가 어느 시점에 바라보고 있었느냐 하는 위치를 앞으로 당기기만 하면 되는 것임 == Fast-forward

- 새로운 커밋을 만들지 않음

### 그래프로 branch 구조 확인하기

- `git log --oneline --graph`

### conflict 충돌 문제

- A는 a 작업, B는 b 작업이 있는데, B도 a 작업을 수정한 부분이 있음
- 3-way merge를 수행하려고 함
- 그럼 충돌이 발생함. A가 수정한 a 작업을 쓸건지? B가 수정한 a 작업을 쓸건지?

### 정리

브랜치 만들고 → 개인작업 하다가 → main 브랜치에 병합하고 → 개인작업은 삭제

---

누군가가 master로 local 작업

조장이 git lab에서 원격 저장소 제작

작업물 push

조장이 팀원들 초대

팀원들이 clone 받아옴

각자 branch 만들고 각자 작업해서 push(master로 병합 안하고 push)

원격 저장소에서 

그 파일을 저장

다른 한 명도 내려 받아서 본인 브랜치에서 똑같은 파일을 수정

master에 merge시키기

그 master에 merge된 것을 pul 받기

---

### 협업 연습하기!

1. 각자 branch 생성 후 작업함 (gayeon)
2. add하고 commit 함 (gayeon)
3. `git push origin gayeon` 으로 push함 (gayeon)
4. Gitlab 홈페이지에 보면 Create merge request 버튼이 뜸 ⇒ master로 merge하게 됨
    1. Create merge request 버튼 누르고
    2. Changes에서 수정된 부분 다시 한번 확인
    3. 최종적으로 Merge 클릭하면 merge 성공!
5. 여기까지 하면 원격저장소(미국컴퓨터ㅋㅋ)에 push된 것임! 따라서 로컬의 master branch에는 변경 내용이 없을 것임
    
    ⇒ `git pull origin master`로 pull 하면, 내 로컬 master에도 똑같이 됨
    

### README.md 파일 동시에 작성 연습!

- A가 수정해서 올렸는데(master 최신본), B는 그 사실을 모르고 수정함(master 이전본)
- B가 merge 하려고 하면 conflict 발생함
- 그럼 B는 본인 branch로 이동해서 master 최신본을 merge하고, ⇒ `git merge master`
    
    그걸 pull 받아서, B가 수정하려고 했던 걸 하면 됨!
    
    내가 합치려고 했던 브랜치 확인 후 거기서 pull 받기
    
    수정된 사항이 있는지 확인해서 conflict 해결
    
    다시 push해두고 .. 
    

### 협업 시 branch 생성 예시

master

- dev
    - front
        - 팀원1
            - 작업1 ⇒ front에 merge하기
            - 작업2
        - 팀원2
            - 작업1 ⇒ 팀원1의 작업이 필요하면, front를 pull 해서 작업하기
            - 작업2
    - back
        - 팀원3
            - 작업1
            - 작업2
        - 팀원4
            - 작업1
            - 작업2

### 중요한 파일 관리

- db 같은 것은 git으로 관리되지 않도록 해야함
    
    ⇒ `.gitignore` 파일을 만들어서, 그 안에 db 파일명 작성해두면 됨
    
- 아래에서 관리할 언어나 프레임워크 입력하면, gitignore 파일 내용이 생성됨!
    
    [gitignore.io](https://www.toptal.com/developers/gitignore/)
    
- git init 시 초기에 gitignore 세팅하는 습관 들이자!
- API KEY 관리
    
    ```bash
    # .env 파일
    OPEN_AI_API_KEY = "BLAH BLAH BLAH"
    ```
    
    ```python
    from dotenv import load_dotenv
    import os # os 조작에 쓰이는 python built-in function
    
    # .env 파일을 열어주는 함수
    load_dotenv()
    
    open_ai_api_key = os.getenv("OPEN_AI_API_KEY")
    ```