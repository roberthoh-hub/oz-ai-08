# 목차
## 1. 버전 관리의 필요성
 - 버전관리는 왜 필요한가? 
    - Vibe 코딩의 사례를 들어보면, AI를 가지고 코딩했을 때 버전 관리가 어렵다. 코드 A에서 B로 고쳤을 때, AI는 SAVEPOINT가 없다. 다시 A로 돌아가지 못한다. B를 기준으로 A를 만들기 위해 B를 수정할 뿐이다. 
    - 따라서 AI코딩은 버전관리가 어려운 점이 한계점이다.
    - 하나 추가로 덧붙이면 이력을 기록하고 관리하는 이유 중 하나는 개발자/ 작성자의 변경에 대한 의도를 명확히 기록하기 위함이다. 코드 변경 내역만 적혀 있으면 언제 어디서 어떻게 변경되었는지는 알 수 있지만, 변경해야 했던 이유를 빠르게 파악할 수 있기 위해서는 개발자의 의도도 함께 기록되면 좋다. 
 - 버전관리의 방식으로 Git이 적합한 이유는?
    - 변경 내용이 커밋 단위로 기록된다.
    - 언제든 특정 시점으로 되돌릴 수 있음.
    - 여러 사람이 동시에 작업 가능합니다.
    - 변경 이력과 책임이 명확합니다.

## 2. Git 기본 개념
### 2.1 Git 과 GitHub
 - Git은 버전 관리를 위한 도구(프로그램)임. 내 컴퓨터에서 동작함.
 - GitHub는 Git 저장소에 올려두는 웹 서비스. 
    - Pull Request, Issue, Review 기능을 제공함.
    - 협업과 공유를 위한 서비스
### 2.2 Repository
 - 정의: 파일과 그 변경 이력을 함께 관리하는 저장소 : 프로젝트 전체와 모든 버전 기록이 들어 있었음.
 - 종류: 크게 로컬 저장소와 원격 저장소로 나눌 수 있다.
    - 로컬 저장소: 내 컴퓨터에 있는 저장소
    - 원격 저장소: GitHub같은 서버에 있는 저장소
### 2.3 Commit
 - 정의: Git에서 하나의 작업 단위를 기록한 것. 변경 사항을 하나의 기록으로 저장하는 단위 (= 하나의 버전)
 - 기능:
    - 무엇을 왜 바꿨는지를 메시지로 남긴다.
    - 특정 시점의 프로젝트 상태를 저장한다.
    - 되돌아갈 수 있는 기준점 역할을 한다.
 - 코드: git commit -m "회원가입 기능 추가"
### 2.4 branch
 - 정의: 독립적으로 작업할 수 있는 작업 공간
    - 기존 코드를 건드리지 않고 기능을 개발할 수 있음.
    - 여러 기능을 동시에 개발할 수 있음.
    - 작업이 끝나면 병합한다.
### 2.5 head
 - 정의: 현재 내가 작업 중인 위치를 가리키는 포인터
    - git log 또는 git log --all을 터미널에 입력하면, 현재 작업 중인 파일의 주소명 오른쪽에 (HEAD -> branch명칭) 형태로 알려준다.
### 2.6 Working Directory
 - 단계: Working Directory에서 repository까지 이동하는 데 거치는 단계는 1가지가 더 있다. Staging Area이다.
    1. Working Directory (.git)
     - 정의: 작업 공간을 의미하며 , "Working Directory 상태에 있다"는 의미는 저장소(Repository)에 내가 작업한 내용이 반영되지 않았음을 의미한다.
     - 프로젝트 폴더
    2. Staging Area
     - 정의: 다음 commit에 포함할 변경 사항을 미리 모아놓는 임시 공간
    3. Repository
     - 정의: 파일과 그 변경 이력을 함께 관리하는 저장소 (local + global)

