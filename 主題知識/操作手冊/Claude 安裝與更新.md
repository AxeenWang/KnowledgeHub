# Claude 安裝、更新與移除

版本：1.0 · 更新與查證日期：2026-10-15

| 我要做什麼 | 直接前往 |
| --- | --- |
| 安裝 | [桌面版](#desktop-install) · [Windows CLI](#cli-install-windows) · [macOS CLI](#cli-install-macos) |
| 更新 | [桌面版](#desktop-update) · [CLI](#cli-update) |
| 移除／反安裝 | [桌面版](#desktop-uninstall) · [CLI](#cli-uninstall) |

本手冊涵蓋兩種用法，選一條路線即可：

- **Claude 桌面版**：視窗操作，內含 Chat、Cowork、Code 三個分頁。只用 Code 分頁寫程式時，不需要另裝 CLI。
- **Claude Code CLI**：在 PowerShell／終端機輸入 `claude` 使用。**CLI 只選一種安裝方式**，官方建議獨立安裝版。

<a id="requirements"></a>

## 0. 使用前確認

| 項目 | 桌面版 | Claude Code CLI |
| --- | --- | --- |
| 作業系統 | Windows 10 以上、macOS 11 以上 | Windows 10 1809 以上、macOS 13.0 以上 |
| 硬體 | x64 或 ARM64 | 4 GB 以上記憶體，x64 或 ARM64 |
| 帳號 | Claude 帳號即可登入使用 Chat | 需 Pro、Max、Team、Enterprise 或 Console 帳號，免費方案不含 Claude Code |

桌面版的 Code 分頁同樣需要付費方案。

<a id="install"></a>

## 1. 安裝

<a id="desktop-install"></a>

### 桌面版

| 系統 | 操作步驟 |
| --- | --- |
| Windows | 開啟[官方下載頁](https://claude.com/download)，下載 Windows 安裝程式並執行，完成後從開始功能表開啟 **Claude**。ARM64 電腦改用 [ARM64 安裝程式](https://claude.ai/api/desktop/win32/arm64/setup/latest/redirect)。 |
| macOS | 開啟[官方下載頁](https://claude.com/download)，下載 macOS 版（Intel 與 Apple 晶片通用），開啟下載檔後依視窗指示拖至「應用程式」，再從「應用程式」開啟 **Claude**。 |

開啟後登入 Claude 帳號。能在 Chat 收到回覆，即完成基本確認。要寫程式時，點上方中間的 **Code** 分頁，選 **Local** 與 **Select folder** 指定專案資料夾。

<a id="cli-install-windows"></a>

### Windows CLI：PowerShell

開啟 PowerShell，執行以下指令。Windows PowerShell 5.1 與 PowerShell 7 以上寫法相同，不需以系統管理員身分執行。

```powershell
irm https://claude.ai/install.ps1 | iex
```

使用命令提示字元（CMD）時改用：

```bat
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

提示字元開頭有 `PS` 就是 PowerShell，沒有就是 CMD。安裝過程不顯示下載進度，等它結束即可。完成後另開新的 PowerShell 視窗，執行 `claude --version`。顯示版本後，前往[登入 CLI](#cli-login)。

建議另裝 [Git for Windows](https://git-scm.com/downloads/win)，安裝時選 **Add to PATH**。沒有它時 Claude Code 改用 PowerShell 執行指令，仍可使用。

<a id="cli-install-macos"></a>

### macOS CLI：終端機

開啟 Terminal／終端機，執行：

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

完成後另開新的終端機視窗，執行 `claude --version`。顯示版本後，前往[登入 CLI](#cli-login)。

<a id="cli-install-alternatives"></a>

### 選用：Homebrew、WinGet 或 npm

僅適用於原本已使用這些工具的人。已完成上方獨立安裝者可略過。這三種方式**不會自動更新**。

| 方式 | 安裝指令 |
| --- | --- |
| Homebrew，macOS | `brew install --cask claude-code` |
| WinGet，Windows | `winget install Anthropic.ClaudeCode` |
| npm，Windows／macOS | `npm install -g @anthropic-ai/claude-code`（需 Node.js 22 以上，不要加 `sudo`） |

Homebrew 的 `claude-code` 走穩定版通道，約落後最新版一週。想跟最新版改裝 `claude-code@latest`。

<a id="cli-login"></a>

### 登入 CLI

先切到要工作的資料夾，再啟動：

```text
claude
```

第一次啟動會引導至瀏覽器登入 Claude 帳號，完成後回到終端機即可開始使用。也可以先用 `claude auth login` 單獨登入，再以 `claude auth status --text` 確認登入狀態。macOS 切換資料夾時，可輸入 `cd` 加一個空白，將 Finder 的資料夾拖入終端機後按 Enter。在 Claude Code 內輸入 `/exit` 退出。

需要完整檢查時，執行 `claude doctor`，會列出安裝狀態、設定檔錯誤與建議修正，不會啟動工作階段。

<a id="update"></a>

## 2. 更新

先存檔並停止目前任務，CLI 使用者先輸入 `/exit` 退出。

<a id="desktop-update"></a>

### 桌面版

桌面版預設會在背景下載更新，並在適當時機自行重新啟動套用。要立即更新時：

| 系統 | 操作步驟 |
| --- | --- |
| Windows | 選單 **Help > Check for Updates**，完成後重新啟動。 |
| macOS | 選單列 **Claude > Check for Updates**，完成後重新啟動。 |

找不到入口或更新失敗時，從[官方下載頁](https://claude.com/download)重新下載安裝。公司管理的設備依 IT 更新流程處理，macOS 裝在系統「應用程式」資料夾時，更新可能需要管理員權限。重開後能登入並收到回覆，即完成更新。

<a id="cli-update"></a>

### CLI：依原安裝方式更新

| 原安裝方式 | 更新方法 |
| --- | --- |
| 官方獨立安裝版，Windows／macOS | 預設自動在背景更新，下次啟動生效。要立即更新時執行 `claude update`。 |
| Homebrew | `brew upgrade claude-code`，安裝的是最新版通道時改用 `brew upgrade claude-code@latest`。 |
| WinGet | `winget upgrade Anthropic.ClaudeCode`，執行前先結束 Claude Code。 |
| npm | `npm install -g @anthropic-ai/claude-code@latest`，不要用 `npm update -g`。 |

`claude update` 顯示 `Successfully updated from … to version …` 表示已更新，顯示 `Claude Code is up to date` 表示原本已是最新版。

更新完成後另開終端機，執行 `claude --version` 與 `claude auth status --text`。版本正確、登入狀態正常且能啟動，才算完成。原本已是最新版時，版本號可以不變。

<a id="uninstall"></a>

## 3. 移除／反安裝

先結束桌面版及 CLI。以下移除程式，不清除專案檔案、設定與對話紀錄，也不會取消訂閱。要連設定一起清除時，再看[選用：清除設定與紀錄](#cleanup-config)。

<a id="desktop-uninstall"></a>

### 桌面版

| 系統 | 移除方式 |
| --- | --- |
| Windows | **開始 > 設定 > 應用程式 > 已安裝的應用程式**，找到 **Claude**，選 **⋯ > 解除安裝**。 |
| macOS | 在 Finder 的「應用程式」找到 **Claude**，移至垃圾桶，確認後再清空。 |

<a id="cli-uninstall"></a>

### CLI：Homebrew、WinGet 或 npm

依原安裝方式擇一執行：

| 方式 | 移除指令 |
| --- | --- |
| Homebrew，macOS | `brew uninstall --cask claude-code`，最新版通道改用 `brew uninstall --cask claude-code@latest` |
| WinGet，Windows | `winget uninstall Anthropic.ClaudeCode` |
| npm，Windows／macOS | `npm uninstall -g @anthropic-ai/claude-code` |

### CLI：官方獨立安裝版

官方沒有一鍵反安裝指令，依官方文件刪除程式本體與版本檔即可。

**Windows：PowerShell**

```powershell
Remove-Item -Path "$env:USERPROFILE\.local\bin\claude.exe" -Force
Remove-Item -Path "$env:USERPROFILE\.local\share\claude" -Recurse -Force
```

**macOS：終端機**

```bash
rm -f ~/.local/bin/claude
rm -rf ~/.local/share/claude
```

只刪除 `claude` 這個檔案，不要刪除整個 `.local\bin`／`~/.local/bin`，其他工具（例如 macOS 的 Codex CLI）也可能放在這裡。PATH 中的 `.local\bin` 項目同理，確認沒有其他工具使用後再移除。

**移除後確認：** 另開終端機執行 `claude --version`。若仍能執行，可能還有另一份安裝，依下方方式查來源。

<a id="cleanup-config"></a>

### 選用：清除設定與紀錄

> [!WARNING]
> 會刪除所有設定、允許的工具、MCP 伺服器設定與工作階段紀錄，無法復原。

桌面版、VS Code 擴充套件與 JetBrains 外掛也會寫入 `~/.claude/`。若它們仍安裝著，下次執行時會重新建立此資料夾，要完全清除就先移除它們。

| 位置 | 內容 |
| --- | --- |
| `%USERPROFILE%\.claude`／`~/.claude` | 使用者設定與狀態，是資料夾 |
| `%USERPROFILE%\.claude.json`／`~/.claude.json` | 使用者設定，是檔案 |
| 專案內的 `.claude` 資料夾與 `.mcp.json` | 該專案的設定，可能已納入 Git 與他人共用，刪除前先確認 |

確認後用檔案總管或 Finder 刪除上述項目。macOS 的 Finder 預設隱藏以 `.` 開頭的項目，按 `Command + Shift + .` 可切換顯示。

<a id="help"></a>

## 4. 卡住時才看

| 問題 | 先做這件事 |
| --- | --- |
| 找不到 `claude` | 完全結束終端機再重開，在 VS Code 等編輯器內的終端機要連編輯器一起重開。仍失敗時看下方[修正 PATH](#fix-path)。 |
| 不知道 CLI 裝在哪裡，或懷疑裝了多份 | Windows 執行 `where.exe claude`，macOS 執行 `which -a claude`。只保留一份，建議留官方獨立安裝版，其餘依[原安裝方式移除](#cli-uninstall)。 |
| Windows 輸入 `claude` 卻開啟桌面版 | 舊版桌面版會搶走 `claude` 指令，把桌面版[更新到最新版](#desktop-update)即可。 |
| PowerShell 顯示 `A parameter cannot be found that matches parameter name 'fsSL'` | 在 PowerShell 誤用了 macOS 指令，改用 [PowerShell 安裝指令](#cli-install-windows)。 |
| CMD 顯示 `'irm' is not recognized` | 這是 CMD 而非 PowerShell，改用 CMD 版安裝指令或開啟 PowerShell。 |
| 安裝指令出現 `403`、`syntax error near unexpected token '<'` | 網路或代理伺服器擋下安裝腳本，查官方[安裝排錯](https://code.claude.com/docs/en/troubleshoot-install)。 |

<a id="fix-path"></a>

### 修正 PATH

**Windows：PowerShell**

1. 執行 `Test-Path "$env:USERPROFILE\.local\bin\claude.exe"`。顯示 `False` 表示沒有獨立安裝版，回[安裝](#cli-install-windows)。
2. 顯示 `True` 時，執行以下兩行，把安裝目錄加入使用者 PATH：

   ```powershell
   $currentPath = [Environment]::GetEnvironmentVariable('PATH', 'User')
   [Environment]::SetEnvironmentVariable('PATH', "$currentPath;$env:USERPROFILE\.local\bin", 'User')
   ```

3. 另開新的 PowerShell 視窗，再執行 `claude --version`。

**macOS：終端機（預設 zsh）**

1. 執行 `ls -la ~/.local/bin/claude`。顯示 `No such file or directory` 表示沒有獨立安裝版，回[安裝](#cli-install-macos)。
2. 檔案存在時，執行以下兩行：

   ```bash
   echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
   source ~/.zshrc
   ```

3. 再執行 `claude --version`。

<a id="sources"></a>

## 5. 官方來源

[Claude Code 安裝、更新與移除](https://code.claude.com/docs/en/setup) · [安裝與登入排錯](https://code.claude.com/docs/en/troubleshoot-install) · [CLI 指令參考](https://code.claude.com/docs/en/cli-reference) · [桌面版入門](https://code.claude.com/docs/en/desktop-quickstart) · [桌面版使用與更新](https://code.claude.com/docs/en/desktop) · [安裝 Claude 桌面版](https://support.claude.com/en/articles/10065433-installing-claude-desktop) · [Windows 桌面版部署](https://support.claude.com/en/articles/12622703-deploy-claude-desktop-for-windows) · [macOS 桌面版部署](https://support.claude.com/en/articles/12611117) · [Windows 移除應用程式](https://support.microsoft.com/en-us/windows/uninstall-or-remove-apps-and-programs-in-windows-4b55f974-2cc6-2d2b-d092-5905080eaf98) · [macOS 移除應用程式](https://support.apple.com/en-ie/102610)

Anthropic 官方文件未提供桌面版的移除步驟，桌面版移除依 Windows 與 macOS 的一般移除方式整理。Windows 桌面版的套件與開始功能表名稱為 **Claude**（發行者 Anthropic, PBC），已於本機 Windows 環境確認。本次僅查證文件與指令語法，未實際安裝、更新或移除。

[返回操作手冊索引](README.md) · [返回 KnowledgeHub](../../README.md)
