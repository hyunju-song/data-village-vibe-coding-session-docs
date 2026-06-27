# Git 명령어 치트시트

> 막혔을 때 찾아보는 페이지입니다.  
> 더 자세한 설명은 [02 · git으로 협업하기](../02-git-collab.md)를 보세요.

---

> 📎 **회사 노션 상세 자료** — 이 장의 심화 내용과 보충 설명은 노션에 있습니다.  
> 링크: <!-- NOTION_LINK -->

---

## 처음 설정

```bash
git config --global user.name "이름"
git config --global user.email "이메일"
```

레포를 clone하거나 commit하기 전에 한 번만 설정합니다. 이후로는 자동 적용됩니다.

---

## 상태 확인

| 명령어 | 하는 일 |
| --- | --- |
| `git status` | 변경된 파일 목록과 현재 브랜치 확인 |
| `git log --oneline` | commit 이력을 한 줄씩 요약해서 보기 |
| `git log --oneline -10` | 최근 10개만 보기 |
| `git diff` | 아직 스테이징 안 된 변경 내용 확인 |
| `git diff --staged` | 스테이징된 변경 내용 확인 |
| `git branch` | 브랜치 목록 확인 (`*`가 현재 위치) |

---

## 브랜치

| 명령어 | 하는 일 |
| --- | --- |
| `git checkout -b 브랜치이름` | 새 브랜치 만들고 바로 이동 |
| `git checkout 브랜치이름` | 이미 있는 브랜치로 이동 |
| `git checkout main` | main 브랜치로 이동 |
| `git branch -d 브랜치이름` | 브랜치 삭제 (merge된 것만 삭제 가능) |
| `git merge main` | 현재 브랜치에 main 내용 합치기 |

---

## 저장 (스냅샷 찍기)

```bash
git add 파일이름       # 특정 파일만 스테이징
git add .             # 변경된 파일 전체 스테이징
git commit -m "메시지" # 스냅샷 찍기
```

| 좋은 commit 메시지 | 나쁜 commit 메시지 |
| --- | --- |
| `add date filter to dashboard` | `수정` |
| `fix null error in user API` | `fix` |
| `update README with setup guide` | `asdf` |

---

## 원격 저장소 (Bitbucket)

| 명령어 | 하는 일 |
| --- | --- |
| `git push -u origin 브랜치이름` | 처음 push할 때 (원격 브랜치 연결) |
| `git push` | 이후 push (이미 연결된 경우) |
| `git pull` | 원격의 최신 내용 가져와서 합치기 |
| `git fetch` | 원격 변경 내용 가져오기만 (합치지 않음) |
| `git clone URL` | 원격 레포 전체를 내 컴퓨터로 복사 |

---

## 되돌리기

| 명령어 | 언제 | 안전도 |
| --- | --- | --- |
| `git revert HEAD` | push 후, 이미 공유된 commit | ✅ 안전 — 되돌리는 commit을 새로 만듦 |
| `git reset --hard HEAD~1` | push 전, 로컬에만 있는 commit | ⚠️ 위험 — commit 기록 삭제됨 |
| `git stash` | commit 전, 변경 내용 임시 저장 | ✅ 안전 |
| `git stash pop` | stash에 저장한 내용 다시 꺼내기 | ✅ 안전 |

> push한 뒤에는 무조건 `git revert`를 씁니다.

---

## 충돌(conflict) 해결 순서

```
1. git status
   → "both modified:" 파일 확인

2. 파일 열기
   → <<<<<<< HEAD ... ======= ... >>>>>>> 구간 찾기

3. 원하는 내용만 남기고 표시 줄(<<<, ===, >>>) 삭제

4. git add 파일이름

5. git commit -m "resolve merge conflict"
```

---

## 자주 쓰는 패턴

**작업 시작할 때마다**
```bash
git checkout main
git pull
git checkout -b 내-브랜치이름
```

**작업 끝내고 올릴 때**
```bash
git add .
git commit -m "무엇을 했는지"
git push -u origin 내-브랜치이름
```

**main 최신 내용 내 브랜치에 반영할 때**
```bash
git checkout main
git pull
git checkout 내-브랜치이름
git merge main
```