## 3. Git 설치와 초기 설정
 1. homebrew 설치 (https://brew.sh/)
 - 터미널에 아래 내용 입력 (macOS, Linux, WSL(Windows Subsystem for Linux)용)
   - /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
 2. git 설치방법
 - 윈도우: https://git-scm.com/download/win에서 Git for Windows를 설치한다. (Git for Windows/x64 Setup)
 - macOS: brew install git
 - 리눅스: 터미널에서 sudo apt-get install git 명령을 실행한다.
 3. 설치 확인: git --version
 - git config: Git의 기본 동작을 설정하는 명령어
 - 전역 설정: 모든 저장소에 적용
   - git config --global user.name "홍길동"
   - git config --global user.email "hong@example.com"
 - 로컬 설정: 특정 저장소에만 적용
   - 프로젝트마다 다른 계정이나 역할을 써야 할 때 사용한다. (회사 프로젝트와 개인 프로젝트 구분)
   - git config user.name "홍길동
   - git config user.email "hong@example.com"

## 4. 로컬에서 Git 사용하기
### 4.1 코드: 
   - git --version: 컴퓨터에 git이 설치돼 있는지 확인
   - git init: 현재 폴더를 Git 레포지토리로 초기화
     - git init 을 사용하면 .git 폴더가 생성되며, 현재 폴더를 기준으로 버전 관리가 시작된다.
   - git status: 해당 저장소(repository)의 상태를 확인한다. 
     - 수정된 파일
     - 스테이징 여부
     - 커밋 가능한 변경 사항 확인
   - git add: 변경된 파일을 staging area로 올리는 명령어
     - git add 파일명 / git add . : 커밋에 포함할 변경 사항을 선택하는 단계로, 아직 커밋이 생성된 것은 아님.
   - git commit: 변경  사항을 기록하는 행위. 특정 시점의 프로젝트 상태를 저장함.
     - git commit -m "Create ozcoding.py": ozcoding.py 파일을 생성한다는 메시지를 넣음.
     - 커밋 메시지 작성 규칙: 
     1. 명확하고 간결하게 작성
     2. 동사로 시작
     3. 한 커밋 = 한 작업
     - 좋은 commit 예시
       - Add login API: (로그인용 인터페이스)를 추가한다.
       - Fix password validation bug: 패스워드 인증 버그를 고친다.
       - Refactor user service: 사용자 서비스의 내부 구조를 깔끔하게 수정한다.
   - gitignore: 버전 관리에서 제외할 파일을 지정하는 설정 파일
      - 불필요한 파일이 커밋되는 것을 방지한다. 
      - 예시: .env  __pycache__/ *.log
      - ⚠️ 이미 커밋된 파일은 Git이 계속 추적하기 때문에 git rm --cached 파일명을 적용해야 한다.
       - 참고 : http://codingdog.tistory.com/entry/gitignore%EA%B0%80-%EB%8F%99%EC%9E%91-%EC%95%88-%ED%95%A0-%EB%95%8C-%EC%93%B4%EB%8B%A4%EB%8A%94-git-rm-cached-%EB%AA%85%EB%A0%B9%EC%96%B4%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B4%85%EC%8B%9C%EB%8B%A4
       - git rm .env -f 명령어는 파일 시스템에서 .env를 제거하는 명령어로, 조심해서 써야 한다.
   - git log: Git 저장소의 커밋 히스토리를 최신순으로 조회하는 명령어
      - 이 명령어를 입력하면 커밋 해시, 작성자, 날짜 및 커밋 메시지가 포함된 커밋 히스토리를 볼 수 있다.
      - git log -1 --name-only: 특정 커밋에서 어떤 파일이 변경되었는지 확인 (-1은 마지막 커밋에서 변경된 파일을 확인)
      - git show <commit_hash> --name-only: 특정 커밋 해시를 알고 있을 때, 해당 커밋의 변경 파일을 확인할 수 있다.  
        --name-only 가 붙어 있으면 변경된 파일명만 확인
        --name-only 없이 git show <commit_hash>만 쓰면 변경된 내용을 상세 확인할 수 있음.
 - 참고 사이트 https://wikidocs.net/book/14452 
#### 4.1.1 working directory 유투브 참고 용어정리
 - https://youtu.be/BIjrKuJGTxw?si=2mGaSgIlsoeakcHN
 - 파일 상태:
    - Untracked files: 백업되지 않고 버전 관리가 안 되는 파일
    - Tracked files: Staging Area를 거쳐 Repository에 저장된 파일
 - Git 파일 상태:
    - commited: 스냅샷되어서 repository에 저장됨. (tracked file)과 비슷
    - modified: 편집하거나 삭제된 상태 --> Staging Area 
    - staged: 파일이  staging area에 올라간 상태 (git add) 
## 5. 브랜치 이해하기
### 5.1 Branch
   - 기존 작업과 분리된 독립적인 작업 흐름
   - 기능 개발, 실험, 수정 작업을 안전하게 진행할 수 있음.
   - 협업과 안정적인 배포를 위해서는 브랜치를 잘 관리하는 것이 중요.
 - 주요 명령어:
   - 브랜치 목록 확인: git branch
   - 브랜치 생성: git branch feature/ui  원본 파일을 복사하여 branch에 feature/ui를 만듦.
   - 브랜치 전환: git switch feature/ui  feature/ui 저장소로 head(현재 작업 중인 위치를 가리키는 포인터)를 옮김.
### 5.2 브랜치 관리 전략
 1. 어떻게 브랜치를 나누고 합칠지 약속
   - 예시: 
      - main: 배포 가능한 안정 버전
      - dev: 개발 중인 기능을 테스트하는 버전
      - feature/*: 기능 개발
      - hotfix/*: 긴급 수정
 2. 브랜치 병합 
   - git merge: 다른 브랜치의 작업 내용을 현재 브랜치로 합치는 명령어.
 3. Fasts-forward vs. 3-way merge
   - Fast-forward merge
      - 브랜치가 직선으로 이어질 때
      - 단순히 커밋 포인터만 이동
   - 3-way merge
      - 브랜치가 갈라졌다가 다시 합쳐질 때
      - 병합 커밋이 생성됨.
   - 분기가 없으면 Fast-forward, 분기가 있으면 3-way merge 
 4. Merge conflict 해결 
   - 같은 파일의 같은 부분을 서로 다르게 수정하면 충돌이 발생.
   해결 방법:
   1. 충돌 파일을 확인
   2. 충돌 코드를 직접 수정
   3. 새로운 커밋 생성
 5. 
## 6. 협업 실습
## 7. 자주 사용하는 명령어