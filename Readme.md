### UI 및 static 파일 관련 git 리포지트리 작업은 데스크탑 Git tortoise 사용
### 기능 및 개발 관련 git 리포지트리는 Eclipse 프로젝트내에서 Git bash 사용
### Git Subtree 장점 
	* 서브 리포지트리를 Copy 하는 개념이므로 CI-CD 배포시 브랜치 및 리포지트리를 연동 시키기 위해 따로 추가 작업이 없음
	* SYNC에 대한 우려가 없으므로 직관적으로 작업 할 수 있음  
### Git Subtree 단점
	* 개발 리포지트리에서 static 파일을 수정시 개발기 리포지트리와 서브트리 리포지트리 두곳에 동시에 push를 해주어야 함
	* 서브트리 리포지트리 push 시 git bash에서 command 명령어로 푸쉬 해야함




## UI 작업 GIT SUBTREE
### UI git 리포지트리 설치 및 PUSH 방법	

	1. Git tortoise 다운로드 및 설치
	2. 폴더 생성 후 마우스 우클릭으로 GIT Clone 선택
	3. Gitlab에 UI 리포지트리 주소를 URL에 복사 프로젝트 생성
	4. 프로젝트 작업 후 해당 프로젝트 우 클릭 후 Git Commit -> master 선택
	5. Commit 클릭 -> Push 클릭 
	6. 해당 리포지트리에서 push된 정보 확인

### UI git 리포지트리 Pull 방법

	1. 해당 폴더 마우스 우 클릭 Tortoise Git -> Pull 선택
	2.  해당 폴더에 Pull 된 정보 확인
	(매 작업전 실행)

### 다른 브랜치 선택 및 작업

	1. 해당 프로젝트에서 Remote Branch 에서 옵션 선택
	2. 원하는 브랜치 pull (예: a-branch)
	3. 해당 프로젝트 -> 우클릭 -> TortoiseGit -> Switch/Checkout -> a-branch 선택
	4. Push 할 때 Git commit -> “a-branch”선택으로 레포지트리에 push
	5. Pull 받아 올 때 Remote Branch 에서 a-branch 선택 후 pull
   

## 개발 작업 GIT SUBTREE
### 해당 프로젝트 Subtree 리포지트리 등록 방법
	
	1. 해당 프로젝트를 우클릭 후 Git bash 또는 Terminal 선택
	2. git remote -v  (깃 리모트 리포짓 확인)
	3. git remote add static_repo https://github.com/vince15dk/spring-boot- subtree-bottom.git (서브트리로 연결할 깃 리모트 리포지트리 추가, 리포지트리  	이름: static_repo) * private git 리포지트리 인 경우 id, password 추가 - git remote add static_repo  	http://sukjoo.kim:sukjoo123@mbrane-gitlab.e4net.net/sukjoo.kim/subtree-  bottom.git 
	4.  git subtree add --prefix=src/main/resources/static static_repo master  (static_repo가 참조하는 원력 repo의 master 브랜치 내용을 	src/main... 디렉토리로  물리적으로 가져옴)
	5. Working tree has modifications.  Cannot add. (만약 이런 문구가 뜨면 git status  명령어를 입력하여 현재 tree가 clean 상태를 유지) 
	6. git status 입력 후  git subtree add --prefix=src/main/resources/static  static_repo master  다시 실행  7. static 폴더가 나타나지 않으면 maven 	update 실행 시키면 나타남

### UI 작업의 CSS, JS 등 Static파일 수정 후 Push된 내용을 Pull 하는 방법
	
	1. 해당 프로젝트를 우클릭 후 Git bash 또는 Terminal 선택
	2. git subtree pull --prefix=src/main/resources/static static_repo master (해당  프로젝트 src/main...폴더에 pull)  * git subtree pull 	--prefix=src/main/resources/static static_repo mvp (mvp  브랜치)  * 최초 pull을 실행 할 경우 remote repository에 한번 push 필요 
	3. Working tree has modifications.  Cannot add. (만약 이런 문구가 뜨면 git status  명령어를 입력하여 현재 tree가 clean 상태로 만들고 다시 명령어 실행)

### UI를 직접 수정후 PUSH 하는 방법
	
	1. 이클립스에서 Gitlab 레포지트리로 Push (sub와 자신 두곳에 push 필요)
	2. 해당 프로젝트를 우클릭 후 Git bash 또는 Terminal 선택
	3. git subtree push --prefix=src/main/resources/static static_repo master (해당  프로젝트 src/main...폴더 내용을 push)
	4. Working tree has modifications.  Cannot add. (만약 이런 문구가 뜨면 git status  명령어를 입력하여 현재 tree가 clean 상태로 만들고 다시 명령어 실행)  5. 	Push 후 UI 작업 리포지트리에서 Pull을 받으면 수정이 반영되어 있음
