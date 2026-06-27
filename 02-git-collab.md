# 02 · git으로 협업하기

`[손]` — 직접 손으로 해봐야 익혀집니다.

> 왜 main에 바로 올리면 안 되는지 충돌로 체감하고, 브랜치 → PR → merge로 안전하게 합치는 법을 연습합니다.

---

## 개념

### git이란

git은 **파일의 변경 이력을 기록하는 도구**입니다.

언제 / 누가 / 무엇을 바꿨는지 스냅샷처럼 저장해 둡니다. 덕분에 실수해도 이전 상태로 되돌릴 수 있습니다.

git으로 관리하는 파일을 원격 서버에 올려두는 공간이 필요합니다. 대표적인 서비스가 **GitHub**과 **Bitbucket**입니다. **우리 회사는 Bitbucket을 사용합니다.** 이 강의에서 나오는 모든 레포와 실습은 Bitbucket에서 진행합니다.

---

### GitHub vs Bitbucket

둘 다 git 저장소를 호스팅하는 서비스입니다. 핵심 차이는 아래 표를 보세요.

| | GitHub | Bitbucket |
| --- | --- | --- |
| 만든 곳 | Microsoft | Atlassian (Jira·Confluence와 같은 회사) |
| 주요 사용처 | 오픈소스, 개인 프로젝트 | 기업 내부 프로젝트 |
| Jira 연동 | 별도 설정 필요 | 기본 지원 |
| 우리 회사 | ✗ | ✅ 사용 중 |

> **git 명령어는 완전히 동일합니다.** `git add`, `git commit`, `git push` — 어느 플랫폼을 쓰든 터미널에서 입력하는 명령어는 한 글자도 바뀌지 않습니다. Bitbucket이냐 GitHub이냐는 "웹 화면"의 차이일 뿐입니다.

이 개념 사이트(SSOT)는 GitHub에 올라가 있지만, **실습·부트캠프 레포는 모두 Bitbucket**에 있습니다.

---

### main 브랜치가 왜 소중한가

레포에는 기본으로 `main`이라는 브랜치가 있습니다. 이곳이 **배포되는 최신 버전**입니다.

여러 명이 main에 동시에 올리면 충돌이 납니다. 내가 올린 내용이 다른 사람의 내용을 덮어쓸 수도 있습니다. 그래서 main에는 **검토를 거친 것만** 올립니다.

---

### 브랜치란

브랜치는 main의 **복사본**입니다. 내 브랜치에서 마음껏 작업해도 main은 건드리지 않습니다.

작업이 끝나면 PR을 열어 검토를 요청하고, 승인되면 merge해서 main에 합칩니다.

```
main ──────────────────────────────► (배포 중)
        │                   ▲
        └── 내 브랜치 작업 ──┘ (PR → merge)
```

---

### PR과 merge

- **PR(Pull Request)** — "내 브랜치를 main에 합쳐도 될까요?" 요청입니다. GitHub에서 버튼을 눌러 열 수 있습니다.
- **merge** — PR이 승인되면 실제로 main에 합치는 동작입니다.

혼자 작업할 때도 이 흐름을 지킵니다. 습관이 돼야 팀 프로젝트에서도 자연스럽게 됩니다.

---

## 쉬운 비유

| git 개념 | 비유 |
| --- | --- |
| main 브랜치 | 최종 제출된 보고서 |
| 내 브랜치 | 내가 작성 중인 초안 |
| commit | 초안에 날짜 도장 찍기 |
| push | 초안을 공유 드라이브에 올리기 |
| PR | 상사에게 "이 초안 본문에 넣어도 될까요?" 요청 |
| merge | 상사가 승인하고 본문에 붙여넣기 |

---

## 해보기

실습 레포(`practice`)에서 진행합니다. 터미널을 열고 레포 폴더로 이동한 뒤 시작하세요.

---

**1. 브랜치 만들기**

```bash
git checkout -b my-first-branch
```

`my-first-branch`라는 이름의 새 브랜치를 만들고 바로 이동합니다.

```bash
git branch
```

현재 브랜치 목록이 나옵니다. `*` 표시가 있는 것이 지금 내 위치입니다.

---

**2. 파일 수정 후 저장**

텍스트 에디터로 아무 파일이나 열어 한 줄 추가하고 저장합니다.

```bash
git status
```

변경된 파일이 빨간색으로 표시됩니다. 아직 git에 기록되지 않은 상태입니다.

---

**3. 스테이징 (기록할 파일 고르기)**

```bash
git add 파일이름
```

또는 변경된 파일 전체를 한 번에 올리려면:

```bash
git add .
```

```bash
git status
```

다시 확인하면 파일이 초록색으로 바뀝니다. "기록 준비 완료"라는 뜻입니다.

---

**4. commit (스냅샷 찍기)**

```bash
git commit -m "내가 무엇을 바꿨는지 한 줄로 적기"
```

메시지는 나중에 봤을 때 무슨 작업인지 알 수 있게 씁니다.

```
좋은 예: "add user name to greeting message"
나쁜 예: "수정", "fix", "asdf"
```

---

**5. push (원격 저장소에 올리기)**

```bash
git push -u origin my-first-branch
```

처음 push할 때는 `-u origin 브랜치이름`을 붙입니다. 이후부터는 `git push`만 해도 됩니다.

---

**6. PR 열기**

Bitbucket에서 레포를 열고 왼쪽 메뉴의 **Pull requests → Create pull request** 를 클릭합니다.

1. **Source** — 내 브랜치 선택
2. **Destination** — `main` 선택
3. 제목 확인 후 **Create pull request** 클릭

> push 직후 Bitbucket 화면 상단에 "Create a pull request" 안내 배너가 뜨기도 합니다. 그 버튼을 눌러도 됩니다.

---

**7. merge**

PR 페이지에서 **Merge** 버튼을 클릭합니다. Merge strategy는 기본값(Merge commit)으로 두면 됩니다.

merge가 끝나면 브랜치를 삭제할지 묻습니다. **Delete branch**를 선택해도 됩니다.

---

**8. 로컬을 최신 상태로 맞추기**

merge 후에는 로컬 main도 당겨와야 합니다.

```bash
git checkout main
git pull
```

---

## 흔한 실수

**main에 직접 commit·push하기**

습관이 안 잡혔을 때 자주 합니다. main에 올라간 내용은 되돌리기 번거롭습니다. 항상 브랜치를 먼저 만들고 시작하는 습관을 들이세요.

```bash
git branch   # 지금 어느 브랜치인지 항상 확인
```

---

**commit 메시지를 "수정"으로만 쓰기**

일주일 뒤에 `git log`를 보면 "수정"이 열 개 나옵니다. 무엇을 바꿨는지 알 수 없습니다. 한 줄이라도 구체적으로 씁니다.

---

**push 없이 PR을 만들려 할 때**

Bitbucket에서 내 브랜치가 안 보인다면 push를 안 한 것입니다. 로컬 commit은 내 컴퓨터에만 있습니다. push해야 Bitbucket에 올라갑니다.

```bash
git push -u origin 브랜치이름
```

---

**git이 꼬였을 때**

[07 · 막혔을 때](07-troubleshooting.md) 또는 [git 치트시트](cheatsheets/git.md)를 확인하세요.
