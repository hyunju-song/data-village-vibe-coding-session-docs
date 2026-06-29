# ⚙️ setup-plugin — 하네스 적용을 위한 플러그인 설치 (전원 · 세션 전)

> `[사전 준비]` 이 페이지는 **모든 수강생이 세션 전에 한 번** 끝내야 합니다.
> 하네스가 "무엇이고 왜 쓰는지"는 → [06 · 하네스: 왜 & 어떻게](#/06-harness). 여기서는 **하네스를 적용하기 위한 플러그인 설치 방법**만 다룹니다.

---

## 이게 뭐예요?

회사 표준 하네스는 **Claude Code 플러그인**으로 제공됩니다. 한 번 설치하면 Claude Code가 회사 표준 규칙·권한·자동 검증(훅)을 갖춘 상태가 됩니다. 우리는 사내 마켓플레이스에서 이 플러그인을 받아 씁니다.

- **마켓플레이스**: [`gsr-agent-marketplace`](https://code.gsretail.com/scm/d-vill/gsr-agent-marketplace.git)
- **플러그인**: `fe-agent-harness` (프론트엔드 — **오전 실습은 이것**) · `be-agent-harness` (백엔드 — 이후 세션)

> 오전·오후 모두 **같은 마켓플레이스에서 같은 플러그인**을 설치합니다. 그래서 아침에 한 경험이 오후에 그대로 재현됩니다.

---

## 시작 전 확인

> 🔑 **Bitbucket 인증 필수** — 플러그인 설치는 사내 git 저장소에서 파일을 받아오므로, 로컬에서 Bitbucket에 접근할 수 있어야 합니다.  
> HTTP 토큰 또는 SSH 키 설정이 안 되어 있다면 먼저 끝내세요 → [Bitbucket 인증 가이드](https://app.notion.com/p/bitbucket-server-360f536db3d580e9ad0dc5cf9baa1496)

- [ ] 회사망 접속 (필요 시 VPN) — `code.gsretail.com`에 접근 가능해야 합니다.
- [ ] 사내 git 로그인/자격증명 설정 — 로그인되어 있어야 설치가 됩니다.
- [ ] (Windows 사용자) [setup-windows](#/setup-windows)를 먼저 끝냈는가 — 같은 셸에서 진행합니다.
- [ ] **터미널** Claude Code에서 진행 — `/plugin` 명령은 터미널에서 동작합니다.

---

## 설치 (3단계)

터미널에서 `claude`를 실행한 뒤, Claude Code 안에서 아래를 차례로 입력하세요.

**1) 마켓플레이스 등록**

```
/plugin marketplace add https://code.gsretail.com/scm/d-vill/gsr-agent-marketplace.git
```

**2) 등록 확인 + 마켓플레이스 이름 확인**

```
/plugin
```

열린 화면의 *Marketplaces* 탭에서 방금 추가한 마켓플레이스가 보이는지 확인합니다.

> 다음 단계에서 `@` 뒤에 붙는 이름은 이 마켓플레이스의 **등록 이름**입니다(레포 이름과 다를 수 있어요). 여기서 정확한 이름을 확인하세요.

**3) 플러그인 설치 (오전 실습 = 프론트엔드)**

```
/plugin install fe-agent-harness@agent-harness-store
```

설치 후 반영:

```
/reload-plugins
```

(또는 Claude Code를 재시작)

> 백엔드 세션 때는 `be-agent-harness@agent-harness-store`도 같은 방식으로 설치합니다. **오전엔 필요 없습니다.**

---

## ✅ 완료 조건

`/plugin`의 *Installed* 탭에 **`fe-agent-harness`가 보이면** 끝입니다. 다음 단계(오전 실습)로 넘어가세요.

---

## 안 될 때

| 증상 | 확인 |
| --- | --- |
| `/plugin`이 "unknown command" | `claude --version`으로 버전 확인 → 업데이트 후 재시작 |
| 마켓플레이스가 안 불러와짐 | URL을 브라우저로 열어 접근되는지(회사망/VPN) 확인 |
| 설치 실패 / 권한 오류 | 사내 git 로그인·자격증명 확인 (안 풀리면 IT 문의) |
| 명령은 됐는데 플러그인이 안 보임 | `/reload-plugins` 또는 Claude Code 재시작 |

> 그래도 막히면 → [07 · 막혔을 때](#/07-troubleshooting) 또는 운영진/IT.

---

> 🛠 **강사용 메모 (게시 전 삭제)**
> - 사내망/자격증명 전제(VPN·BITBUCKET_TOKEN 필요 여부)는 환경에 맞게 한 줄 보정.
> - `_sidebar.md`와 인덱스의 "사전 준비" 콜아웃에 이 페이지를 `setup-windows`와 함께 링크.