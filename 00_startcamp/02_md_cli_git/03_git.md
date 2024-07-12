# Git

- 분산 버전 관리 시스템
    - 저장되는 위치를 분산시키는 것
    - 버전을 여러 개의 복제된 저장소에 저장 및 관리 ⇒ 수정 사항들을 관리
- 변화를 기록하고 추적하는 것
- 코드의 버전(히스토리)을 관리
- 개발되어 온 과정 파악 가능
- 이전 버전과의 변경 사항 비교
- 협업 시 commit을 통해, 해당 코드에 문제 발생 시 담당자에게 물어보기 수월하기 때문

### git의 3가지 영역

- Working Directory
    - 로컬 환경
    - git으로 관리가 되어있을 수도 아닐 수도 있음
- Staging Area
    - git으로 관리할 파일 ⇒ 변경사항만 기록됨
    - 변경된 사항 중 다음 버전에 포함시켜야 할 파일(= Repository에 올릴 파일)을 모아두는 곳
    - commit을 통해 변경 사항들만을 가지고 새로운 버전을 생성
- Repository
    - 새로운 버전으로 생성된 것이 저장되는 곳

### git의 동작

- `git init`
    - git으로 관리하기 위한 디렉토리에서 딱 한 번만 실행하면 됨
    - *git 로컬 저장소 내에 또 다른 git 로컬 저장소를 만들지 말 것!!!*
        - *바깥쪽의 git 저장소가 안쪽의 git 저장소를 인식할 수 없기 때문*
    - (master)라고 뜰 것임 ⇒ 이 폴더로부터 하위 폴더들은 master라는 작업 영역에서 관리하겠다는 뜻
    - `ls -a` 로 디렉토리를 확인해보면, 숨김파일로 .git이 생성되어 있을 것임
        - 변경사항들이 저장될 곳
- `git add {dir_name}`
    - 작업할 디렉토리를 add 해줌 ⇒ Staging Area로 옮기기
        - `git add .` : 현재 경로를 기준으로 모든 하위 폴더를 add 해줌
- `git status`
    - 현재 변경 사항의 상태를 볼 수 있음
    - *nothing to commit, working tree clean 문구 확인하고(= commit 다 하고) 퇴실하자!!!*
- `git commit -m "커밋 메시지"`
    - 내가 어떤 수정사항을 발생시켰는지 알 수 있는 커밋 메시지를 작성
    - *커밋 메시지는 상세하게 작성하자!!!*
- `git config --global user.email "123@123.com"`
    
    `git config --global user.name "이름"`
    
    - 작성자 설정
- `git rm -r --cached 00_startcamp/02_md_cli_git/`
    - Staging Area에 있는 걸 내리고 싶은 경우
- `git log`
    - commit 내용 살펴보기
    - `git log --oneline` : 한 줄로 커밋 메시지 보이기
- **배운 내용 연습 해보자!**
    1. 현재 상태 출력해보기 `git status`
    2. 오늘자 공부한 내용 Staging Area에 옮기기 `git add {dir_name}` 
    3. 현재 상태 출력해보기 `git status`
    4. SA → Repository로 옮겨서 새 버전 남기기 `git commit -m "커밋 메시지"`
    5. 현재 상태 출력해보기 `git status`
    6. 커밋 버전 내역 확인해보기 `git log`

---

# Remote Repository

- 원격 저장소
    - 코드와 버전 관리 이력을 온라인 상의 특정 위치에 저장하여 여러 개발자가 협업하고 코드를 공유할 수 있는 저장 공간
- 원격 저장소의 url을 로컬 컴퓨터에 알려주기
    - 원격 저장소에 업로드 == push 한다
- GitLab, GitHub, Bitbucket 등이 있음

### Git과 GitHub의 차이

- Git은 로컬에서 **버전 관리 시스템**
- GitHub는 Git으로 관리된 버전들을 모아두는 **원격 저장소**

### Remote 연습

1. 작업할 폴더에서 git bash 실행
    - `git init` → 파일 수정 → `git add {dir_name}` … 등등 초기화 후 파일 수정해보기
2. GitHub에서 Repository 생성하기
    - README.md 생성해도 역시나 하나의 버전이 생긴 것임
        
        ⇒ 만약 내가 git init을 한 후에 Repository를 만들었다면 버전 관리하기 복잡해짐
        
        ⇒ 따라서 원격저장소에서 최초로 git init할건지, Repository 만든 후에 할 것인지 잘 생각하고 README 파일 생성 여부 체크하기
        
3. 원격 저장소 연결하기
    - `git remote add origin {레포지토리 url}`
        - 로컬과 원격 저장소 연결하기
        - 앞으로 내 Repository url을 origin이라고 칭하겠다는 뜻
    - `git push origin master`
        - origin이라는 이름으로 master branch에 push 하겠다는 뜻
    - GitHub에서 commit 내역 확인해보기
    - *원격 저장소에 저장됐으므로, 로컬에 있는 해당 폴더는 지워도 상관 없는 것임!*
        
        ⇒ 이런 경우, 원격 저장소에서 로컬로 다시 어떻게 가져오지? (아래에 계속)
        

### 원격 저장소 → 로컬 가져오기 : clone

- Repository에 들어가서 code 부분 클릭해서 HTTPS 부분에 있는 url 복사
- 바탕화면에서 Git BASH 실행
    
    ⇒ `git clone {HTTPS}` 실행
    
    ⇒ 바탕화면에 Repository에 있는 것이 다운로드 됨!
    
- clone은 복붙해오는 거라서, 만약 로컬에 같은 이름으로 폴더가 있으면 못 가져옴
    
    ⇒ 따라서 pull을 사용하자!
    

### Repository에 있는거 clone하고 로컬에서 수정하고 다시 push 하기

- `git clone {HTTPS}`
    
    → 작업하고
    
    → `git add {파일명}`
    
    → `git commit -m "커밋 메시지"`
    
    → `git push origin master`
    

**로컬 → 원격 저장소 : push**

**원격 저장소 → 로컬 : pull**

### 원격 저장소 → 로컬 가져오기 : pull

- 작업할 폴더에서 `git pull origin master` 실행