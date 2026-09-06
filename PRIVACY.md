# SteamAchieve 개인정보 안내 · Privacy Notice

버전 1.1 · 2026-09-07 · 앱 버전 0.5.6 기준

## 한국어

### 한 줄 요약
SteamAchieve 는 서버가 없는 완전 로컬 도구입니다. 사용자의 데이터는 사용자의 PC 를 벗어나지 않으며, 개발자는 어떤 데이터도 받지 않습니다.

### 앱이 다루는 데이터
| 데이터 | 어디서 오는가 | 어디에 저장되는가 | 밖으로 나가는가 |
|---|---|---|---|
| Steam Web API 키 | 사용자가 첫 실행 때 입력 | `%APPDATA%\SteamAchieve\credentials.dat` (Windows DPAPI 로 암호화, 이 Windows 계정에서만 복호화) | **Steam API 호출의 인증 파라미터로만** 전송. 그 외 어디로도 안 감 |
| SteamID64 | 사용자가 입력(프로필 주소·맞춤 이름은 Steam 이 숫자로 변환) | `state.json` | Steam API 호출 파라미터로만 |
| 보유 게임·플레이타임·업적·전역 달성률·게임 태그·가격 | Steam Web API / Steam 스토어 API | `cache\` 폴더 | 안 감 |
| 업적·게임 아이콘, 커버 이미지 | Steam CDN | `cache\icons\` | 안 감 |
| 친구 목록·친구의 보유 게임·친구의 업적 (옵트인) | Steam Web API — **친구가 공개한 것만** | `cache\friends\` (7일) | 안 감 |
| 수동 추가 친구, 친구 별명 | 사용자가 입력 | `friends_manual.json` | 안 감 |
| 업적 메모·북마크, 월간 목표, 화면 설정 | 사용자가 입력 | `notes.json`, `state.json` | 안 감 |
| 업적 내 진행도("8,988 / 10,000") | 내 **공개 프로필 업적 페이지**(Web API 에 없는 값) | `cache\progress\` (1시간) | 안 감 |
| 오류 기록 | 앱 내부 예외 | `last_error.txt`, `session_log.txt` (SteamID 는 가려서 기록) | 안 감 — 사용자가 문제 보고 때 직접 첨부할 때만 |

### 앱이 접속하는 곳 (전체 목록)
아래 외에는 어떤 주소에도 접속하지 않습니다. 방화벽·프록시로 확인할 수 있습니다.

| 호스트 | 용도 | 언제 |
|---|---|---|
| `api.steampowered.com` | Steam Web API (보유 게임·업적·스키마·전역 달성률·프로필 요약·친구 목록·스토어 목록) | 항상(계정 연결 후) |
| `store.steampowered.com` | 스토어 API (추천 후보의 가격·태그·설명) | 추천 탭을 연 뒤 |
| `steamcommunity.com` | 맞춤 URL 해석, **업적 내 진행도를 읽을 내 공개 업적 페이지**(게임을 열 때 1회), 브라우저로 여는 링크(가이드·통계·프로필 설정) | 첫 실행 · 게임을 열 때 · 사용자가 링크를 눌렀을 때 |
| `cdn.cloudflare.steamstatic.com`, `cdn.akamai.steamstatic.com`, `shared.cloudflare.steamstatic.com`, `steamcdn-a.akamaihd.net` | 업적 아이콘·게임 아이콘·커버 이미지 (Steam API 응답이 주는 이미지 주소도 이 계열 호스트) | 화면에 보이는 이미지가 필요할 때 |
| `api.github.com` | **새 버전 확인 (옵트인, 기본 꺼짐)** — 릴리스 페이지에 인증 없는 GET 1회/일. 키·SteamID 는 어떤 형태로도 실리지 않음 | 설정에서 켠 경우만 |
| `github.com` | 릴리스 페이지·문제 보고 페이지를 **브라우저로** 열 때(앱 자체는 접속하지 않음) | 사용자가 버튼을 눌렀을 때 |

### 수집하지 않는 것
- 사용 통계, 클릭 로그, 광고 식별자, 크래시 자동 전송 — 코드에 그런 경로 자체가 없습니다.
- 다른 사람의 비공개 데이터 — Steam 이 403 으로 거부하면 "미확인"으로 두고 우회하지 않습니다.

### 옵트인 기능
- **친구 비교**와 **새 버전 확인**은 기본 꺼짐이며 설정에서 켠 경우에만 해당 호출이 나갑니다. 끄면 즉시 멈춥니다.

### 데이터 삭제
- 설정 › 저장 › "캐시 비우기" 로 캐시를, "로그아웃"으로 키를 지웁니다.
- 전부 지우려면 `%APPDATA%\SteamAchieve\` 폴더를 삭제하면 됩니다. 앱은 그 밖에 아무것도 남기지 않습니다(레지스트리는 읽기만 하고 쓰지 않습니다).

### 로컬 레지스트리 · 스팀 클라이언트
- 현재 실행 중인 게임을 표시하기 위해 `HKCU\Software\Valve\Steam` 의 `RunningAppID` 등 몇 개 키를 **읽기만** 합니다. 값을 쓰거나 Steam 클라이언트에 영향을 주지 않습니다.
- "스팀에서 보기" 버튼은 `steam://nav/games/details/<appid>`(보유) 또는 `steam://store/<appid>`(미보유) 주소를 **운영체제 셸에 넘길 뿐**입니다. 게임 번호 외에 아무것도 실리지 않고, 앱이 직접 접속하는 곳은 늘어나지 않습니다. **게임을 실행하거나 설치하지 않습니다.**

