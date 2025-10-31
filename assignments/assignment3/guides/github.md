# GitHub 사용법 가이드

이 가이드는 과제 제출에 필요한 GitHub의 기본 사용법을 다룹니다. Git과 GitHub에 익숙하지 않아도 브라우저만으로 과제를 제출할 수 있습니다.

---

## 목차
1. [GitHub 기본 개념](#1-github-기본-개념)
2. [브라우저로 과제 제출하기](#2-브라우저로-과제-제출하기)
3. [Git CLI 기본 사용법 (선택)](#3-git-cli-기본-사용법-선택)
4. [자주 묻는 질문 (FAQ)](#4-자주-묻는-질문-faq)
5. [문제 해결 (Troubleshooting)](#5-문제-해결-troubleshooting)

---

## 1. GitHub 기본 개념

### 1.1 주요 용어

| 용어 | 설명 |
|------|------|
| **Repository (레포지토리)** | 프로젝트 파일과 히스토리를 저장하는 공간 (줄여서 "repo") |
| **Fork (포크)** | 다른 사람의 레포지토리를 내 계정으로 복사하는 것 |
| **Clone (클론)** | 레포지토리를 내 컴퓨터로 다운로드하는 것 |
| **Commit (커밋)** | 변경사항을 저장하는 단위 (스냅샷) |
| **Pull Request (PR)** | 내가 만든 변경사항을 원본 레포지토리에 반영해달라고 요청하는 것 |
| **Merge (머지)** | Pull Request를 승인하여 변경사항을 반영하는 것 |
| **Branch (브랜치)** | 독립적인 작업 공간 (기본 브랜치는 `main` 또는 `master`) |

### 1.2 과제 제출 흐름

```
1. 원본 레포지토리 Fork
   ↓
2. 내 레포지토리에서 파일 작성/수정
   ↓
3. 변경사항 Commit
   ↓
4. Pull Request 생성
   ↓
5. 교수/조교가 리뷰 후 Merge
```

---

## 2. 브라우저로 과제 제출하기

브라우저만으로 과제를 제출할 수 있습니다. CLI 설정이 필요 없습니다!

### 2.1 Repository Fork 하기

1. **원본 레포지토리 접속**
   - 예: [https://github.com/HUFS-LAI-Seungtaek/HUFS-LAI-ML4E-2025-2](https://github.com/HUFS-LAI-Seungtaek/HUFS-LAI-ML4E-2025-2)

2. **Fork 버튼 클릭**
   - 우측 상단의 `Fork` 버튼 클릭
   - `Create Fork` 버튼 클릭 (기본 설정 그대로 사용)

3. **내 레포지토리 확인**
   - Fork가 완료되면 자동으로 내 레포지토리로 이동
   - URL이 `https://github.com/{내_계정명}/HUFS-LAI-ML4E-2025-2`로 바뀜

**참고**: Fork는 한 번만 하면 됩니다. 이후 과제는 같은 레포지토리에서 작업합니다.

---

### 2.2 파일 생성 및 수정하기

#### 방법 1: 브라우저에서 직접 작성 (권장)

1. **파일 생성**
   - `Add file` > `Create new file` 클릭
   - 파일 경로 입력 (예: `projects/2025122_paper-bot/proposal.md`)
     - 폴더를 만들려면 `/`를 입력하면 자동으로 폴더가 생성됨

2. **파일 작성**
   - 편집기에 내용 작성
   - Preview 탭으로 Markdown 미리보기 가능

3. **커밋 (저장)**
   - 페이지 하단의 `Commit changes` 섹션으로 스크롤
   - Commit message 입력 (예: `Add project proposal`)
   - `Commit changes` 버튼 클릭

#### 방법 2: 파일 업로드

1. **파일 업로드**
   - `Add file` > `Upload files` 클릭
   - 파일을 드래그 앤 드롭하거나 선택
   - Commit message 입력 후 `Commit changes` 클릭

**팁**:
- 한 번에 여러 파일을 업로드할 수 있습니다
- 폴더째 드래그하면 폴더 구조가 유지됩니다

---

### 2.3 Pull Request 생성하기

1. **내 레포지토리 메인 페이지로 이동**

2. **Contribute 섹션 확인**
   - Fork한 레포지토리가 원본과 다르면 `Contribute` 버튼이 표시됨

3. **Pull Request 열기**
   - `Contribute` > `Open pull request` 클릭
   - 또는 상단의 `Pull requests` 탭 > `New pull request` 클릭

4. **PR 내용 작성**
   - **Title**: `3rd Assignment by {학번} ({영어 이름})`
     - 예: `3rd Assignment by 2025122 (Seungtaek Choi)`
     - ⚠️ 포맷을 정확히 지켜야 합니다!

   - **Description**:
     ```markdown
     - `projects/{학번}_{프로젝트명}/proposal.md` 파일 제출합니다.
     - 프로젝트명: {한글 프로젝트명}
     ```

5. **Create pull request 클릭**

6. **PR 확인**
   - PR이 생성되면 원본 레포지토리의 Pull requests 탭에서 확인 가능
   - 교수/조교가 코멘트를 남기거나 변경을 요청할 수 있음

---

### 2.4 PR 수정하기

PR을 생성한 후에도 수정이 가능합니다.

1. **내 레포지토리에서 파일 수정**
   - 파일로 이동 > 연필 아이콘(Edit) 클릭
   - 수정 후 `Commit changes` 클릭

2. **자동 반영**
   - 같은 브랜치에 커밋하면 PR에 자동으로 반영됨
   - PR 페이지에서 변경사항 확인 가능

**팁**: PR이 merge되기 전까지는 언제든지 수정 가능합니다.

---

## 3. Git CLI 기본 사용법 (선택)

CLI(Command Line Interface)를 사용하면 더 효율적으로 작업할 수 있습니다.

### 3.1 Git 설치 및 설정

#### 설치 확인
```bash
git --version
```

#### 초기 설정
```bash
# 사용자 이름 설정
git config --global user.name "Your Name"

# 이메일 설정 (GitHub 계정 이메일)
git config --global user.email "your.email@example.com"

# 설정 확인
git config --list
```

---

### 3.2 Repository Clone 하기

```bash
# HTTPS로 클론 (권장)
git clone https://github.com/{내_계정명}/HUFS-LAI-ML4E-2025-2.git

# 디렉토리 이동
cd HUFS-LAI-ML4E-2025-2
```

**SSH vs HTTPS**:
- HTTPS: 간편하지만 매번 비밀번호 입력 필요
- SSH: 초기 설정이 필요하지만 이후 편리함

---

### 3.3 기본 Git 명령어

#### 상태 확인
```bash
# 현재 상태 확인
git status

# 변경 내역 확인
git diff

# 커밋 히스토리 확인
git log
git log --oneline  # 간단히 보기
```

#### 변경사항 커밋
```bash
# 파일 추가 (staging)
git add 파일명
git add .  # 모든 변경사항 추가

# 커밋
git commit -m "커밋 메시지"

# 추가 + 커밋 동시에
git commit -am "커밋 메시지"  # 새 파일은 포함 안 됨
```

#### 원격 저장소와 동기화
```bash
# 원격 저장소에 푸시
git push origin main

# 원격 저장소에서 풀
git pull origin main

# 원격 저장소 확인
git remote -v
```

---

### 3.4 CLI로 과제 제출하기

```bash
# 1. 레포지토리 클론
git clone https://github.com/{내_계정명}/HUFS-LAI-ML4E-2025-2.git
cd HUFS-LAI-ML4E-2025-2

# 2. 파일 작성
mkdir -p projects/2025122_paper-bot
nano projects/2025122_paper-bot/proposal.md  # 또는 원하는 에디터 사용

# 3. 변경사항 커밋
git add projects/2025122_paper-bot/proposal.md
git commit -m "Add project proposal for paper translation bot"

# 4. 원격에 푸시
git push origin main

# 5. 브라우저에서 PR 생성
# GitHub에서 Contribute > Open pull request
```

---

### 3.5 브랜치 사용하기 (고급)

```bash
# 새 브랜치 생성 및 이동
git checkout -b assignment3

# 브랜치 확인
git branch

# 작업 후 커밋
git add .
git commit -m "Complete assignment3"

# 브랜치 푸시
git push origin assignment3

# main 브랜치로 이동
git checkout main

# 브랜치 병합
git merge assignment3
```

---

## 4. 자주 묻는 질문 (FAQ)

### Q1. Fork와 Clone의 차이는?

| Fork | Clone |
|------|-------|
| GitHub 웹에서 수행 | 로컬 컴퓨터에서 수행 |
| 다른 사람의 레포를 내 계정으로 복사 | 레포를 내 컴퓨터로 다운로드 |
| 원본과 연결 유지 | 로컬에서 작업 |

**과제 제출 흐름**: Fork (GitHub) → Clone (선택, 로컬 작업) → Push → Pull Request

---

### Q2. PR을 잘못 만들었어요. 삭제할 수 있나요?

**답**: 네, 가능합니다.
1. PR 페이지 하단으로 스크롤
2. `Close pull request` 클릭
3. 필요시 다시 PR 생성

**팁**: PR을 닫아도 원본 레포에는 영향이 없습니다.

---

### Q3. Commit message를 어떻게 작성하나요?

**좋은 커밋 메시지**:
- 명확하고 간결하게
- 무엇을 했는지 설명
- 영어 또는 한글 (일관성 유지)

**예시**:
```
✅ Add project proposal
✅ Fix typo in proposal.md
✅ Update technical stack section
✅ 프로젝트 제안서 추가

❌ asdf
❌ fix
❌ ㅇㅇ
```

---

### Q4. Fork한 레포를 원본과 동기화하고 싶어요

**브라우저 방법**:
1. Fork한 레포 메인 페이지
2. `Sync fork` 버튼 클릭
3. `Update branch` 클릭

**CLI 방법**:
```bash
# 원본 레포를 upstream으로 추가 (최초 1회)
git remote add upstream https://github.com/HUFS-LAI-Seungtaek/HUFS-LAI-ML4E-2025-2.git

# 원본에서 최신 변경사항 가져오기
git fetch upstream

# main 브랜치로 이동
git checkout main

# 원본의 main 브랜치와 병합
git merge upstream/main

# 내 원격 레포에 푸시
git push origin main
```

---

### Q5. 실수로 잘못된 파일을 커밋했어요

**아직 Push 하지 않은 경우**:
```bash
# 마지막 커밋 취소 (변경사항은 유지)
git reset --soft HEAD~1

# 마지막 커밋 완전히 취소
git reset --hard HEAD~1
```

**이미 Push한 경우**:
```bash
# 파일 삭제 후 새로운 커밋
git rm 파일명
git commit -m "Remove wrong file"
git push origin main
```

**브라우저 방법**:
1. 파일 삭제: 파일로 이동 > 휴지통 아이콘 클릭
2. Commit changes

---

## 5. 문제 해결 (Troubleshooting)

### 문제 1: `Permission denied` 에러

**원인**: GitHub 인증 문제

**해결**:
```bash
# HTTPS 사용 (권장)
git remote set-url origin https://github.com/{내_계정명}/레포명.git

# GitHub Personal Access Token 사용
# Settings > Developer settings > Personal access tokens > Generate new token
# Token을 비밀번호 대신 사용
```

---

### 문제 2: `Merge conflict` 발생

**원인**: 같은 파일의 같은 부분을 동시에 수정

**해결**:
1. **브라우저**: GitHub이 자동으로 conflict 표시
   - Resolve conflicts 버튼 클릭
   - 충돌 부분 수정 후 Mark as resolved

2. **CLI**:
```bash
# 충돌 파일 확인
git status

# 파일 열어서 충돌 부분 수정
# <<<<<<< HEAD
# 내 변경사항
# =======
# 상대방 변경사항
# >>>>>>> branch-name

# 충돌 해결 후
git add 파일명
git commit -m "Resolve merge conflict"
git push
```

---

### 문제 3: 파일이 너무 커서 push가 안돼요

**원인**: GitHub는 100MB 이상 파일을 거부

**해결**:
```bash
# 큰 파일 제거
git rm --cached 파일명

# .gitignore에 추가
echo "큰파일명" >> .gitignore

# 커밋
git commit -m "Remove large file"
git push
```

**팁**:
- 데이터셋, 모델 파일은 Git에 올리지 말고 외부 링크 사용
- `.gitignore`에 `*.pkl`, `*.h5`, `*.pth` 등 추가

---

### 문제 4: 커밋 히스토리를 깨끗하게 유지하고 싶어요

**너무 많은 커밋 합치기**:
```bash
# 최근 3개 커밋을 하나로 합치기
git rebase -i HEAD~3

# 에디터에서:
# pick 첫번째커밋
# squash 두번째커밋
# squash 세번째커밋

# Force push (주의!)
git push -f origin main
```

**⚠️ 주의**: Force push는 협업 시 문제를 일으킬 수 있습니다. 개인 브랜치에서만 사용하세요!

---

## 추가 리소스

### 공식 문서
- [GitHub Docs](https://docs.github.com/)
- [Git Book (한글)](https://git-scm.com/book/ko/v2)
- [GitHub Skills](https://skills.github.com/)

### 시각적 학습
- [Visualizing Git](https://git-school.github.io/visualizing-git/)
- [Learn Git Branching](https://learngitbranching.js.org/?locale=ko)

### 치트시트
- [GitHub Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Atlassian Git Cheatsheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)

### GitHub Desktop (GUI)
Git CLI가 어렵다면 GitHub Desktop을 사용해보세요:
- [GitHub Desktop 다운로드](https://desktop.github.com/)
- 드래그 앤 드롭으로 커밋, 푸시 가능

---

## 마무리

GitHub는 처음에는 어려워 보이지만, 몇 번 사용하다 보면 익숙해집니다.

**과제 제출을 위한 최소한의 지식**:
1. Fork하기
2. 파일 작성/수정하기
3. Commit하기
4. Pull Request 만들기

**더 나아가기**:
- CLI 사용법 익히기
- 브랜치 활용하기
- 협업 워크플로우 이해하기

궁금한 점이 있으면 언제든지 질문하세요!

Happy Coding! 🚀
