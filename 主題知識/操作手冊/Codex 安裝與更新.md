# Codex 安裝與更新

文件版本：1.3 · 排版更新日期：2026-10-15 · 資料查證日期：2026-10-15

適用範圍：Windows 與 macOS 桌面版，以及 Codex CLI 的安裝、登入與更新。

<a id="start"></a>

## 1. 開始前與快速導覽

先選桌面版或 CLI 的一條路線即可。只想使用視窗介面者，從桌面版安裝開始。想在終端機操作者，從 CLI 安裝方式選擇開始。已有 CLI、只想更新者，可直接前往 CLI 更新。

| 我要做什麼 | 直接前往 |
| --- | --- |
| 安裝 Windows 桌面版 | [Windows 桌面版安裝](#desktop-install-windows) |
| 安裝 macOS 桌面版 | [macOS 桌面版安裝](#desktop-install-macos) |
| 登入桌面版並確認可用 | [桌面版登入](#desktop-login) |
| 更新桌面版 | [桌面版更新](#desktop-update) |
| 第一次安裝 CLI | [CLI 安裝方式選擇](#cli-install-select) |
| 更新已安裝的 CLI | [CLI 更新方式選擇](#cli-update-select) |
| 安裝、登入或更新失敗 | [疑難排解](#troubleshooting) |

**本書目錄**

1. [開始前與快速導覽](#start)
2. [桌面版安裝與更新](#desktop)
3. [CLI 首次安裝](#cli-install)
4. [CLI 更新](#cli-update)
5. [疑難排解](#troubleshooting)
6. [來源與驗證範圍](#references)

<a id="before-start"></a>

### 1.1 準備條件

- 準備可登入的 ChatGPT 帳號及網路連線。本手冊採用 ChatGPT 帳號登入流程。
- 確認電腦允許安裝應用程式。受公司管理的設備應使用管理員核准的安裝方式。
- 從下方官方文件進入下載頁，核對發行者為 OpenAI，並確認該頁顯示的系統及處理器需求。
- 先準備一個不含機密或重要原始資料的練習資料夾，供首次開啟專案時使用。

帳號可用功能及權限應以實際登入結果與組織設定確認。本手冊不固定列出方案價格、最新版本號或最低作業系統版本，避免將變動資訊當成永久條件。

<a id="terminal-basics"></a>

### 1.2 看懂指令與操作位置

- **Windows**：從開始功能表開啟 **Windows PowerShell**或已安裝的 **PowerShell 7**。Windows PowerShell 5.1 的啟動指令是 `powershell`，PowerShell 7.0 以上版本則是 `pwsh`。兩者可以並存，不會因為目前視窗是 PowerShell 7，就將 `powershell` 自動改成 7。
- **macOS**：按 `Command + Space`，搜尋並開啟 Terminal／終端機。
- 程式碼框中的指令貼到對應的 PowerShell 或終端機，一次執行一行並按 Enter。不要複製框線、語言標籤或指令前額外的 `$`、`>` 提示符號。
- 指令報錯時先停止，看[疑難排解](#troubleshooting)，不要繼續執行後面的登入或驗證步驟。
- 首次安裝 CLI 可使用一般使用者的終端機。若受管理的設備要求核准，依組織流程處理。

練習資料夾可先用檔案總管或 Finder 建立，例如在自己的使用者資料夾新增 `CodexPractice`。CLI 使用者也可照[練習資料夾指令](#cli-practice)建立。

<a id="desktop"></a>

## 2. 桌面版安裝與更新

桌面版透過視窗管理專案、對話與本機檔案。依自己的作業系統完成安裝，再進行[登入與確認可用](#desktop-login)。產品名稱差異見[產品名稱與文件沿革](#product-background)。

<a id="desktop-install-windows"></a>

### 2.1 Windows：安裝桌面版

**適用環境：** Windows。

**必要條件：** 已確認官方頁面的系統需求，且設備允許安裝應用程式。

**操作步驟**

1. 開啟 [ChatGPT desktop app for Windows](https://learn.chatgpt.com/docs/windows/windows-app)。
2. 點選頁面內的 Windows 桌面程式下載連結。
3. 依 Windows 安裝提示完成安裝。如出現管理員核准提示，交由有權限的人員確認。
4. 從開始功能表開啟安裝完成的程式。

**成功判斷：** 可看到登入畫面或程式主畫面。官方安裝流程可能出現 Microsoft Store 元件。受管理的電腦若無法自行安裝，請管理員參考[官方 Windows 部署說明](https://learn.chatgpt.com/docs/enterprise/windows-deployment)。

**選用：透過 winget 安裝**

若電腦已有 winget，也可在 PowerShell 執行官方提供的安裝指令。這與上一種方式擇一使用即可。

```powershell
winget install --id 9PLM9XGG6VKS -s msstore
```

**成功判斷：** 安裝作業完成後，可從開始功能表開啟程式。此指令使用 Microsoft Store 來源，產品識別碼依查證日的 [Windows 官方文件](https://learn.chatgpt.com/docs/windows/windows-app)記錄。

**失敗時：** [桌面版與其他問題](#troubleshoot-desktop)。

**下一步：** [登入桌面版](#desktop-login)。

<a id="desktop-install-macos"></a>

### 2.2 macOS：安裝桌面版

**適用環境：** macOS，須確認下載項目與自己的 Mac 相容。

**必要條件：** 已確認系統與晶片需求，且設備允許安裝應用程式。

**操作步驟**

1. 在 Mac 開啟 [ChatGPT desktop app 官方頁面](https://learn.chatgpt.com/docs/app)。
2. 確認下載項目適用於自己的 Mac。查證時頁面標示 **macOS（Apple Silicon）**，可先從 Apple 選單的「關於這台 Mac」確認晶片。Intel Mac 請先確認當時官方是否另有相容下載。
3. 點選 macOS 下載連結，開啟下載的安裝檔，依安裝視窗指示完成。
4. 若下載的是磁碟映像檔，且視窗顯示拖曳安裝方式，將程式拖至 **Applications／應用程式**，再從應用程式資料夾開啟。
5. 依 macOS 的正常提示確認開啟，接著進行[桌面版登入與確認可用](#desktop-login)登入。

**成功判斷：** 可從應用程式資料夾開啟程式並看到登入或主畫面。下載來源及登入流程依[官方桌面版說明](https://learn.chatgpt.com/docs/app)，拖曳安裝步驟為依實際安裝視窗操作的一般指引，未在 Mac 上實測。

**失敗時：** [桌面版與其他問題](#troubleshoot-desktop)。

**下一步：** [登入桌面版](#desktop-login)。

<a id="desktop-login"></a>

### 2.3 登入桌面版並確認可用

**操作位置：** 桌面程式與開啟的瀏覽器。

**操作步驟**

1. 開啟桌面程式，選擇 **Continue to sign in／繼續登入**或對應的 ChatGPT 帳號登入選項。
2. 在開啟的瀏覽器完成登入，再回到桌面程式，確認已進入主畫面。
3. 若帳號有多個工作區，確認目前選到預期的工作區。
4. 在新版介面的 ChatGPT 下拉選單選擇 **Codex**。
5. 使用新增專案或開啟資料夾的選項，選取準備好的練習資料夾，核對畫面顯示的位置。
6. 建立新對話，送出以下練習提示。

    ```text
    請列出目前資料夾的第一層項目，簡單說明這個資料夾的內容。只讀取，不修改檔案。
    ```

**成功判斷：** Codex 能回應提示，並在需要存取本機資料時依目前權限處理。完成後確認練習資料夾沒有被修改。這是本手冊建議的操作檢查，不代表官方保證每個帳號均具備相同功能。

登入、選擇資料夾及切換 Codex 的介面流程依[官方快速入門](https://learn.chatgpt.com/docs/quickstart)及[官方驗證文件](https://learn.chatgpt.com/docs/auth)整理。

**失敗時：** [桌面版與其他問題](#troubleshoot-desktop)。

<a id="desktop-update"></a>

### 2.4 更新桌面版

**適用環境：** Windows 或 macOS 桌面版。

**操作步驟**

官方文件指出，桌面程式通常會自行檢查並安裝更新。手動檢查時依下列方式操作。

1. 先將正在編輯的文件存檔，確認進行中的任務已到適合重啟的時點。
2. 在程式選單尋找 **Check for Updates／檢查更新**。選單位置可能隨版本不同。
3. 若提示有更新，依畫面完成下載、安裝與重新啟動。
4. 完全結束並重新開啟程式，再執行[桌面版更新後檢查](#desktop-verify)檢查。

Windows 使用者依程式的結束選項操作。macOS 使用者可透過程式選單的「結束」或 `Command + Q` 完全結束，再從應用程式資料夾重開。只關閉視窗不一定會結束程式。

若沒有檢查更新入口，先依原安裝管道或組織的軟體派送方式確認更新，不要改裝另一個來源來推測問題已解決。

**成功判斷：** 完成[桌面版更新後檢查](#desktop-verify)。

**失敗時：** 先看[組織管理的更新](#desktop-managed-updates)，再看[桌面版與其他問題](#troubleshoot-desktop)。

<a id="desktop-managed-updates"></a>

### 2.5 組織管理的更新

1. 開啟 **Settings > General／設定 > 一般**。
2. 若 **In-app updates** 顯示 **Managed**，且註明組織已關閉程式內更新，請由管理員派送核准版本。
3. 即使仍看到 **Check for Updates**，也不能據此判斷組織允許程式內更新。

組織停用程式內更新，不代表 Microsoft Store、Intune 或其他管理工具也停止更新。以上行為依[官方更新管理說明](https://learn.chatgpt.com/docs/enterprise/manage-app-updates)整理。

<a id="desktop-verify"></a>

### 2.6 桌面版更新後檢查

- 程式可以重新開啟，登入狀態與工作區符合預期。
- 原有專案與資料夾仍可開啟。
- 重做[桌面版登入與確認可用](#desktop-login)的只讀取練習，確認基本功能可用。
- 若要留下更新紀錄，記下程式顯示的版本、日期及更新結果。

「已安裝某版本」與「目前管道沒有可用更新」是兩種不同結果。記錄版本號本身不能證明已是最新版本，也不能證明所有新功能都已開放。

<a id="cli-install"></a>

## 3. CLI 首次安裝

CLI 是 Command Line Interface，指在終端機輸入指令操作的版本。**只用桌面版可以略過本節**，桌面版與 CLI 分別安裝、分別更新。

本節已逐一核對 [CLI 官網](https://learn.chatgpt.com/docs/codex/cli)的 **macOS/Linux、Windows、npm、Homebrew** 四個安裝分頁。初次安裝建議先走官方獨立安裝程式，這條路線不用先準備 Node.js、npm 或 Homebrew。這是本手冊為初學者安排的路線。

<a id="cli-install-select"></a>

### 3.1 選擇安裝方式

| 你的情況 | 安裝方式與下一步 |
| --- | --- |
| Windows，首次安裝 | [官方 Windows 獨立安裝程式](#cli-install-windows) |
| macOS，首次安裝 | [官方 macOS 獨立安裝程式](#cli-install-macos) |
| 已習慣使用 npm | [使用 npm 安裝](#cli-install-npm) |
| 已習慣使用 Homebrew | [使用 Homebrew 安裝](#cli-install-homebrew) |
| 已經裝過 CLI，只想更新 | [先辨識原安裝方式，再更新](#cli-update-select) |

**只選一種安裝方式**。完成該方式後，前往[CLI 登入](#cli-login)，不需要把所有安裝指令都執行一遍。Windows 的 PowerShell 與 WSL 是不同環境，本手冊的 Windows 指令以原生 PowerShell 為準。

<a id="cli-install-windows"></a>

### 3.2 Windows：安裝 CLI

**適用環境：** Windows，使用 Windows PowerShell 5.1 或 PowerShell 7.0 以上版本。

**必要條件：** 電腦可連線至官方下載來源。選用 PowerShell 7 寫法時，須已安裝且可執行 `pwsh`。

**操作步驟**

1. 開啟新的 Windows PowerShell 或 PowerShell 7 視窗，檢查目前版本。

    ```powershell
    $PSVersionTable.PSVersion
    ```

    `Major` 為 `5`、`Minor` 為 `1` 時是 Windows PowerShell 5.1，`Major` 為 `7` 或更高時可使用 PowerShell 7.0 以上版本的寫法。

2. 依要使用的版本，**擇一**執行下列安裝指令，等待完成。

    **Windows PowerShell 5.1，OpenAI 官網原樣指令：**

    ```powershell
    powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
    ```

    **PowerShell 7.0 以上版本，使用 `pwsh` 啟動：**

    先執行 `pwsh --version`，確認可以找到 `pwsh`，且顯示版本為 7.0 以上，再執行：

    ```powershell
    pwsh -NoProfile -ExecutionPolicy Bypass -Command "irm https://chatgpt.com/codex/install.ps1 | iex"
    ```

3. 安裝完成後關閉此 PowerShell，重新開啟一個新視窗，讓命令搜尋路徑的變更生效。
4. 執行版本檢查。

    ```powershell
    codex --version
    ```

**成功判斷：** 顯示以 `codex-cli` 開頭的版本資訊。

**失敗時：** 先看[找不到 codex 或仍是舊版本](#troubleshoot-path)，不要連續改用其他方式重裝。

**指令說明**

兩種寫法均下載並執行同一份 OpenAI 安裝腳本。`powershell` 版本依 [CLI 官網 Windows 分頁](https://learn.chatgpt.com/docs/codex/cli)，`pwsh` 版本是本手冊依 [Microsoft 的 pwsh 參數文件](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_pwsh)調整的等效啟動寫法，並非 OpenAI 官網逐字範例。`-NoProfile` 表示這次啟動不載入個人 PowerShell 設定檔。

`-ExecutionPolicy Bypass` 僅設定這次啟動的 PowerShell 行程，不會永久變更執行原則。若組織政策阻擋執行，請交由管理員處理。若找不到 `pwsh`，代表尚未有可用的 PowerShell 7 命令，可先使用 Windows PowerShell 5.1 的方式。

**下一步：** [登入 CLI](#cli-login)。

<a id="cli-install-macos"></a>

### 3.3 macOS：安裝 CLI

**適用環境：** macOS 終端機。

**必要條件：** 電腦可連線至官方下載來源。

**操作步驟**

1. 按 `Command + Space` 開啟 Spotlight，搜尋並開啟 **Terminal／終端機**。
2. 貼上下列整行指令，按 Enter，等待安裝完成。

    ```bash
    curl -fsSL https://chatgpt.com/codex/install.sh | sh
    ```

這是 [CLI 官網 macOS/Linux 分頁](https://learn.chatgpt.com/docs/codex/cli)列出的指令，會下載並執行 OpenAI 的安裝腳本。若安裝程式提示命令搜尋路徑的後續設定，依畫面完成。

3. 關閉終端機視窗，開啟新的終端機視窗，再檢查版本。

    ```bash
    codex --version
    ```

**成功判斷：** 顯示以 `codex-cli` 開頭的版本資訊。若找不到指令，先看[找不到 codex 或仍是舊版本](#troubleshoot-path)。

**下一步：** [登入 CLI](#cli-login)。

<a id="cli-install-npm"></a>

### 3.4 選用：使用 npm 安裝 CLI

**適用環境：** Windows 或 macOS，已有可用的 Node.js 與 npm。

若已完成官方獨立安裝程式的安裝，直接前往[CLI 登入](#cli-login)。npm 是隨 Node.js 提供的套件管理工具。

**操作步驟**

1. 在 PowerShell 或終端機依序檢查 Node.js 與 npm。

    ```text
    node --version
    npm --version
    ```

    兩者都須顯示版本號，才能繼續。若尚未安裝這些工具，可改走 [Windows 獨立安裝程式](#cli-install-windows)或 [macOS 獨立安裝程式](#cli-install-macos)，不必為了 Codex 額外設定 npm 環境。

2. 執行安裝並檢查版本，Windows 與 macOS 指令相同。

    ```text
    npm install -g @openai/codex
    codex --version
    ```

**成功判斷：** 安裝沒有報錯，且 `codex --version` 顯示 CLI 版本。

**指令說明**

`-g` 表示安裝到 npm 的全域工具位置，讓你可以從不同資料夾執行 `codex`，不是將它加入目前專案。官網 npm 分頁的安裝與更新使用同一指令。也可使用 `npm install -g @openai/codex@latest` 明確指定 npm 的 `latest` 標籤。

**失敗時：** [npm 與更新指令報錯](#troubleshoot-update)。

**下一步：** [登入 CLI](#cli-login)。

<a id="cli-install-homebrew"></a>

### 3.5 選用：使用 Homebrew 安裝 CLI

**適用環境：** 已有 Homebrew 的 macOS。

若已完成官方獨立安裝程式的安裝，直接前往[CLI 登入](#cli-login)。

**操作步驟**

1. 執行 `brew --version`，確認工具可用。
2. 安裝並檢查版本。

    ```bash
    brew install --cask codex
    codex --version
    ```

**成功判斷：** 安裝沒有報錯，且 `codex --version` 顯示 CLI 版本。

**指令說明：** 這裡的 `codex` cask 安裝的是 CLI。指令依 [CLI 官網 Homebrew 分頁](https://learn.chatgpt.com/docs/codex/cli)，桌面程式請依[桌面版安裝與更新](#desktop)安裝。

**失敗時：** [npm 與更新指令報錯](#troubleshoot-update)。

**下一步：** [登入 CLI](#cli-login)。

<a id="cli-login"></a>

### 3.6 登入 CLI

**操作位置：** PowerShell 或 macOS 終端機，登入驗證在瀏覽器完成。

**操作步驟**

1. 在 PowerShell 或終端機執行登入指令。

    ```text
    codex login
    ```

2. 依開啟的瀏覽器畫面完成登入，再回到終端機確認登入成功。若沒有自動開啟瀏覽器，依終端機顯示的登入網址操作。
3. 檢查目前登入狀態。

    ```text
    codex login status
    ```

**成功判斷：** 顯示已登入及目前的驗證方式。未登入成功時，先處理登入問題，再開始任務。

**登入方式說明：** 本手冊使用 ChatGPT 帳號登入，不需要先建立 API key。API key 是另一種按 API 使用量計費的登入方式，不要為了完成本節而改用金鑰登入。以上依[官方驗證文件](https://learn.chatgpt.com/docs/auth)整理。

**失敗時：** [CLI 瀏覽器登入沒有完成](#troubleshoot-login)。

**下一步：** [建立練習資料夾並第一次使用](#cli-practice)。

<a id="cli-practice"></a>

### 3.7 建立練習資料夾並第一次使用

**必要條件：** 已完成 CLI 登入。下列範例會在自己的使用者資料夾建立或沿用 `CodexPractice`，不會建立範例內容檔。若該資料夾已有重要資料，請先換一個名稱。

**操作步驟**

1. 依自己的作業系統，**擇一**執行練習資料夾指令。

    **Windows PowerShell：**

    ```powershell
    New-Item -ItemType Directory -Path "$env:USERPROFILE\CodexPractice" -Force
    Set-Location "$env:USERPROFILE\CodexPractice"
    Get-Location
    ```

    **macOS 終端機：**

    ```bash
    mkdir -p "$HOME/CodexPractice"
    cd "$HOME/CodexPractice"
    pwd
    ```

    最後一行顯示的位置應以 `CodexPractice` 結尾。Windows 與 macOS 的指令區塊擇一執行。

2. 在剛才的終端機啟動 CLI。

    ```text
    codex
    ```

3. 若出現資料夾信任或權限提示，確認畫面上的位置就是練習資料夾，再選擇適合的權限。
4. 在 **Codex 的輸入區**輸入下列文字並送出。

    ```text
    請列出目前資料夾的第一層項目，簡單說明這個資料夾的內容。只讀取，不修改檔案。
    ```

**成功判斷：** 收到回覆。新建的空資料夾可能回報沒有項目，這也是正常結果。這次練習以確認登入、資料夾及基本回應為目的。

**下一步：** [退出與再次啟動 CLI](#cli-exit)。

<a id="cli-exit"></a>

### 3.8 退出與再次啟動 CLI

在 Codex 輸入區輸入 `/exit` 並送出，回到 PowerShell 或 macOS 的命令提示畫面。之後重新使用時，切到要處理的資料夾再執行 `codex` 即可。

**分清楚輸入位置**：`codex login`、安裝與更新指令放在 PowerShell／終端機，`/exit` 與練習提示放在 Codex 輸入區。不要把安裝指令當成對話送給 Codex。退出方式依[官方 CLI 指令參考](https://learn.chatgpt.com/docs/cli/reference#interactive-shortcuts)。

<a id="cli-update"></a>

## 4. CLI 更新

**先退出正在使用的 CLI，再開啟新的 PowerShell 或終端機視窗**。以下方式擇一使用，完成後重新執行 `codex --version` 及 `codex login status`，再用[CLI 第一次使用練習](#cli-practice)確認可用。

<a id="cli-update-select"></a>

### 4.1 選擇更新方式

| 原安裝來源或情況 | 直接前往 |
| --- | --- |
| 官方 Windows 獨立安裝程式 | [Windows CLI 更新](#cli-update-windows) |
| 官方 macOS 獨立安裝程式 | [macOS CLI 更新](#cli-update-macos) |
| npm | [npm 更新](#cli-update-npm) |
| Homebrew | [Homebrew 更新](#cli-update-homebrew) |
| 支援自我更新的發行版本 | [codex update](#cli-update-self) |
| 不確定實際執行的是哪一份 CLI | [檢查命令來源](#troubleshoot-path) |

**完成後：** 統一進行[CLI 更新後檢查](#cli-update-verify)。

<a id="cli-update-windows"></a>

### 4.2 Windows：更新獨立安裝版 CLI

**適用環境：** Windows PowerShell 5.1 或 PowerShell 7.0 以上版本。

重新執行同一個安裝腳本即可更新。依 PowerShell 版本**擇一**執行：

**Windows PowerShell 5.1：**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

**PowerShell 7.0 以上版本，需已安裝且可執行 `pwsh`：**

```powershell
pwsh -NoProfile -ExecutionPolicy Bypass -Command "irm https://chatgpt.com/codex/install.ps1 | iex"
```

完成後重新開啟原本使用的 PowerShell 版本，再執行 `codex --version`。PowerShell 7 的版本確認、參數及找不到 `pwsh` 的處理方式見[Windows CLI 安裝](#cli-install-windows)。

**成功判斷：** [CLI 更新後檢查](#cli-update-verify)。

**失敗時：** [npm 與更新指令報錯](#troubleshoot-update)或[檢查命令來源](#troubleshoot-path)。

<a id="cli-update-macos"></a>

### 4.3 macOS：更新獨立安裝版 CLI

**適用環境：** macOS 終端機。

依官網 macOS/Linux 分頁，重新執行同一個安裝腳本即可更新：

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

完成後重新開啟終端機，再檢查版本。

**成功判斷：** [CLI 更新後檢查](#cli-update-verify)。

**失敗時：** [npm 與更新指令報錯](#troubleshoot-update)或[檢查命令來源](#troubleshoot-path)。

<a id="cli-update-npm"></a>

### 4.4 使用 npm 更新 CLI

**適用環境：** Windows 或 macOS，原本透過 npm 安裝。

使用官網 npm 分頁列出的更新指令：

```text
npm install -g @openai/codex
codex --version
```

**成功判斷：** [CLI 更新後檢查](#cli-update-verify)。

**失敗時：** [npm 與更新指令報錯](#troubleshoot-update)或[檢查命令來源](#troubleshoot-path)。

<a id="cli-update-homebrew"></a>

### 4.5 使用 Homebrew 更新 CLI

**適用環境：** macOS，原本透過 Homebrew 安裝。

先更新 Homebrew 的套件資料，再執行官網 Homebrew 分頁列出的升級指令：

```bash
brew update
brew upgrade --cask codex
codex --version
```

**成功判斷：** [CLI 更新後檢查](#cli-update-verify)。

**失敗時：** [npm 與更新指令報錯](#troubleshoot-update)或[檢查命令來源](#troubleshoot-path)。

<a id="cli-update-self"></a>

### 4.6 選用：使用 codex update 自我更新

[官方 CLI 指令參考](https://learn.chatgpt.com/docs/cli/reference#codex-update)另列有以下指令，適用於**支援自我更新的已安裝發行版本**：

```text
codex update
codex --version
```

這會檢查並套用 CLI 更新，不是只有查詢版本。若顯示不支援、找不到子命令或要求改用安裝工具，依訊息回到上方原安裝方式更新。不要假設每種來源與舊版本都支援此指令。

**成功判斷：** [CLI 更新後檢查](#cli-update-verify)。

**失敗時：** [選擇原安裝管道更新](#cli-update-select)。

<a id="cli-update-verify"></a>

### 4.7 CLI 更新後檢查

**更新成功的判斷**：更新過程沒有失敗訊息，更新後版本符合工具回報，且登入及基本練習正常。若原本已是該管道最新版本，版本號可以維持不變。`codex --version` 只顯示本機版本，本身不會上網檢查是否最新。

確認登入及基本功能的操作，見[CLI 登入](#cli-login)與[第一次使用練習](#cli-practice)。

<a id="troubleshooting"></a>

## 5. 疑難排解

以下為本手冊建議的初步排查順序，未逐項實測所有環境。

| 遇到的情況 | 直接前往 |
| --- | --- |
| 找不到 codex、更新後仍是舊版本、多個安裝位置 | [命令與 PATH 檢查](#troubleshoot-path) |
| npm 執行原則、更新權限或網路錯誤 | [npm 與更新排錯](#troubleshoot-update) |
| CLI 瀏覽器登入無法完成 | [登入排錯](#troubleshoot-login) |
| 桌面版安裝、帳號、組織政策或產品名稱問題 | [桌面版與其他問題](#troubleshoot-desktop) |

<a id="troubleshoot-path"></a>

### 5.1 找不到 codex，或更新後仍是舊版本

1. 先確認安裝或更新過程沒有錯誤，完全關閉舊終端機，再開新的視窗。
2. 檢查目前實際執行哪一份 CLI。

Windows PowerShell：

```powershell
Get-Command codex -All -ErrorAction SilentlyContinue | Select-Object CommandType, Source
```

macOS 終端機：

```bash
type -a codex
```

**成功判斷：** 顯示命令來源。如果出現多個安裝目錄，可能同時裝了不同管道。先核對來源及原安裝方式，再更新相符的那份 CLI，不要直接刪除不熟悉的檔案。

3. 若使用官方獨立安裝程式，可用完整路徑檢查。以下為未自訂安裝位置時的預設值，依[官方環境變數文件](https://learn.chatgpt.com/docs/config-file/environment-variables)。

Windows PowerShell：

```powershell
& "$env:LOCALAPPDATA\Programs\OpenAI\Codex\bin\codex.exe" --version
```

macOS 終端機：

```bash
"$HOME/.local/bin/codex" --version
```

如果完整路徑可以顯示版本，單獨輸入 `codex` 卻找不到，表示終端機的 **PATH 命令搜尋路徑**尚未包含該位置。依安裝程式顯示的路徑設定提示完成後重新開啟終端機。若完整路徑也不存在，或安裝時自訂過目錄，回頭確認安裝結果與實際位置。npm 與 Homebrew 安裝者不要套用上述預設路徑。

<a id="troubleshoot-update"></a>

### 5.2 npm 與更新指令報錯

| 問題 | 建議處理 |
| --- | --- |
| `node` 或 `npm` 找不到 | 目前尚未有可用的 Node.js／npm 環境，初次安裝可改走[Windows CLI 安裝](#cli-install-windows)或 [macOS CLI 安裝](#cli-install-macos)的獨立安裝程式。 |
| Windows 顯示 `npm.ps1` 因執行原則無法載入 | 若 Node.js 安裝附有 `npm.cmd`，可用下方指令呼叫它。這不需要永久放寬 PowerShell 執行原則。 |
| 更新出現權限不足、網路或憑證錯誤 | 停止後續步驟，記下錯誤及原安裝方式，確認組織政策或網路設定。更新失敗時不要將版本檢查成功當成更新成功。 |
| `codex update` 顯示不支援或未知子命令 | 使用[CLI 更新方式選擇](#cli-update-select)列出的原安裝管道更新指令。 |
| Homebrew 顯示已是最新版本 | 沒有可升級版本時可維持原版本，仍做版本與基本功能檢查。 |

Windows 若是 `npm.ps1` 的執行原則問題，先檢查 `npm.cmd` 是否可用，再依需要安裝或更新：

```powershell
npm.cmd --version
npm.cmd install -g @openai/codex
codex --version
```

<a id="troubleshoot-login"></a>

### 5.3 CLI 瀏覽器登入沒有完成

先重新執行 `codex login`，完成瀏覽器驗證後回到終端機，再執行 `codex login status`。

若瀏覽器回傳登入結果受阻，可參考官網提供的裝置代碼登入方式：

```text
codex login --device-auth
```

此方式在官方文件標為 **Beta**，個人帳號須在 ChatGPT 安全設定啟用，組織帳號可能需要管理員開啟權限。依終端機顯示的網址登入並輸入一次性代碼，完成後再查登入狀態。參見[官方裝置代碼登入說明](https://learn.chatgpt.com/docs/auth#preferred-device-code-authentication-beta)。

<a id="troubleshoot-desktop"></a>

### 5.4 桌面版與其他問題

| 問題 | 建議處理 |
| --- | --- |
| 下載頁顯示 ChatGPT，舊教學寫 Codex | 核對[產品名稱與文件沿革](#product-background)，沿官方入口下載，登入後選 Codex。 |
| 公司電腦禁止安裝或更新 | 記下完整錯誤訊息，交由管理員確認部署方式及更新政策。 |
| 更新後畫面沒有改變 | 完全結束再開啟，核對實際安裝版本、帳號與工作區，再確認該功能的官方條件。 |
| 登入後無法使用 Codex | 確認帳號、工作區與錯誤訊息，不要只靠重裝判定原因。 |
| 已裝桌面版但終端機沒有 `codex` | 前往[CLI 首次安裝](#cli-install)確認是否另行安裝 CLI，不以桌面版可以啟動判定 CLI 已安裝。 |

遇到仍無法排除的問題，記錄作業系統、安裝方式、版本、操作步驟及錯誤訊息。對外提供資料前，先移除帳號識別資料、金鑰及敏感路徑。

<a id="references"></a>

## 6. 來源與驗證範圍

本章保留產品名稱背景、官方來源、查證方式與驗證限制，方便後續維護。

<a id="product-background"></a>

### 6.1 產品名稱與文件沿革

官方於 2026-07-09 宣布 Codex 納入 macOS 與 Windows 的 ChatGPT 桌面程式，既有使用者可照常更新。參見[官方更新紀錄](https://learn.chatgpt.com/docs/changelog)。

截至查證日，原 Codex Windows 文件已轉向 **ChatGPT desktop app for Windows**。新版官方流程是安裝 ChatGPT 桌面程式，登入後從選單選擇 **Codex**。若既有程式仍顯示 Codex 名稱，先確認安裝來源與版本，再依對應更新入口操作。參見 [Windows 官方說明](https://learn.chatgpt.com/docs/windows/windows-app)及[官方快速入門](https://learn.chatgpt.com/docs/quickstart)。

<a id="source-list"></a>

### 6.2 官方來源

下列產品文件來源為 OpenAI，PowerShell 啟動方式另參考 Microsoft Learn，查證日期均為 **2026-10-15**。本文為自行整理的操作說明，非官方原文全文翻譯。

| 官方來源 | 用途 |
| --- | --- |
| [ChatGPT desktop app for Windows](https://learn.chatgpt.com/docs/windows/windows-app) | Windows 下載入口與 winget 安裝指令。 |
| [Quickstart](https://learn.chatgpt.com/docs/quickstart) | 登入、開啟資料夾及選擇 Codex。 |
| [ChatGPT desktop app](https://learn.chatgpt.com/docs/app) | macOS 下載入口與桌面程式基本流程。 |
| [ChatGPT & Codex changelog](https://learn.chatgpt.com/docs/changelog) | 2026-07-09 Codex 納入 ChatGPT 桌面程式的公告。 |
| [Deploy the Windows app](https://learn.chatgpt.com/docs/enterprise/windows-deployment) | 使用者安裝及企業部署方式。 |
| [Manage app updates](https://learn.chatgpt.com/docs/enterprise/manage-app-updates) | 自動更新、手動更新入口與組織管理限制。 |
| [Codex CLI](https://learn.chatgpt.com/docs/codex/cli) | 已逐一切換四個安裝分頁，核對 Windows、macOS/Linux、npm、Homebrew 的安裝及更新指令。 |
| [Command line options](https://learn.chatgpt.com/docs/cli/reference) | `codex update` 的適用限制、CLI 退出方式。 |
| [Authentication](https://learn.chatgpt.com/docs/auth) | ChatGPT 登入、登入狀態、裝置代碼登入及 API key 計費差異。 |
| [Environment variables](https://learn.chatgpt.com/docs/config-file/environment-variables) | 官方獨立安裝程式的預設命令位置。 |
| [Microsoft Learn：about_Pwsh](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_pwsh) | PowerShell 7 的 `pwsh` 啟動方式，以及 `-NoProfile`、`-ExecutionPolicy`、`-Command` 參數。 |
| [Microsoft Learn：Getting Started with PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/learn/ps101/01-getting-started) | Windows PowerShell 5.1 與 PowerShell 7 並存及版本辨識。 |

<a id="validation"></a>

### 6.3 查證與實測範圍

本手冊依 OpenAI 官方文件整理。安裝、登入與更新流程尚未在全新環境逐步實測。介面名稱、安裝需求與可用功能可能隨版本或帳號而變動，操作時以官方頁面及實際畫面為準。

前次查證已核對官網安裝分頁，並在現有 Windows CLI 檢查版本、一般說明、更新子命令說明及登入子命令說明。這些是文件與命令介面的檢查，本次未執行安裝、更新、重新登入或 macOS 實機測試。[疑難排解](#troubleshooting)的一般排錯步驟為本手冊整理的操作建議。

PowerShell 7 寫法已依 Microsoft 參數文件及語法檢查核對，未逐一實測所有 PowerShell 7.x 版本的安裝與更新結果。

本次 1.3 版調整閱讀結構、版型與章節連結，沒有重新查證產品資訊或執行安裝、更新。

<a id="maintenance"></a>

### 6.4 後續維護

後續若下載入口、產品名稱、更新方式或指令改變，應先重新查證相關來源，再更新對應章節及查證日期。實測結果應另註明環境與測試日期，與文件查證區分。

[返回快速導覽](#start) · [返回操作手冊索引](README.md) · [返回 KnowledgeHub](../../README.md)
