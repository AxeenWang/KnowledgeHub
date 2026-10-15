# Git CLI 安裝、更新與移除

版本：1.0 · 更新與查證日期：2026-10-15

| 我要做什麼 | 直接前往 |
| --- | --- |
| 安裝 | [Windows](#install-windows) · [macOS](#install-macos) |
| 更新 | [依原安裝方式更新](#update) |
| 移除／反安裝 | [Windows](#uninstall-windows) · [macOS](#uninstall-macos) |

本手冊涵蓋 Windows 10／11 與 macOS，在 PowerShell／終端機輸入 `git` 使用。Windows 指令適用於 Windows PowerShell 5.1 與 PowerShell 7 以上。Linux、WSL、Portable、MacPorts 與原始碼編譯安裝不在本篇範圍。

Git 負責本機版本控制，使用本機功能不需要 GitHub 帳號。GitHub CLI 的指令是 `gh`，屬於另一項工具。連線到 GitHub 等遠端服務時，另依服務要求設定登入或 SSH。

<a id="requirements"></a>

## 0. 使用前確認

先開啟 PowerShell／Terminal，執行：

```text
git --version
```

顯示 `git version ...` 表示已有可用的 Git，先[確認來源](#check-source)，需要時再更新。macOS 若跳出安裝開發工具的提示，可依下方 [Apple 路線](#install-macos-apple)完成。

**Windows 選一種安裝方式即可。macOS 已有 Apple Git 且夠用時可以直接使用，需要獨立管理較新版本時再安裝 Homebrew 版。** 後續更新與移除都依原安裝方式進行。

<a id="install"></a>

## 1. 安裝

<a id="install-windows"></a>

### Windows：Git for Windows 安裝程式

1. 開啟 [Git 官方 Windows 下載頁](https://git-scm.com/install/windows)，選 **Standalone Installer**。一般 Intel／AMD 電腦用 x64，Windows ARM 電腦用 ARM64。可到 **設定 > 系統 > 關於 > 系統類型** 確認。
2. 執行下載的安裝程式，需要時依 Windows 提示授予管理員權限。
3. 出現 **Adjusting your PATH environment** 時，選 **Git from the command line and also from 3rd-party software**，讓 PowerShell、CMD 與編輯器都能找到 Git。其餘選項可先保留預設值，或遵循專案與公司規範。
4. 安裝完成後，另開新的 PowerShell 視窗，執行 `git --version`。顯示版本後，前往[首次設定](#first-setup)。

Git for Windows 也包含 Git Bash。使用 PowerShell 執行 `git` 時，不必另外開啟 Git Bash。安裝選項可參考 [GitHub 官方操作說明](https://accessibility.github.com/documentation/guide/cli/)。

### Windows 選用：WinGet

若原本已使用 WinGet，可改採此路線。先執行 `winget --version` 確認可用，再執行：

```powershell
winget install --id Git.Git -e --source winget
```

依提示完成後，另開 PowerShell 執行 `git --version`。沒有 WinGet 時可直接使用上方安裝程式，需要 WinGet 本身時再看 [Microsoft 官方說明](https://learn.microsoft.com/en-us/windows/package-manager/winget/)。

這個套件安裝的也是 Git for Windows，不需再下載安裝一份。Git 官方提醒，WinGet 的 `Git.Git` 套件由社群維護，版本可能晚於官方發布。[來源：Git Windows 安裝頁](https://git-scm.com/install/windows)

<a id="install-macos"></a>

### macOS：Homebrew

適合希望自行安裝與更新 Git 的使用者，Intel 與 Apple 晶片皆可使用。先執行 `brew --version`，確認 Homebrew 可用。

沒有 Homebrew 時，先依 [Homebrew 官方安裝說明](https://docs.brew.sh/Installation)安裝，完成安裝器顯示的 **Next steps**，再另開 Terminal。Homebrew 需要相容的 macOS 與開發工具，安裝前以該頁需求為準。

```bash
brew install git
```

完成後另開 Terminal，執行：

```bash
git --version
command -v git
```

預設 Homebrew 路徑，Apple 晶片通常是 `/opt/homebrew/bin/git`，Intel 通常是 `/usr/local/bin/git`。若仍顯示 `/usr/bin/git`，看[來源與 PATH 排錯](#help)。這裡的 Git 是 formula，安裝時不加 `--cask`。[來源：Git 套件](https://formulae.brew.sh/formula/git)、[Homebrew 安裝布局](https://docs.brew.sh/Installation)

<a id="install-macos-apple"></a>

### macOS 選用：Apple Command Line Tools

不想另外管理 Homebrew，且 Apple 提供的 Git 已符合需求時，可用這條路線：

```bash
xcode-select --install
```

依系統視窗按「安裝」並同意授權，完成後再執行 `git --version`。若顯示工具已安裝，就先確認 Git 能否執行，更新請用下方 Apple 路線。已有完整 Xcode 時，不必為 Git 再裝一套 Command Line Tools。

Apple Git 隨開發工具提供，版本可能與 Git 官網不同。Git 官網已不再推薦長期未更新的舊 macOS 獨立安裝包。[來源：Git macOS 安裝頁](https://git-scm.com/install/mac)、[Apple 開發工具說明](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools)

<a id="first-setup"></a>

### 首次設定：提交者姓名與電子郵件

要建立 commit 前，將以下範例換成自己的資料，Windows 與 macOS 寫法相同。已有設定且正確時可略過。

```text
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

姓名與電子郵件會寫進之後建立的 commit，公開專案應使用你願意公開的地址。這兩項是提交者資訊，不會讓你登入 GitHub。`--global` 套用於目前電腦使用者，個別專案可在其資料夾內省略 `--global` 另設。

確認設定：

```text
git config --get user.name
git config --get user.email
```

能顯示版本與預期的提交者資訊，即完成基本確認。這不代表已驗證遠端登入或推送權限。[來源：Pro Git 首次設定](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

<a id="update"></a>

## 2. 更新

先存檔並結束正在執行 Git 的任務，關閉使用該 Git 的編輯器與終端機。另開一個 PowerShell／Terminal 執行更新，**依原安裝方式擇一**。

| 原安裝方式 | 更新方法 |
| --- | --- |
| Windows，官方安裝程式 | 執行 `git update-git-for-windows`，依提示下載與安裝。找不到此子指令時，從[官方下載頁](https://git-scm.com/install/windows)下載新版，安裝至原位置。 |
| Windows，WinGet | 執行 `winget upgrade --id Git.Git -e --source winget`。 |
| macOS，Homebrew | 先執行 `brew update` 更新套件資料，再執行 `brew upgrade git` 更新 Git。 |
| macOS，Apple Command Line Tools | 到 **系統設定 > 一般 > 軟體更新**，安裝適用的 Command Line Tools 更新。 |
| macOS，完整 Xcode 內的 Git | 依原取得方式更新 Xcode，例如 App Store 的「更新」，或從 Apple Developer 取得相容版本。 |

Windows 的 `git update-git-for-windows` 是 Git for Windows 專屬工具。`git pull` 用來取得並整合專案內容，更新 Git 程式請使用上表方法。

完成後另開終端機，再執行 `git --version` 並[確認執行來源](#check-source)。更新無錯誤、來源符合預期且可顯示版本，即完成基本確認。原本已是該來源最新版時，版本號可以不變，各發行管道也不一定同時提供同一版本。

來源：[Git for Windows 更新 FAQ](https://gitforwindows.org/faq)、[WinGet upgrade](https://learn.microsoft.com/en-us/windows/package-manager/winget/upgrade)、[Homebrew 指令](https://docs.brew.sh/Manpage)、[Apple 開發工具更新](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools)。

<a id="uninstall"></a>

## 3. 移除／反安裝

先結束正在使用 Git 的任務、編輯器與終端機。**移除 Git 程式時保留專案資料夾及其中的 `.git`**，`.git` 保存該專案的本機版本歷史。

使用者的 `.gitconfig`、`.config/git/`、`.ssh/` 與系統憑證儲存區也不需要為反安裝而刪除。保留這些資料方便重新安裝，移除程式也不等於登出遠端服務或撤銷憑證。

<a id="uninstall-windows"></a>

### Windows

| 原安裝方式 | 移除方式 |
| --- | --- |
| Git for Windows 安裝程式 | 到 **開始 > 設定 > 應用程式 > 已安裝的應用程式**，找到 **Git**，選 **⋯ > 解除安裝**。Windows 10 的入口為「應用程式與功能」。 |
| WinGet | 在 PowerShell 執行 `winget uninstall --id Git.Git -e --source winget`。 |

WinGet 找不到已安裝套件時，改用 Windows 設定中的解除安裝入口。使用正常反安裝流程，避免直接刪除整個安裝資料夾而留下反安裝與 PATH 紀錄。

完成後確認 Windows 應用程式清單已不再列出該套 Git，另開 PowerShell 執行 `git --version`。若已沒有其他 Git，應顯示找不到命令。若仍顯示版本，依下方[確認來源](#check-source)辨識是否還有另一套安裝。

來源：[Windows 移除程式](https://support.microsoft.com/en-us/windows/uninstall-or-remove-apps-and-programs-in-windows-4b55f974-2cc6-2d2b-d092-5905080eaf98)、[WinGet uninstall](https://learn.microsoft.com/en-us/windows/package-manager/winget/uninstall)。

<a id="uninstall-macos"></a>

### macOS：Homebrew

```bash
brew uninstall git
```

若 Homebrew 提示其他套件依賴 Git，先處理依賴關係，不加 `--ignore-dependencies` 強制移除。

完成後執行 `brew list --versions git`，正常情況不再列出版本。再另開 Terminal 執行 `command -v git` 與 `git --version`。若改為 `/usr/bin/git` 或顯示 Apple Git，表示目前使用的是 Apple 提供的另一份 Git，不能只憑 `git` 還能執行就判定移除失敗。[來源：Homebrew 指令](https://docs.brew.sh/Manpage)

### macOS：Apple 提供的 Git

Apple Git 隨 Command Line Tools 或 Xcode 提供。本手冊建議保留系統提供的版本，不手動刪除 `/usr/bin/git`。

如果確定整組 **Command Line Tools** 都不再需要，Apple 官方提供以下移除方式。**這會刪除整套開發工具，影響編譯器、SDK 與依賴它們的工具，並非只移除 Git。** 使用 Homebrew 或其他開發工具者應先確認依賴。

```bash
sudo rm -rf /Library/Developer/CommandLineTools
```

這個位置只適用於獨立 Command Line Tools。若 `xcode-select -p` 顯示 `/Applications/Xcode.app/Contents/Developer` 等 Xcode 路徑，上述指令不會移除 Xcode 內的 Git。需要移除整套 Xcode 時，另按 Xcode 的管理流程處理。

移除 Command Line Tools 後，系統仍可能保留 `/usr/bin/git` 的入口，執行時可能再次提示安裝工具，不要為了讓指令完全消失去刪除它。其他移除與更新收據的細節見 [Apple 官方文件](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools)。

<a id="help"></a>

## 4. 卡住時才看

<a id="check-source"></a>

### 確認目前執行哪一份 Git

**Windows：PowerShell**

```powershell
Get-Command git -All | Select-Object CommandType, Source, Definition
where.exe git
winget list --id Git.Git -e
```

前兩行列出命令來源及 PATH 中找到的執行檔，最後一行協助確認 WinGet 是否辨識到 Git for Windows，未使用 WinGet 時可略過。同一安裝目錄內的 `cmd\git.exe` 與 `bin\git.exe` 可能屬於同一套 Git，不能只憑列出多個路徑就認定重複安裝。

**macOS：Terminal**

```bash
type -a git
command -v git
```

已使用 Homebrew 時，再執行 `brew list --versions git` 確認 Homebrew 管理的版本。不同位置可能同時存在，實際使用哪份由命令解析與 PATH 順序決定。

| 問題 | 先做這件事 |
| --- | --- |
| Windows 找不到 `git` | 完全結束終端機再重開。編輯器內的終端機要連編輯器一起重開。仍失敗時，重新執行原安裝程式並選擇上方 PATH 選項。 |
| Windows 更新後版本沒變 | 先確認原本是否已是最新版，再查來源，可能先執行到其他工具附帶的 Git。由該工具管理的版本要透過原工具更新。 |
| `git update-git-for-windows` 顯示不是 Git 指令 | 可能不是 Git for Windows 或版本太舊，依上方原安裝方式更新。macOS 不使用這個指令。 |
| WinGet 找不到可更新版本 | 執行 `winget list --id Git.Git -e` 確認辨識結果。可能已是該管道最新版，套件發布也可能較晚，不代表官網沒有新版。 |
| macOS 裝了 Homebrew Git，仍執行 Apple Git | 依 [Homebrew 安裝說明](https://docs.brew.sh/Installation)完成 `brew shellenv` 的 Next steps 設定，另開 Terminal，再用 `command -v git` 確認。 |
| macOS 顯示 `invalid active developer path` | 系統更新後開發工具可能需更新，先查看「軟體更新」，必要時依 Apple 文件重新安裝相容的 Command Line Tools。 |
| 移除後仍能執行 `git` | 查來源。可能是另一套獨立安裝、工具內附版本或 Apple 系統入口，依對應方式處理。 |

PATH 與開發工具排錯參考：[GitHub Windows 安裝說明](https://accessibility.github.com/documentation/guide/cli/)、[Homebrew shellenv 指令](https://docs.brew.sh/Manpage)、[Apple 開發工具說明](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools)。

<a id="sources"></a>

## 5. 官方來源與驗證範圍

| 來源 | 查證內容 |
| --- | --- |
| [Git — Install for Windows](https://git-scm.com/install/windows) | 安裝程式架構、WinGet 指令與套件維護來源。 |
| [Git — Install for macOS](https://git-scm.com/install/mac) | Homebrew、Command Line Tools 與舊獨立安裝包狀態。 |
| [Git for Windows FAQ](https://gitforwindows.org/faq) | 更新方式與專屬更新指令。 |
| [GitHub — Using Git, GitHub CLI, and Copilot CLI with a Screen Reader](https://accessibility.github.com/documentation/guide/cli/) | Windows 安裝器的 PATH 選項。 |
| [Pro Git — First-Time Git Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) | 提交者身分與設定範圍，作者 Scott Chacon、Ben Straub。 |
| [Git — gitrepository-layout](https://git-scm.com/docs/gitrepository-layout) | `.git` 與版本庫資料的用途。 |
| [Microsoft WinGet：install](https://learn.microsoft.com/en-us/windows/package-manager/winget/install)、[upgrade](https://learn.microsoft.com/en-us/windows/package-manager/winget/upgrade)、[uninstall](https://learn.microsoft.com/en-us/windows/package-manager/winget/uninstall) | 套件識別、安裝、更新與移除指令。 |
| [Microsoft — Uninstall or remove apps and programs in Windows](https://support.microsoft.com/en-us/windows/uninstall-or-remove-apps-and-programs-in-windows-4b55f974-2cc6-2d2b-d092-5905080eaf98) | Windows 解除安裝入口。 |
| [Homebrew — Installation](https://docs.brew.sh/Installation)、[git formula](https://formulae.brew.sh/formula/git)、[brew Manpage](https://docs.brew.sh/Manpage) | 安裝前提、預設路徑、套件與更新／移除指令。 |
| [Apple — Installing the command-line tools](https://developer.apple.com/documentation/xcode/installing-the-command-line-tools) | Apple 開發工具的安裝、更新、移除與適用範圍。 |
| [Apple — Xcode Resources](https://developer.apple.com/xcode/resources) | Xcode 的 App Store 與 Apple Developer 下載管道。 |

以上程序依官方文件整理，PATH 來源判讀與保留資料的建議為本手冊的操作整理。本次查證日期為 2026-10-15，未實際安裝、更新或移除 Git，也未測試遠端登入、clone 或 push。實際可用版本與相容性以各管道當時提供的資訊為準。

[返回操作手冊索引](README.md) · [返回 KnowledgeHub](../../README.md)
