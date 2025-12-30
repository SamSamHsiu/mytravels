沒問題！既然你有 VS Code，我們就用最「工程師正規軍」但又不會太難的方式來做。

這是一套 **Windows + VS Code + Hugo** 的完整教學。為了讓你容易成功，我們採用**「Stack」**這個主題，它的介面是卡片式的，非常適合放旅遊照片加文字。

---

### 第一步：環境準備 (如果你還沒裝)

請打開 VS Code，按下 `Ctrl + ~` (鍵盤左上角那個波浪鍵) 打開終端機 (Terminal)。

1.  **檢查有沒有 Git**：
    輸入 `git --version`
    *   如果有出現版本號 -> 繼續。
    *   如果出現錯誤 -> 去 [git-scm.com](https://git-scm.com/downloads) 下載並安裝 (一直按 Next 即可)。

2.  **安裝 Hugo (使用 Winget 指令最快)**：
    在 VS Code 終端機輸入：
    ```powershell
    winget install Hugo.Hugo.Extended
    ```
    *(一定要裝 Extended 版本，這樣圖片處理功能才夠強)*
    *安裝完後，建議重開機或重開 VS Code，確保指令生效。*

---

### 第二步：建立你的網站骨架

假設我們要建立一個叫做 `mytravels` 的資料夾。

1.  **建立網站**：
    在終端機輸入：
    ```bash
    hugo new site mytravels
    ```
2.  **進入資料夾**：
    ```bash
    cd mytravels
    ```
3.  **用 VS Code 開啟這個資料夾**：
    輸入 `code .` (注意 code 後面有一個點)
    *這時候 VS Code 會重新開啟，左邊檔案總管就是你的網站檔案了。*

---

### 第三步：安裝主題 (Congo 或 Stack)

為了展示照片，我們選一個現代化、卡片風格的主題，這裡推薦 **Stack**。

1.  **初始化 Git (重要)**：
    在新的 VS Code 終端機輸入：
    ```bash
    git init
    ```
2.  **下載主題**：
    ```bash
    git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
    ```
3.  **設定設定檔**：
    *   在左側檔案列表找到 `hugo.toml`。
    *   把裡面的內容全部刪掉，貼上以下最基本的設定 (記得改你的名字)：

```toml
baseURL = 'https://你的帳號.github.io/mytravels/' # 先暫時這樣填
languageCode = 'zh-tw'
title = '我的旅遊日記'
theme = 'hugo-theme-stack'

[params]
    # 你的名字
    author = "你的名字"
    # 側邊欄的介紹
    sidebar = { avatar = "avatar.jpg", subtitle = "愛旅遊的工程師" }

[menu]
    [[menu.main]]
        identifier = "home"
        name = "首頁"
        url = "/"
        weight = 1
```

---

### 第四步：寫第一篇遊記 (這才是重點！)

Hugo 有一個很棒的功能叫 **Page Bundles (頁面同捆)**，這對旅遊相簿超重要！意思是「一篇文章一個資料夾，照片直接丟裡面」，不用擔心檔名重複。

1.  **建立文章資料夾**：
    在左側 `content` 資料夾上面按右鍵 -> `New Folder` -> 命名為 `post`。
    在 `post` 裡面再建一個資料夾 -> 命名為 `2024-tokyo` (你的旅遊代號)。

2.  **放入照片**：
    把你的幾張東京照片，直接拖拉進 `content/post/2024-tokyo/` 資料夾裡。
    *(假設有一張封面圖叫 cover.jpg，還有一張風景照叫 view.jpg)*

3.  **建立文章檔案**：
    在 `content/post/2024-tokyo/` 裡面按右鍵 -> `New File` -> 命名為 `index.md` (一定要叫 index.md)。

4.  **寫內容**：
    打開 `index.md`，貼上以下內容：

```markdown
---
title: "東京五日遊：淺草寺大冒險"
date: 2025-01-30
description: "這是我第一次去東京，天氣超級好！"
image: "cover.jpg"  # 這裡直接打檔名，它會自己抓同資料夾的照片
---

這是我的第一篇遊記！

## 第一站：雷門
人超級多，但是燈籠真的很壯觀。

![雷門風景](view.jpg) 
<!-- 這裡也是直接打檔名即可，不用寫很長的網址 -->

我覺得這裡的氛圍... (繼續寫你的遊記)
```

---

### 第五步：本機預覽 (看看長怎樣)

在終端機輸入：
```bash
hugo server
```
它會跑出一行網址，通常是 `http://localhost:1313/`。
按住 `Ctrl` 點擊那個網址，瀏覽器就會打開。你應該會看到一個漂亮的卡片式網站，裡面有你的東京遊記！

*(如果不滿意，隨時改 VS Code 裡的字，網頁會自動更新，不用重整)*

---

### 第六步：上傳到 GitHub (讓全世界看到)

這是最簡單的「Docs 資料夾大法」，不需要設定複雜的自動化流程。

1.  **停止預覽**：在終端機按 `Ctrl + C`。

2.  **修改設定檔 (關鍵一步)**：
    打開 `hugo.toml`，在最上面加一行：
    ```toml
    publishDir = "docs"
    ```
    *這告訴 Hugo：等等把做好的網站放在 docs 資料夾裡。*

3.  **生成網站**：
    在終端機輸入：
    ```bash
    hugo
    ```
    *(你會發現左邊多了一個 `docs` 資料夾)*

4.  **上傳到 GitHub**：
    去 GitHub 建立一個新的 Repository (例如叫 `mytravels`)。
    然後在 VS Code 終端機依序輸入 (把網址換成你的)：

    ```bash
    git add .
    git commit -m "我的第一次上傳"
    git branch -M main
    git remote add origin https://github.com/你的帳號/mytravels.git
    git push -u origin main
    ```

5.  **開啟 GitHub Pages**：
    *   回到 GitHub 網頁 -> 進入你的 Repository。
    *   點 `Settings` -> 左邊點 `Pages`。
    *   **Build and deployment** -> Source 選 `Deploy from a branch`。
    *   **Branch** 選 `main`，**Folder (重點)** 選 `/docs` (不要選 root)。
    *   按 Save。

等個 1 分鐘，重新整理頁面，GitHub 就會給你這個網站的網址了！

### 之後要新增遊記怎麼辦？
1. 在 `content/post` 建新資料夾 (如 `2025-kyoto`)。
2. 丟照片進去，建 `index.md` 寫字。
3. 終端機跑 `hugo` (生成)。
4. 終端機跑 `git add .` -> `git commit -m "new post"` -> `git push`。
5. 結束！網站自動更新。