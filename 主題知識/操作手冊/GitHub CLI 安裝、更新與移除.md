# GitHub CLI 安裝、更新與移除

版本：1.0 · 更新與查證日期：2026-10-15

| 我要做什麼 | 直接前往 |
| --- | --- |
| 安裝 | [Windows](#install-windows) · [macOS](#install-macos) · [登入確認](#login) |
| 更新 | [依原安裝方式更新](#update) |
| 移除／反安裝 | [登出](#logout) · [移除程式](#remove-program) · [選用：清除設定](#cleanup-config) |

GitHub CLI 的指令是 `gh`，用來操作 GitHub 的 repository、issue、pull request 等功能。Git 的指令是 `git`，負責版本控制，兩者可搭配使用。需要 Git 的安裝與管理步驟時，查閱 [Git CLI 手冊](<Git CLI 安裝、更新與移除.md>)。

本手冊涵蓋 Windows 10／11 與 macOS，以 GitHub.com 的瀏覽器登入流程為主。Windows 指令適用於 Windows PowerShell 5.1 與 PowerShell 7 以上。Linux、WSL、解壓縮版、原始碼編譯與其他套件管理器不在本篇範圍。**每個系統選一種安裝方式，更新與移除沿用原方式。**

<a id="requirements"></a>

## 0. 使用前確認

開啟 PowerShell／Terminal，執行：

```text
gh --version
```

顯示 `gh version ...` 表示已有可用的程式，先[確認來源](#check-source)，需要時再更新。使用 GitHub 帳號功能時還要[登入](#login)，顯示版本只代表程式能執行。

若要 clone、commit 或 push 專案，也先執行 `git --version` 確認 Git 可用。GitHub CLI 的安裝與 Git 的安裝分別管理。[來源：GitHub CLI 快速入門](https://docs.github.com/en/github-cli/github-cli/quickstart)

<a id="install"></a>

## 1. 安裝

<a id="install-windows"></a>

### Windows：WinGet

先在 PowerShell 執行 `winget --version`，確認可用，再執行：

```powershell
winget install --id GitHub.cli -e --source winget
```

依提示完成安裝，需要時授予管理員權限。完成後關閉原終端機，**另開新的 PowerShell／Windows Terminal 視窗**，執行 `gh --version`。只開新分頁可能仍沿用舊 PATH。

沒有 WinGet 時，可依 [Microsoft 官方說明](https://learn.microsoft.com/en-us/windows/package-manager/winget/)取得 App Installer，或改用下方 MSI 路線。[來源：GitHub CLI Windows 安裝文件](https://github.com/cli/cli/blob/trunk/docs/install_windows.md)

### Windows 選用：官方 MSI 安裝程式

1. 開啟 [GitHub CLI 最新正式版發布頁](https://github.com/cli/cli/releases/latest)，展開 **Assets**。
2. 一般 Intel／AMD 64 位元電腦選檔名結尾為 `_windows_amd64.msi` 的檔案，Windows ARM 電腦選 `_windows_arm64.msi`。可到 **設定 > 系統 > 關於 > 系統類型** 確認架構。
3. 執行 MSI，依視窗指示完成安裝。
4. 另開新的 PowerShell 視窗，執行 `gh --version`，再前往[登入確認](#login)。

此路線與 WinGet 安裝的是同一項工具，不需要兩種都裝。官方亦提供其他架構與解壓縮檔，選 MSI 才適用本篇的 Windows 解除安裝流程。[來源：Windows 安裝文件](https://github.com/cli/cli/blob/trunk/docs/install_windows.md)

<a id="install-macos"></a>

### macOS：Homebrew

先執行 `brew --version`。尚未安裝 Homebrew 時，依 [Homebrew 官方安裝說明](https://docs.brew.sh/Installation)確認系統相容性並安裝，完成安裝器顯示的 **Next steps** 後另開 Terminal。

```bash
brew install gh
```

這裡的 `gh` 是 formula，指令不加 `--cask`。完成後另開 Terminal，執行 `gh --version`，再前往[登入確認](#login)。[來源：GitHub CLI macOS 安裝文件](https://github.com/cli/cli/blob/trunk/docs/install_macos.md)、[Homebrew gh 套件](https://formulae.brew.sh/formula/gh)

<a id="login"></a>

### 登入與基本確認

Windows 與 macOS 寫法相同。先執行：

```text
gh auth login --hostname github.com --git-protocol https --web
```

1. 依終端機提示複製一次性驗證碼，按提示開啟瀏覽器。
2. 確認登入的是預期的 GitHub 帳號，輸入驗證碼並完成授權。
3. 若詢問是否讓 Git 使用 GitHub 憑證，需要共用 HTTPS 登入時選 **Yes**，已有自己的 Git 驗證設定時可選 **No**。
4. 完成後回到終端機確認：

   ```text
   gh auth status --hostname github.com
   ```

顯示預期帳號與正常驗證狀態，即完成登入確認。程式能顯示版本且登入正常，才算完成本篇的基本設定，這不代表已驗證每個私有專案或組織的權限。

GitHub CLI 會優先將登入憑證存入系統憑證儲存區，無法使用時可能改存明文設定檔。可從 `gh auth status` 確認儲存來源，設定檔不要直接分享。公司使用自有 GitHub 網域時，將指令中的 `github.com` 換成公司提供的主機名稱，並依公司授權流程處理。

來源：[gh auth login](https://cli.github.com/manual/gh_auth_login)、[gh auth status](https://cli.github.com/manual/gh_auth_status)、[GitHub CLI 快速入門](https://docs.github.com/en/github-cli/github-cli/quickstart)。

<a id="update"></a>

## 2. 更新

先結束正在執行 `gh` 的任務。另開 PowerShell／Terminal，**依原安裝方式擇一**：

| 原安裝方式 | 更新方法 |
| --- | --- |
| Windows，WinGet | `winget upgrade --id GitHub.cli -e --source winget` |
| Windows，官方 MSI | 從[最新正式版發布頁](https://github.com/cli/cli/releases/latest)取得相同架構的新版 MSI，執行並依提示完成更新。 |
| macOS，Homebrew | 先執行 `brew update`，再執行 `brew upgrade gh`。 |

`gh` 的更新提示只通知有新版，實際更新仍用上表方式。`gh extension upgrade` 更新的是擴充套件，GitHub CLI 本體另行更新。

完成後另開終端機，執行 `gh --version`、[確認來源](#check-source)，再執行 `gh auth status --hostname github.com`。更新無錯誤、來源正確且登入正常，即完成基本確認。原本已是該管道最新版時，版本號可以不變，套件管道也可能晚於官方發布。

來源：[Windows 安裝與更新](https://github.com/cli/cli/blob/trunk/docs/install_windows.md)、[macOS 安裝與更新](https://github.com/cli/cli/blob/trunk/docs/install_macos.md)、[WinGet upgrade](https://learn.microsoft.com/en-us/windows/package-manager/winget/upgrade)、[Homebrew 指令](https://docs.brew.sh/Manpage)、[gh 環境變數與更新通知](https://cli.github.com/manual/gh_help_environment)。

<a id="uninstall"></a>

## 3. 移除／反安裝

移除程式時保留本機專案、`.git` 及 `.ssh`。以下步驟不會刪除 GitHub 上的 repository、issue 或 pull request，也不會取消訂閱。

若曾讓 Git 使用 GitHub CLI 提供 HTTPS 憑證，登出或移除 `gh` 後，Git 的遠端驗證可能受影響。仍要使用 Git 時，先安排其他適用的憑證管理方式或 SSH。這是依 [gh auth setup-git 的憑證輔助程式行為](https://cli.github.com/manual/gh_auth_setup-git)整理的操作提醒。

<a id="logout"></a>

### 選用：先登出這台電腦

若希望移除本機登入資料，在反安裝前執行：

```text
gh auth logout --hostname github.com
```

依提示選擇要登出的帳號，多帳號時逐一處理。再執行 `gh auth status --hostname github.com` 確認預期帳號已移除，沒有任何登入帳號時，狀態指令會回報未登入。

`gh auth logout` 只移除本機儲存的驗證，不會撤銷伺服器上的 token。若使用 `GH_TOKEN`、`GITHUB_TOKEN` 等環境變數，需另到原設定位置處理，它們優先於儲存的憑證，不會隨程式移除而自動消失。

**需要撤銷 GitHub CLI 授權時才做：** 到 GitHub 的 **Settings > Applications > Authorized OAuth Apps**，找到 **GitHub CLI** 並選 **Revoke**／**Revoke Access**。此操作會影響該帳號在其他裝置上的 GitHub CLI 授權。自行建立的 personal access token 則在其 token 設定頁另行撤銷。

來源：[gh auth logout](https://cli.github.com/manual/gh_auth_logout)、[環境變數](https://cli.github.com/manual/gh_help_environment)、[檢查與撤銷 OAuth App 授權](https://docs.github.com/en/apps/oauth-apps/using-oauth-apps/reviewing-your-authorized-oauth-apps)。

<a id="remove-program"></a>

### 依原安裝方式移除程式

| 原安裝方式 | 移除方法 |
| --- | --- |
| Windows，WinGet | `winget uninstall --id GitHub.cli -e --source winget` |
| Windows，官方 MSI | **開始 > 設定 > 應用程式 > 已安裝的應用程式**，找到 **GitHub CLI**，選 **⋯ > 解除安裝**。Windows 10 的入口為「應用程式與功能」。 |
| macOS，Homebrew | `brew uninstall gh` |

WinGet 無法辨識套件時，改用 Windows 設定的解除安裝入口。Homebrew 若提示其他套件依賴 `gh`，先處理依賴關係，不強制略過。

完成後另開終端機執行 `gh --version`，應顯示找不到命令。Windows 可再確認應用程式清單已無該項目，Homebrew 可用 `brew list --versions gh` 確認不再列出版本。若仍能執行，依[來源辨識](#check-source)查出另一份安裝，再用其原方式處理。

來源：[WinGet uninstall](https://learn.microsoft.com/en-us/windows/package-manager/winget/uninstall)、[Windows 移除程式](https://support.microsoft.com/en-us/windows/uninstall-or-remove-apps-and-programs-in-windows-4b55f974-2cc6-2d2b-d092-5905080eaf98)、[Homebrew 指令](https://docs.brew.sh/Manpage)。

<a id="cleanup-config"></a>

### 選用：清除本機設定

一般反安裝可保留設定，重新安裝後繼續使用。確定不再需要且已處理登入憑證時，再用檔案總管／Finder 移除 **GitHub CLI 專用**設定目錄：

| 系統 | 預設位置 |
| --- | --- |
| Windows | `%APPDATA%\GitHub CLI` |
| macOS | `~/.config/gh` |

若有設定 `GH_CONFIG_DIR`，以該目錄為準。未設定時，`XDG_CONFIG_HOME` 存在會優先使用其下的 `gh` 目錄。不要刪除整個 `.config` 或其他工具的資料夾。設定目錄可能含登入資料，清除後也無法取代伺服器端的撤銷授權。[來源：GitHub CLI 設定目錄規則](https://cli.github.com/manual/gh_help_environment)

<a id="help"></a>

## 4. 卡住時才看

<a id="check-source"></a>

### 確認目前執行哪一份 GitHub CLI

**Windows：PowerShell**

```powershell
Get-Command gh -All | Select-Object CommandType, Source, Definition
where.exe gh
```

已使用 WinGet 時，再執行 `winget list --id GitHub.cli -e`，確認是否辨識到已安裝套件。WinGet 也可能辨識原本以 MSI 安裝的程式，這不等於有兩份安裝。

**macOS：Terminal**

```bash
type -a gh
command -v gh
```

使用 Homebrew 時，再執行 `brew list --versions gh` 確認管理的版本。PATH 排在前面的程式通常會先被執行，也要留意 alias 或 function。

| 問題 | 先做這件事 |
| --- | --- |
| Windows 安裝完成仍找不到 `gh` | 完全結束終端機並另開新視窗，編輯器內的終端機要連編輯器一起重開。仍失敗時，查安裝來源或重新執行原 MSI。 |
| macOS 找不到 `brew` 或 `gh` | 依 [Homebrew 安裝說明](https://docs.brew.sh/Installation)完成 Next steps 的 PATH 設定，另開 Terminal 再確認。 |
| 版本沒變或更新工具說找不到套件 | 先查來源，確認是否已是該管道最新版，或執行到另一份安裝。不要直接改用另一個管理器再裝一份。 |
| 登入失敗、過期或帳號不對 | 先執行 `gh auth status --hostname github.com` 確認帳號與驗證來源，需要時重新執行上方登入指令。 |
| 顯示正在使用環境變數 token，瀏覽器登入無法取代 | 檢查自己設定的 `GH_TOKEN`、`GITHUB_TOKEN`，回原設定位置調整。不要把 token 值貼進文件或公開求助訊息。 |
| 已登入，但私有專案或組織仍無法存取 | 確認帳號權限、組織 SSO 與公司的授權要求。安裝成功不等於具有該資源的存取權。 |
| `git` 可用但沒有 `gh`，或反過來 | 兩項工具分別安裝與更新，Git 的設定不會自動完成 GitHub CLI 登入。 |

需要查指令用法時，執行 `gh --help` 或 `gh auth login --help`。分享登入排錯輸出前先遮蔽帳號等私人資訊，不加 `--show-token`。

<a id="sources"></a>

## 5. 官方來源與驗證範圍

| 來源 | 查證內容 |
| --- | --- |
| [GitHub CLI 官方專案](https://github.com/cli/cli)、[Windows 安裝文件](https://github.com/cli/cli/blob/trunk/docs/install_windows.md)、[macOS 安裝文件](https://github.com/cli/cli/blob/trunk/docs/install_macos.md) | 工具用途、官方安裝管道、架構、更新與 PATH 提示。 |
| [GitHub CLI releases](https://github.com/cli/cli/releases/latest) | 正式版安裝檔下載入口。 |
| [GitHub CLI quickstart](https://docs.github.com/en/github-cli/github-cli/quickstart) | 初次登入與 Git HTTPS 憑證共用。 |
| [gh auth login](https://cli.github.com/manual/gh_auth_login)、[status](https://cli.github.com/manual/gh_auth_status)、[logout](https://cli.github.com/manual/gh_auth_logout)、[setup-git](https://cli.github.com/manual/gh_auth_setup-git) | 登入、狀態、登出範圍與 Git 憑證輔助程式。 |
| [gh environment](https://cli.github.com/manual/gh_help_environment) | token 優先順序、設定目錄及更新通知。 |
| [Reviewing your authorized OAuth apps](https://docs.github.com/en/apps/oauth-apps/using-oauth-apps/reviewing-your-authorized-oauth-apps) | 檢查與撤銷 OAuth App 授權。 |
| [WinGet：install](https://learn.microsoft.com/en-us/windows/package-manager/winget/install)、[upgrade](https://learn.microsoft.com/en-us/windows/package-manager/winget/upgrade)、[uninstall](https://learn.microsoft.com/en-us/windows/package-manager/winget/uninstall) | 套件精確比對、安裝、更新與移除。 |
| [Windows 移除應用程式](https://support.microsoft.com/en-us/windows/uninstall-or-remove-apps-and-programs-in-windows-4b55f974-2cc6-2d2b-d092-5905080eaf98) | Windows 解除安裝入口。 |
| [Homebrew Installation](https://docs.brew.sh/Installation)、[gh formula](https://formulae.brew.sh/formula/gh)、[brew Manpage](https://docs.brew.sh/Manpage) | Homebrew 前提、套件與更新／移除指令。 |

本次依官方資料查證，並在本機 Windows 執行 `gh --version` 與登入、狀態、登出指令的 `--help`，確認基本語法。未實際安裝、更新、移除、登入、登出或撤銷授權，也未測試 macOS 操作。保留資料與 PATH 排錯的建議為操作整理，實際版本與相容性以各管道當時提供的資訊為準。

[返回操作手冊索引](README.md) · [返回 KnowledgeHub](../../README.md)
