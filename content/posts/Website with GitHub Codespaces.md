---
title: "用github的codespace打造部落格網站"
date: 2023-11-27T10:00:00+08:00
draft: false
cover: "https://images.unsplash.com/photo-1556075798-4825dfaaf498?q=80"
tags: ["軟體技能", "github"]
categories: ["軟體技能"]
---

你要走的這條路叫做 「靜態網站 (Static Site)」。 跟之前的 WordPress（有店面、有後台）不同，這條路像是 「你自己在電腦上寫好傳單，然後請免費的工讀生（GitHub）幫你貼到佈告欄上」。

優點： 絕對免費、速度快、看起來很駭客（很酷）。

缺點： 沒有後台。你不能像發 FB 一樣打字按送出，你必須「寫程式碼檔案」來發文。

因為你說你是電腦小白，我不會教你用電腦的「命令提示字元 (CMD)」，那會讓你崩潰。我們要用 GitHub Codespaces（雲端電腦）來作弊完成這件事。

🚀 第一階段：把網站架起來 (複製別人的作品)
你提供的那個連結是「佈景主題 (Theme)」，就像是「裝潢材料包」。你不能直接 Fork 它就變成網站，你需要先蓋一個「骨架」再把裝潢包放進去。

請一步一步跟著做，不要漏掉任何一個標點符號：

步驟 1：準備倉庫 (Create Repository)
註冊並登入 GitHub。

點選右上角的 + 號，選擇 New repository。

Repository name 取名：my-dream-blog (或你喜歡的名字)。

設定為 Public (公開)。

重要： 勾選 Add a README file (這樣我們才能開啟雲端電腦)。

按下 Create repository。

步驟 2：開啟雲端駭客電腦 (GitHub Codespaces)
在你剛建立好的頁面，點選綠色的 <> Code 按鈕。

切換到 Codespaces 分頁。

點選綠色的 Create codespace on main。

這時會跳出一個像駭客電影一樣的黑底畫面，等待它跑完（會看到很多字在跑），直到你看到最下方出現可以打字的地方（終端機 Terminal）。

步驟 3：輸入魔法指令 (安裝 Hugo 與主題)
請一次複製一行下面的指令，貼到那個黑黑的視窗裡，然後按 Enter 執行：

指令 A：下載並安裝 Hugo (你的網站製造機)

Bash

wget https://github.com/gohugoio/hugo/releases/download/v0.124.1/hugo_extended_0.124.1_linux-amd64.tar.gz && tar -zxvf hugo_extended_0.124.1_linux-amd64.tar.gz && sudo mv hugo /usr/local/bin/
(解釋：這行是去網路上下載 Hugo 這個軟體並裝在這台雲端電腦裡)

指令 B：建立網站骨架

Bash

hugo new site . --force --format toml
(解釋：這行是告訴 Hugo 在這裡蓋一棟新房子)

指令 C：下載你想要的 Dream 主題

Bash

git submodule add https://github.com/g1eny0ung/hugo-theme-dream.git themes/dream
(解釋：這行是去把 g1en 的裝潢材料包抓進來)

指令 D：複製範例設定 (這步最關鍵)

Bash

cp themes/dream/exampleSite/hugo.toml . && cp -r themes/dream/exampleSite/content/* content/
(解釋：這行是把主題作者做好的「範例房間」直接搬到你家，這樣你就有現成的樣子了)

步驟 4：存檔並上傳 (Commit & Push)
現在你的雲端電腦裡已經做好網站了，我們要把它傳回 GitHub：

在左邊的選單，點選第三個圖示（長得像樹枝圖的 Source Control）。

在 "Message" 框框隨便打個字，例如 "init"。

點選藍色的 Commit 按鈕。

接著點選 Sync Changes (或 Publish Branch)。

🌐 第二階段：讓網站被看見 (串接 Vercel)
GitHub 本身雖然能放網頁，但對小白來說設定太複雜。我們用 Vercel 這個免費服務，它會自動幫你把 GitHub 的程式碼變成網站。

去 Vercel 官網 註冊，選擇 Continue with GitHub。

登入後點選 Add New ... -> Project。

你會看到你剛剛做的 my-dream-blog，點選 Import。

Framework Preset 這一欄，Vercel 通常會聰明地自動選 Hugo。如果沒有，請手動選 Hugo。

點選 Deploy (部署)。

等待約 1 分鐘，當噴彩帶的畫面出現，恭喜你！點擊圖片，你的瀑布流部落格就上線了！🎉

✍️ 第三階段：我是小白，我該如何發文？
這就是「免費」的代價。你沒有漂亮的後台輸入框，你要寫「Markdown 文件」。

發文流程：

回到你的 GitHub Repository 頁面 (網頁版)。

點選資料夾 content -> posts。

你會看到一些範例文章。點選右上角的 Add file -> Create new file。

檔案名稱： 必須以 .md 結尾，例如 my-first-trip.md。

檔案內容 (這是格式，一定要照抄)：

Markdown

---
title: "我的第一篇瀑布流文章"
date: 2023-11-27T10:00:00+08:00
draft: false
cover: "https://你的圖片網址.jpg"
tags: ["日記", "生活"]
categories: ["我的故事"]
---

這裡開始寫你的內容。
你可以直接打字。

如果要放圖片，格式是這樣：
![圖片描述](https://你的圖片網址.jpg)

這裡是第二段...
白話講解這些亂碼的用意：

--- 包起來的區塊叫做 Front Matter (前言)：這是給電腦看的。告訴電腦這篇文章的標題、時間、封面圖(Cover)是哪張。

draft: false：意思是「這不是草稿」，設為 true 網站就不會顯示。

cover：這就是瀑布流列表上顯示的那張縮圖。你必須先把圖片上傳到圖床（如 Imgur）取得網址填進來。

寫完後，按右上角的 Commit changes (綠色按鈕)，再按一次 Commit。

等待魔法發生： 你不需要做任何事，Vercel 會偵測到你更新了檔案，大約 1-2 分鐘後，你的網站就會自動更新了。

⚠️ 小白生存指南 (良心建議)
圖片是大麻煩： 這種寫法不能直接從電腦拉圖片進去。你必須先把圖片上傳到像 Imgur 這種網站，複製「圖片連結 (Direct Link)」，然後貼到你的文章裡。

不要亂動其他檔案： 除了 content/posts 裡面的東西，其他檔案（特別是 hugo.toml）沒事不要亂改，一改錯整個網站就會掛掉（白屏）。

如果覺得太難： 如果你發現這種「寫程式碼發文」的方式讓你很痛苦，請回頭考慮我之前說的 WordPress，那是用錢買方便；而這個方法，是用方便換免費。

