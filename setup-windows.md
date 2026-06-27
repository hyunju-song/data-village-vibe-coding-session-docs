# 🪟 Windows 사전 준비 (WSL 설치)

> **Mac 사용자는 이 페이지를 건너뛰세요.** 터미널이 이미 bash/zsh로 동작합니다.  
> **세션 전에 미리** 끝내세요. WSL 설치는 재부팅과 관리자 권한이 필요합니다.  
> IT/BIOS 정책으로 막히면 IT 팀에 먼저 문의하세요.

---

이 준비를 마치면 Mac 사용자와 **똑같은 bash 셸**에서 똑같은 명령어로 진행할 수 있습니다.

---

## 1단계 — WSL 설치

1. **시작 메뉴**에서 `PowerShell`을 검색합니다.
2. **"관리자 권한으로 실행"** 을 선택합니다.
3. 아래 명령어를 입력하고 Enter를 누릅니다.

```powershell
wsl --install
```

4. 설치가 끝나면 **재부팅**합니다.
5. 재부팅 후 Ubuntu 창이 자동으로 열립니다.

> 이미 WSL이 설치되어 있다면 이 단계를 건너뛰세요.

---

## 2단계 — Ubuntu 사용자 설정

Ubuntu 창에서 아래를 진행합니다.

1. **username** 입력 (영소문자, 공백 없이)
2. **password** 입력 (화면에 안 보이는 게 정상)
3. 동일 password 재입력

설정이 끝나면 이런 프롬프트가 보입니다.

```
username@DESKTOP:~$
```

여기가 bash 셸입니다. 이제 Mac 사용자와 같은 출발선입니다.

---

## 3단계 — git 동작 확인

```bash
git --version
```

`git version 2.x.x` 형태로 출력되면 완료입니다.

> 출력이 없거나 오류가 나면 아래를 실행하세요.
> ```bash
> sudo apt update && sudo apt install -y git
> ```

---

## 4단계 — AWS CLI 동작 확인

```bash
aws --version
```

`aws-cli/2.x.x` 형태로 출력되면 완료입니다.

> 설치되어 있지 않으면 아래를 실행하세요.
> ```bash
> curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
> unzip awscliv2.zip
> sudo ./aws/install
> ```

---

## 확인 완료 체크리스트

- [ ] `git --version` 출력됨
- [ ] `aws --version` 출력됨
- [ ] 프롬프트가 `username@DESKTOP:~$` 형태임

세 개 모두 확인했으면 준비 완료입니다. [01 · 터미널](01-terminal.md)로 넘어가세요.

---

> **Git Bash 대안** — WSL이 IT/BIOS 정책으로 막혔을 때만 사용합니다.  
> Git for Windows 설치 후 "Git Bash"를 열면 bash 셸을 쓸 수 있습니다.  
> 단, AWS CLI는 별도 설치가 필요합니다. IT 팀과 함께 진행하세요.
