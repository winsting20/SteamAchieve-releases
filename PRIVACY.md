# SteamAchieve 개인정보 안내 · Privacy Notice

버전 1.3 · 2026-09-16 · 앱 버전 0.5.17 기준

## 한국어

### 한 줄 요약
SteamAchieve 는 서버가 없는 완전 로컬 도구입니다. 사용자의 데이터는 사용자의 PC 를 벗어나지 않으며, 개발자는 어떤 데이터도 받지 않습니다.

### 앱이 다루는 데이터
| 데이터 | 어디서 오는가 | 어디에 저장되는가 | 밖으로 나가는가 |
|---|---|---|---|
| Steam Web API 키 | 사용자가 첫 실행 때 입력하거나, **앱 안 브라우저**가 발급 페이지에서 읽어 옴 | `%APPDATA%\SteamAchieve\credentials.dat` (Windows DPAPI 로 암호화, 이 Windows 계정에서만 복호화) | **Steam API 호출의 인증 파라미터로만** 전송. 그 외 어디로도 안 감 |
| 스팀 계정 비밀번호 · 스팀 로그인 세션 | 사용자가 **앱 안에 뜨는 스팀 로그인 창**(Microsoft Edge WebView2)에 직접 입력 | **저장하지 않습니다.** 그 창의 세션 데이터(쿠키 등)는 임시 폴더에 1회용으로만 두고 창이 닫히면 폴더째 삭제합니다 | 사용자가 친 비밀번호는 **스팀 서버로만** 갑니다. 앱은 그 입력을 읽지 않고(자바스크립트로 읽는 것은 주소가 `/dev/apikey` 일 때의 키 문자열뿐입니다) 개발자에게도 가지 않습니다 |
| SteamID64 | 사용자가 입력(프로필 주소·맞춤 이름은 Steam 이 숫자로 변환) | `state.json` | Steam API 호출 파라미터로만 |
| 보유 게임·플레이타임·업적·전역 달성률·게임 태그·가격 | Steam Web API / Steam 스토어 API | `cache\` 폴더 | 안 감 |
| 업적·게임 아이콘, 커버 이미지 | Steam CDN | `cache\icons\` | 안 감 |
| 친구 목록·친구의 보유 게임·친구의 업적 (옵트인) | Steam Web API — **친구가 공개한 것만** | `cache\friends\` (7일) | 안 감 |
| 수동 추가 친구, 친구 별명 | 사용자가 입력 | `friends_manual.json` | 안 감 |
| 친구 활동 기록 — 친구가 업적을 **딴 시각**, 친구의 최근 2주 플레이 (옵트인) | Steam Web API — **친구가 공개한 것만** | `friend_activity.json` (친구당 최근 90일·2,000개까지, 친구를 목록에서 지우면 그 친구 몫도 함께 지워짐) | 안 감 |
| 업적 메모·북마크, 월간 목표, 화면 설정 | 사용자가 입력 | `notes.json`, `state.json` | 안 감 |
| 업적 내 진행도("8,988 / 10,000") | 내 **공개 프로필 업적 페이지**(Web API 에 없는 값) | `cache\progress\` (1시간) | 안 감 |
| 오류 기록 | 앱 내부 예외 | `last_error.txt`, `session_log.txt` (SteamID 는 가려서 기록) | 안 감 — 사용자가 문제 보고 때 직접 첨부할 때만 |

### 앱이 접속하는 곳 (전체 목록)
아래 외에는 어떤 주소에도 접속하지 않습니다. 방화벽·프록시로 확인할 수 있습니다.

| 호스트 | 용도 | 언제 |
|---|---|---|
| `api.steampowered.com` | Steam Web API (보유 게임·업적·스키마·전역 달성률·프로필 요약·친구 목록·친구의 최근 2주 플레이·스토어 목록) | 항상(계정 연결 후) |
| `store.steampowered.com` | 스토어 API (추천 후보의 가격·태그·설명) | 추천 탭을 연 뒤 |
| `steamcommunity.com` | 맞춤 URL 해석, **업적 내 진행도를 읽을 내 공개 업적 페이지**(게임을 열 때 1회), 브라우저로 여는 링크(가이드·통계·프로필 설정), **앱 안 브라우저로 여는 스팀 로그인·키 발급 페이지** | 첫 실행 · 게임을 열 때 · 사용자가 링크를 눌렀을 때 · [앱 안에서 키 받아오기]를 눌렀을 때 |
| `cdn.cloudflare.steamstatic.com`, `cdn.akamai.steamstatic.com`, `shared.cloudflare.steamstatic.com`, `steamcdn-a.akamaihd.net` | 업적 아이콘·게임 아이콘·커버 이미지 (Steam API 응답이 주는 이미지 주소도 이 계열 호스트) | 화면에 보이는 이미지가 필요할 때 |
| `api.github.com` | **새 버전 확인 (옵트인, 기본 꺼짐)** — 릴리스 페이지에 인증 없는 GET 1회/일. 키·SteamID 는 어떤 형태로도 실리지 않음 | 설정에서 켠 경우만 |
| `github.com` | 릴리스 페이지·문제 보고 페이지를 **브라우저로** 열 때, 그리고 **업데이트 받기** — 새 버전의 `SteamAchieve.exe` 와 해시 파일(`SHA256SUMS.txt`)을 인증 없이 GET. 키·SteamID 는 어떤 형태로도 실리지 않음 | 사용자가 버튼을 눌렀을 때 · 업데이트 창에서 [업데이트]를 눌렀을 때만 |
| `release-assets.githubusercontent.com`, `objects.githubusercontent.com` | **업데이트 받기** — GitHub 가 위 파일 다운로드를 이 주소로 넘겨 줌(파일 저장소). 앱은 이 두 호스트 외의 넘김 주소는 거부 | 업데이트 창에서 [업데이트]를 눌렀을 때만 |
| `isthereanydeal.com`, `www.fanatical.com`, `www.greenmangaming.com`, `www.humblebundle.com` | "최저가 보기" — 설정에서 고른 사이트의 게임 페이지를 **브라우저로** 열 때(앱 자체는 접속하지 않으며 가격 데이터도 받지 않음). 주소에는 스팀 게임 번호 또는 게임 이름만 실림. 제휴 링크 아님 | 사용자가 메뉴·버튼을 눌렀을 때 |

### 앱 안 브라우저 (키 발급 전용)
[앱 안에서 키 받아오기]를 누르면 Windows 의 Microsoft Edge WebView2 로 **스팀 로그인 페이지**를 앱 창 안에 띄웁니다. 복사·붙여넣기 단계를 없애기 위한 것이며, 아래를 지킵니다.

- **별도 프로세스에서 뜹니다.** 그 창은 스팀이 보낸 페이지를 그대로 보여줄 뿐이고, 앱은 그 안에서 **주소가 `steamcommunity.com/dev/apikey` 일 때만** 본문에서 16진수 32자(키)를 찾습니다. 로그인 화면의 입력값은 읽지 않습니다.
- **비밀번호는 저장하지 않습니다.** 스팀 서버로만 갑니다.
- **세션은 1회용입니다.** WebView2 사용자 데이터 폴더를 임시 폴더 안에 두고 창이 닫히면 지웁니다 — 다음에 다시 누르면 처음부터 로그인해야 합니다.
- 그 창은 일반 브라우저와 같아서, 스팀 로그인 페이지가 요구하는 스팀 도메인과 그 CDN(위 표의 호스트들)에 접속합니다.
- 도메인 칸은 `localhost` 로 채워 두지만 **[등록] 버튼은 누르지 않습니다** — 약관 동의가 걸린 행위라 사람이 누릅니다.
- WebView2 가 없는 PC 에서는 이 창이 뜨지 않고, 예전처럼 기본 브라우저가 열립니다(그때는 키를 복사하면 앱이 자동으로 받아 채웁니다).

### 수집하지 않는 것
- 사용 통계, 클릭 로그, 광고 식별자, 크래시 자동 전송 — 코드에 그런 경로 자체가 없습니다.
- 다른 사람의 비공개 데이터 — Steam 이 403 으로 거부하면 "미확인"으로 두고 우회하지 않습니다.
- 스팀 계정 비밀번호 — 앱은 입력칸을 만들지도, 읽지도, 저장하지도 않습니다.

### 옵트인 기능
- **친구 비교**와 **새 버전 확인**은 기본 꺼짐이며 설정에서 켠 경우에만 해당 호출이 나갑니다. 끄면 즉시 멈춥니다.
- **업데이트 받기**는 새 버전 알림을 눌러 연 창에서 [업데이트]를 누를 때만 일어납니다. 받은 파일은 해시가 릴리스의 `SHA256SUMS.txt` 와 일치할 때만 기존 `SteamAchieve.exe` 를 바꾸고, 일치하지 않으면 지웁니다.

### 데이터 삭제
- 설정 › 저장 › "캐시 비우기" 로 캐시를, "로그아웃"으로 키를 지웁니다.
- 전부 지우려면 `%APPDATA%\SteamAchieve\` 폴더를 삭제하면 됩니다. 앱은 그 밖에 아무것도 남기지 않습니다(레지스트리는 읽기만 하고 쓰지 않습니다). 업데이트 중에만 exe 옆에 `SteamAchieve.exe.new`·`.old` 가 잠시 생기고, 다음 실행 때 지워집니다.

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
| Steam Web API key | You, at first run — or read off the key page by the **in-app browser** | `%APPDATA%\SteamAchieve\credentials.dat` (Windows DPAPI, decryptable only by this Windows account) | **Only as the auth parameter of Steam API calls.** Nowhere else |
| Steam password · Steam sign-in session | Typed by you into the **Steam sign-in window shown inside the app** (Microsoft Edge WebView2) | **Not stored.** That window's session data (cookies etc.) lives in a temporary folder for one use only and the whole folder is deleted when the window closes | The password you type goes **only to Steam**. The app never reads it (the only thing it reads with JavaScript is the key string, and only while the address is `/dev/apikey`), and it never reaches the developer |
| SteamID64 | You (profile URL / custom name resolved by Steam) | `state.json` | Only as a Steam API parameter |
| Owned games, playtime, achievements, global percentages, tags, prices | Steam Web API / Steam store API | `cache\` | No |
| Achievement/game icons, cover images | Steam CDN | `cache\icons\` | No |
| Friend list, friends' owned games and achievements (opt-in) | Steam Web API — **public data only** | `cache\friends\` (7 days) | No |
| Manually added friends, friend nicknames | You | `friends_manual.json` | No |
| Friend activity — **when** friends unlocked achievements, their last-2-weeks playtime (opt-in) | Steam Web API — **public data only** | `friend_activity.json` (up to 90 days / 2,000 entries per friend; removing a friend deletes their entries too) | No |
| Notes, bookmarks, monthly goal, UI settings | You | `notes.json`, `state.json` | No |
| In-achievement progress ("8,988 / 10,000") | Your **public profile achievement page** (not available in the Web API) | `cache\progress\` (1 hour) | No |
| Error logs | App exceptions | `last_error.txt`, `session_log.txt` (SteamID masked) | No — only if you attach them to a bug report yourself |

### Hosts the app connects to (complete list)
Nothing else. You can verify with a firewall or proxy.

| Host | Purpose | When |
|---|---|---|
| `api.steampowered.com` | Steam Web API | Always, after connecting |
| `store.steampowered.com` | Store API (prices, tags, descriptions for recommendations) | After opening the Discover tab |
| `steamcommunity.com` | Custom URL resolution; **your public achievement page** read once per game for in-achievement progress; links opened in your browser; **the Steam sign-in and key pages opened in the in-app browser** | First run; when you open a game; when you click a link; when you press [Get the key inside the app] |
| `cdn.cloudflare.steamstatic.com`, `cdn.akamai.steamstatic.com`, `shared.cloudflare.steamstatic.com`, `steamcdn-a.akamaihd.net` | Icons and cover images (image URLs returned by the Steam API point at these hosts) | When an image is shown |
| `api.github.com` | **Update check (opt-in, off by default)** — one unauthenticated GET per day to the releases page. The key and SteamID are never included | Only if enabled in Settings |
| `github.com` | Release page / issue page opened **in your browser**, and **downloading an update** — unauthenticated GET of the new `SteamAchieve.exe` and its hash file (`SHA256SUMS.txt`). The key and SteamID are never included | When you click the button · only when you press [Update] in the update window |
| `release-assets.githubusercontent.com`, `objects.githubusercontent.com` | **Downloading an update** — GitHub redirects the file download above to this file storage. The app refuses redirects to any other host | Only when you press [Update] in the update window |
| `isthereanydeal.com`, `www.fanatical.com`, `www.greenmangaming.com`, `www.humblebundle.com` | "See best price" — opens the game's page on the site you chose **in your browser** (the app itself does not connect and downloads no price data). The URL carries only the Steam app id or the game name. Not affiliate links | When you click the menu item or button |

### The in-app browser (key issuance only)
Pressing [Get the key inside the app] opens the **Steam sign-in page** inside the app window using Windows' Microsoft Edge WebView2. It exists to remove the copy-and-paste step, and it follows these rules.

- **It runs in a separate process.** The window just shows what Steam sends; the app looks for a 32-character hex string (the key) in the page text **only while the address is `steamcommunity.com/dev/apikey`**. It never reads what you type on the sign-in screen.
- **Your password is not stored.** It goes only to Steam.
- **The session is single-use.** The WebView2 user-data folder lives inside a temporary folder and is deleted when the window closes — next time you will have to sign in again.
- Like any browser, that window connects to the Steam domains and CDNs the sign-in page asks for (the hosts listed above).
- The domain box is pre-filled with `localhost`, but the app **never presses [Register]** — that step involves accepting terms, so a human presses it.
- On a PC without WebView2 the window does not open and your default browser is used instead (then copying the key is enough; the app picks it up automatically).

### What is not collected
- Usage statistics, click logs, advertising IDs, automatic crash upload — the code has no such path.
- Other people's private data — when Steam answers 403 the app shows "unknown" and does not try to work around it.
- Your Steam password — the app has no field for it, never reads it, and never stores it.

### Opt-in features
- **Friends comparison** and **update check** are off by default; their calls happen only when you enable them in Settings and stop immediately when disabled.
- **Downloading an update** happens only when you press [Update] in the window opened from the new-version notice. The downloaded file replaces `SteamAchieve.exe` only if its hash matches the release's `SHA256SUMS.txt`; otherwise it is deleted.

### Deleting your data
- Settings › Storage › "Clear cache" removes the cache; "Log out" removes the key.
- To remove everything, delete `%APPDATA%\SteamAchieve\`. The app leaves nothing else (it only reads the registry, never writes). Only during an update, `SteamAchieve.exe.new` / `.old` appear next to the exe for a moment and are removed on the next start.

### Local registry and the Steam client
- To show the currently running game the app **reads** a few keys under `HKCU\Software\Valve\Steam` (e.g. `RunningAppID`). It never writes or affects the Steam client.
- The "View in Steam" button only hands `steam://nav/games/details/<appid>` (owned) or `steam://store/<appid>` (not owned) to the OS shell. Nothing but the app id travels with it, and it adds no host the app connects to. **It does not launch or install the game.**

Contact: https://github.com/winsting20/SteamAchieve-releases/issues