문의: https://github.com/winsting20/SteamAchieve-releases/issues

---

## English

### One line
SteamAchieve is a fully local tool with no server. Your data never leaves your PC, and the developer receives nothing.

### Data the app handles
| Data | Source | Stored at | Leaves your PC? |
|---|---|---|---|
| Steam Web API key | You, at first run | `%APPDATA%\SteamAchieve\credentials.dat` (Windows DPAPI, decryptable only by this Windows account) | **Only as the auth parameter of Steam API calls.** Nowhere else |
| SteamID64 | You (profile URL / custom name resolved by Steam) | `state.json` | Only as a Steam API parameter |
| Owned games, playtime, achievements, global percentages, tags, prices | Steam Web API / Steam store API | `cache\` | No |
| Achievement/game icons, cover images | Steam CDN | `cache\icons\` | No |
| Friend list, friends' owned games and achievements (opt-in) | Steam Web API — **public data only** | `cache\friends\` (7 days) | No |
| Manually added friends, friend nicknames | You | `friends_manual.json` | No |
| Notes, bookmarks, monthly goal, UI settings | You | `notes.json`, `state.json` | No |
| In-achievement progress ("8,988 / 10,000") | Your **public profile achievement page** (not available in the Web API) | `cache\progress\` (1 hour) | No |
| Error logs | App exceptions | `last_error.txt`, `session_log.txt` (SteamID masked) | No — only if you attach them to a bug report yourself |

### Hosts the app connects to (complete list)
Nothing else. You can verify with a firewall or proxy.

| Host | Purpose | When |
|---|---|---|
| `api.steampowered.com` | Steam Web API | Always, after connecting |
| `store.steampowered.com` | Store API (prices, tags, descriptions for recommendations) | After opening the Discover tab |
| `steamcommunity.com` | Custom URL resolution; **your public achievement page** read once per game for in-achievement progress; links opened in your browser | First run; when you open a game; when you click a link |
| `cdn.cloudflare.steamstatic.com`, `cdn.akamai.steamstatic.com`, `shared.cloudflare.steamstatic.com`, `steamcdn-a.akamaihd.net` | Icons and cover images (image URLs returned by the Steam API point at these hosts) | When an image is shown |
| `api.github.com` | **Update check (opt-in, off by default)** — one unauthenticated GET per day to the releases page. The key and SteamID are never included | Only if enabled in Settings |
| `github.com` | Release page / issue page opened **in your browser** (the app itself does not connect) | When you click the button |

### What is not collected
- Usage statistics, click logs, advertising IDs, automatic crash upload — the code has no such path.
- Other people's private data — when Steam answers 403 the app shows "unknown" and does not try to work around it.

### Opt-in features
- **Friends comparison** and **update check** are off by default; their calls happen only when you enable them in Settings and stop immediately when disabled.

### Deleting your data
- Settings › Storage › "Clear cache" removes the cache; "Log out" removes the key.
- To remove everything, delete `%APPDATA%\SteamAchieve\`. The app leaves nothing else (it only reads the registry, never writes).

### Local registry and the Steam client
- To show the currently running game the app **reads** a few keys under `HKCU\Software\Valve\Steam` (e.g. `RunningAppID`). It never writes or affects the Steam client.
- The "View in Steam" button only hands `steam://nav/games/details/<appid>` (owned) or `steam://store/<appid>` (not owned) to the OS shell. Nothing but the app id travels with it, and it adds no host the app connects to. **It does not launch or install the game.**

Contact: https://github.com/winsting20/SteamAchieve-releases/issues
