# Codex 安裝、更新與移除

版本：1.6 · 更新與查證日期：2026-10-15

| 我要做什麼 | 直接前往 |
| --- | --- |
| 安裝 | [桌面版](#desktop-install) · [Windows CLI](#cli-install-windows) · [macOS CLI](#cli-install-macos) |
| 更新 | [桌面版](#desktop-update) · [CLI](#cli-update) |
| 移除／反安裝 | [桌面版](#desktop-uninstall) · [CLI](#cli-uninstall) |

桌面版用視窗操作，CLI 在 PowerShell／終端機輸入指令。**選一條路線即可，CLI 只選一種安裝方式。**

<a id="install"></a>

## 1. 安裝

<a id="desktop-install"></a>

### 桌面版

| 系統 | 操作步驟 |
| --- | --- |
| Windows | 開啟 [Windows 官方下載頁](https://learn.chatgpt.com/docs/windows/windows-app)，下載並安裝，從開始功能表開啟。 |
| macOS | 開啟[桌面版官方頁](https://learn.chatgpt.com/docs/app)，確認晶片及系統相容，下載後依視窗指示拖至「應用程式」，再開啟。 |

目前桌面程式名稱是 **ChatGPT**。開啟後登入 ChatGPT 帳號，再從下拉選單選 **Codex**。能進入 Codex 並收到回覆，即完成基本確認。

<a id="cli-install-windows"></a>

### Windows CLI：PowerShell

開啟 PowerShell，依版本**擇一**執行。用 `$PSVersionTable.PSVersion` 查看目前版本。

**Windows PowerShell 5.1：**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

**PowerShell 7.0 以上，需已安裝 `pwsh`：**

```powershell
pwsh -NoProfile -ExecutionPolicy Bypass -Command "irm https://chatgpt.com/codex/install.ps1 | iex"
```

完成後另開新的 PowerShell 視窗，執行 `codex --version`。顯示版本後，前往[登入 CLI](#cli-login)。

<a id="cli-install-macos"></a>

### macOS CLI：終端機

開啟 Terminal／終端機，執行：

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

完成後另開新的終端機視窗，執行 `codex --version`。顯示版本後，前往[登入 CLI](#cli-login)。

<a id="cli-install-alternatives"></a>

### 選用：npm 或 Homebrew

僅適用於原本已使用這些工具的人。已完成上方獨立安裝者可略過。

| 方式 | 安裝指令 |
| --- | --- |
| npm，Windows／macOS | `npm install -g @openai/codex` |
| Homebrew，macOS | `brew install --cask codex` |

<a id="cli-login"></a>

### 登入 CLI

在 PowerShell／終端機依序操作：

```text
codex login
codex login status
```

第一行會引導至瀏覽器登入 ChatGPT 帳號，完成後再執行第二行確認。之後切到要工作的資料夾，輸入 `codex` 啟動，在 Codex 輸入 `/exit` 退出。

<a id="update"></a>

## 2. 更新

先存檔，退出正在使用的桌面程式或 CLI。

<a id="desktop-update"></a>

### 桌面版

1. 開啟程式選單的 **Check for Updates／檢查更新**，完成後重新啟動。
2. Windows 找不到入口時，到 **Microsoft Store > 下載／程式庫 > 檢查更新**，更新 OpenAI 的 ChatGPT。
3. macOS 找不到入口時，從[官方頁面](https://learn.chatgpt.com/docs/app)重新下載相容版本，結束程式後依安裝視窗取代原程式。

公司管理的設備依 IT 更新流程處理。重開後能進入 Codex 並收到回覆，再確認更新結果。

<a id="cli-update"></a>

### CLI：依原安裝方式更新

| 原安裝方式 | 更新方法 |
| --- | --- |
| Windows 官方獨立安裝版 | 重新執行上方 [PowerShell 5.1 或 7 的安裝指令](#cli-install-windows)。 |
| macOS 官方獨立安裝版 | 重新執行上方 [macOS 安裝指令](#cli-install-macos)。 |
| npm | `npm install -g @openai/codex` |
| Homebrew | 先執行 `brew update`，再執行 `brew upgrade --cask codex`。 |

支援自我更新的版本也可用 `codex update`，若顯示不支援，就回原安裝方式更新。

更新完成後另開終端機，執行 `codex --version` 與 `codex login status`。更新過程無錯誤且能正常啟動，才算完成。原本已是最新版時，版本號可以不變。

<a id="uninstall"></a>

## 3. 移除／反安裝

先結束桌面程式及 CLI。以下移除程式，不清除專案檔案或整個 `.codex` 資料夾，也不會取消訂閱。

<a id="desktop-uninstall"></a>

### 桌面版

| 系統 | 移除方式 |
| --- | --- |
| Windows | **開始 > 設定 > 應用程式 > 已安裝的應用程式**，找到 OpenAI 的 **ChatGPT**，選 **⋯ > 解除安裝**。舊版名稱可能仍是 Codex。 |
| macOS | 在 Finder 的「應用程式」找到 **ChatGPT**，若附有移除工具就使用該工具，否則移至垃圾桶，確認後再清空。 |

<a id="cli-uninstall"></a>

### CLI：npm／Homebrew

依原安裝方式擇一執行：

| 方式 | 移除指令 |
| --- | --- |
| npm，Windows／macOS | `npm uninstall -g @openai/codex` |
| Homebrew，macOS | `brew uninstall --cask codex` |

### CLI：官方獨立安裝版

以下為依官方安裝布局整理的**手動移除**，僅適用於未自訂 `CODEX_INSTALL_DIR`、`CODEX_HOME` 的預設安裝。

**Windows**

1. 用檔案總管開啟 `%LOCALAPPDATA%\Programs\OpenAI\Codex`，刪除裡面的 `bin` 項目本身，不進入後逐一刪檔。
2. 開啟 `%USERPROFILE%\.codex\packages`，只刪除 `standalone` 資料夾，保留其他資料夾。
3. 在「環境變數 > 使用者變數 > Path」移除原本的 `%LOCALAPPDATA%\Programs\OpenAI\Codex\bin` 項目，保留其他項目。

**macOS**

1. Finder 按 `Command + Shift + G`，輸入 `~/.local/bin`，將 `codex` 與存在的 `codex-code-mode-host` 項目移至垃圾桶。
2. 同樣前往 `~/.codex/packages`，只將 `standalone` 資料夾移至垃圾桶，保留其他資料夾。

找不到上述位置或曾自訂安裝目錄時，先確認實際安裝來源，不刪除其他同名檔案。檔案被使用時，先確認程式已完全結束。

**移除後確認：** 另開終端機執行 `codex --version`。若仍能執行，可能還有另一份安裝，依下方方式查來源。

<a id="help"></a>

## 4. 卡住時才看

| 問題 | 先做這件事 |
| --- | --- |
| 找不到 `codex` | 完全結束終端機再重開。仍失敗時，查看[詳細版的 PATH 排錯](<Codex 安裝與更新（1.5 詳細版）.md#troubleshoot-path>)。 |
| 不知道 CLI 裝在哪裡 | Windows 執行 `Get-Command codex -All`，macOS 執行 `type -a codex`。看不懂結果再查[來源判讀](<Codex 安裝與更新（1.5 詳細版）.md#troubleshoot-sources>)。 |
| PowerShell 阻擋 `npm.ps1`／`codex.ps1` | npm 指令改用 `npm.cmd`。Codex 啟動問題見[詳細處理](<Codex 安裝與更新（1.5 詳細版）.md#troubleshoot-codex-ps1>)。 |

<a id="sources"></a>

## 5. 官方來源

[CLI 安裝與更新](https://learn.chatgpt.com/docs/codex/cli) · [桌面更新](https://learn.chatgpt.com/docs/enterprise/manage-app-updates) · [Windows 移除](https://support.microsoft.com/en-us/windows/uninstall-or-remove-apps-and-programs-in-windows-4b55f974-2cc6-2d2b-d092-5905080eaf98) · [macOS 移除](https://support.apple.com/en-ie/102610) · [npm 移除](https://docs.npmjs.com/cli/v11/commands/npm-uninstall/) · [Homebrew 指令](https://docs.brew.sh/Manpage)

獨立版的手動移除位置依官方 [Windows 安裝腳本](https://github.com/openai/codex/blob/main/scripts/install/install.ps1)與 [macOS 安裝腳本](https://github.com/openai/codex/blob/main/scripts/install/install.sh)整理，並非官方提供的一鍵反安裝指令。本次僅查證文件與指令語法，未實際安裝、更新或移除。

[詳細教學、排錯與背景（1.5 版留存）](<Codex 安裝與更新（1.5 詳細版）.md>) · [返回操作手冊索引](README.md) · [返回 KnowledgeHub](../../README.md)
