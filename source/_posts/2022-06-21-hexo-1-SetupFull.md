---
title: Hexo + GitHub Pages 架設個人網誌-完整版-1
date: 2022-06-21 20:34:18
tags:
- Hexo
categories:
- Hexo
---
＃ 如何使用 Hexo + GitHub Pages 架設個人網誌

## 什麼是 Hexo？
- HEXO 是一套`Static Site Generators(SSG)`網誌框架工具，只要把建立和編寫`markdown`就可以變成轉成靜態網頁。一般都用在架自己的部捼洛客，不用花很多時間設計排版等等。目前最有名的SSG有包括: **Hexo(node.js語言)**，**HUGO(go語言)**，**Jekyll(ruby語言)** 等等。
- 其實就是一個基於 `Node.js` 開發的網誌框架。具有下列幾項**特點**：
    - NODE.JS
    - 能夠支援 **Markdown** 語法解析文章，並透過主題渲染靜態檔案
    - 具有豐富的**外掛套件**
    - 支援一鍵部署到 **GitHub Pages** 或 **Heroku** 等支援靜態網頁的空間

## 前置作業
### 安裝需要工具
在開始安裝 Hexo 之前，必須先在電腦安裝下列工具: 

- #### [Node.js](https://nodejs.org/en/): npm 來安裝所需的套件。你可以把npm當作是linux的 `apt` 或`yum`。他主要是幫我們安裝JS等套件。
> - Linux (Ubuntu, Debian)：
>> `sudo apt-get install -y nodejs`

- #### [git](https://git-scm.com/): 是專們做版本控制的工具。外面有多版本控制，我選用github，因為他比較多人用，還有他有GitHub Page可以幫我們架設網站，又是免費。window 可以用這個git-bash 來下載[git-for-window](https://gitforwindows.org/)
    > - Linux (Ubuntu, Debian)：
    >> `$ sudo apt-get install git-core`

    > - Linux (Fedora, Red Hat, CentOS)
    >> `sudo yum install git-core`

    > mac 安裝:
    >> `brew install git`     

## Hexo 環境建置 
### Ste 1. 安裝 Hexo
- 安裝 hexo
開啟 CLI/Terminal 介面（例如 cmd `git-bash` 等終端機），並輸入下列指令安裝 Hexo：
    > `npm install hexo-cli -g`
	> `npm install`
- 檢查有安裝成功
安裝完後，查看 Hexo 版本，確認是否有安裝成功，可輸入:
    > `hexo version` 
    或 
    > `hexo -v` 

### Step 2. 初始化 Hexo
其實HEXO初始化，其實就是去github的`hexojs/hexo-starter` clone下來到你的目錄。Hexo初始化，有兩種做法:
- 方法1
可以先建立資料夾名稱，然後`cd`進去資料夾，再下`hexo init`初始化，如下:
    ```
    #1. create directory
    mkdir hexotest
    #2. go to hexotest directory
    cd hexotest
    #3 hexo inital 
    hexo init
    ```
- 方法2
我們可以指定我們資料夾名稱，在 init 後面如:
    > `hexo init <資料夾名稱>`
### Step 3. 在資料夾安裝所需檔案

上一步我們已經下`hexo init`，如果失敗，說明有些套件沒有，所以請下列指來安裝`npm 套件`
> `$ npm install`

安裝完成後，資料夾會看到下方這些檔案和資料夾:
- 架構:
```
.
├── _config.landscape.yml
├── _config.yml
├── db.json
├── package-lock.json
├── package.json
├── scaffolds
│   ├── draft.md
│   ├── page.md
│   └── post.md
├── source
│   └── _posts
│       └── hello-world.md
└── themes
```

#### _config.yml

- 有關網站配置的檔案，可修改各種配置設定。例如：網站標題、網站的網址、使用主題名稱等等
- 詳細內容可以參考[官方文件](https://hexo.io/zh-tw/docs/configuration)

#### package.json
記錄所有載入的應用程式資料，也就是專案中需要的所有模組。

#### scaffolds 模板

- 當我們建立新文章時，Hexo 會根據 scaffolds 中的模板建立相對應的檔案。理面有post、page 和 draft，它會從這裡copy到source資料夾。
- 資料夾中有三種預設[佈局](https://hexo.io/zh-tw/docs/writing.html)：post、page 和 draft，分別對應：要發布的文章、頁面、草稿

#### themes 主題

- 用來存放主題的資料夾
- Hexo 會根據主題來解析 scouce 資料夾中的檔案並產生靜態頁面。預設主題為 [landscape](https://github.com/hexojs/hexo-theme-landscape)

#### source 資源

- 主要用來存放我們寫的文章，頁面地方，一般都是，例如檔 Markdown 、圖片、各種頁面（分頁、關於等）。
- 以 `_` 開頭的檔案、資料夾或隱藏檔案會被忽略，除了 `_posts` 資料夾以外
- 我們可以從重新立名用我們文章用日期來取名，這樣才好認。
- Markdown 檔和 HTML 檔會被解析，並放到 public 資料夾，而其他檔案則會被拷貝過去

#### source & public & .deploy_git 的差別
- 執行 `$ hexo generate`或 `hexo g` 之後，會把 source理資料夾中的Markdown檔和HTML 檔進行解析，再結合主題進行渲染，生成我們看到的靜態網站，也就是會產生在public資料夾
- 如果你下 `hexo clean` 或 `hexo cl`，會把`public`裡面`Markdown`清掉，你再按`hexo generate`重新稱生回來。
- 執行 `$ hexo deploy` 之後，則會將 `public` 文件夾中的內容部署到 GitHub，並生成 `.deploy_git` 資料夾，因此內容與 `public` 幾乎相同
- 這三者的關係可想成：
    > source -> public -> .deploy_git
- 你可以這樣想PUBLIC當案就是你網頁會顯示出來。只要你source資料還在，都可以再把它產生回來。
    - 產生`MD` -> HTML到PUBLIC: `hexo generate` or `hexo g`
    - public 推上github: `hexo deploy` or `hexo d`

## 常用指令
Hexo 會用到一些指令，更多詳細指令可參考[官方文件](https://hexo.io/zh-tw/docs/commands)。
### 1. new 新增文章post and page: `hexo new` 
> **建立文章Post**
>> `hexo new \[layout] \<title>`
>> or
>> `hexo new \<title>`

> **建立頁面Pages**
>> `hexo new post \<title>`
- 你也可以去`scaffolds`資料夾複製posts or page 到 `/source/_posts/title.md`
- 如果沒有設定 `layout`，則會使用 `_config.yml` 中的 `default_layout` 來設定
- 檔案名稱盡量以英文命名，避免出現亂碼，也可以用中文。

### 2. clean 清除靜態檔案與快取
> `hexo clean`
- 在每次儲存修正後的檔案之前，會建議先輸入此指令，清除快取檔案 （db.json）和已產生的靜態檔案（public），public裡面Markdown清掉。
- 你再按`hexo generate` 靜態檔案（public）會重新產生回來。

### 3. generate 產生靜態檔案
> `hexo generate`
> 或
>`hexo g`
- 重新產生靜態檔案，把source理的Markdown檔進行解析並放到 public 資料夾。
- 只要你有修改你的MD檔案一定要下這個指令，不然他不會轉成靜態檔案，就無法在網頁顯示出來。

### 4. server 啟動伺服器
- 在本地端啟動 Hexo 伺服器，預設路徑為：`http://localhost:4000/`
> 啟動server ，預設port 為4000
>>  `hexo server`

這時候你你就可以去瀏覽器打開: http://localhost:4000 就是你架設HEXO的首頁。

- 停止server，按 `Ctrl + C` 即可關閉
- 手動換其他port，如果port 4000被用掉
> `$ npm -s -p:xxx ` #xxx是你要的port

#### <font color="red"> 補充:</font>
- 如果你產生完靜態網頁(`hexo -g`)，可以去單獨把PUBLIC資料夾放在server，就可以看到預覽結果。
- 你可以`停掉hexo server`服務，用`ctrl+c`。如果用VSCODE可以用CODE LIVE套件，就會顯示預覽設定結果。

## 部署到 GitHub

### 建立 GitHub 專案
在架設網誌之前，還必須準備一個存放網站的空間，例如架設主機，或是選擇現有的平台，例如 `GitHub Pages` 或 `Heroku` 等，本篇以 GitHub 作為範例。

#### Step1. 註冊 [GitHub](https://github.com/) 帳號並登入
#### Step2. 點選 `New` 新增一個 Repository（專案）
#### Step3. 將專案名稱命名為 `username.github.io`，username 記得改成自己的帳號名稱
這樣就成功建立了一個網域：`username.github.io`
<font color="red"> 補充:</font>
- 網域username（`username.github.io`），只能用一次。- 也就是說如果你已經用掉你就無法用。
- 網域username用掉我們可以在後面加其他名字。Example: `username.github.io/projectname`


### 將檔案發布到 GitHub
#### Step1. 安裝 Git 相關套件

回到 hexo 資料夾，在終端機輸入下列指令安裝部署所需套件：

```
$ npm install hexo-deployer-git --save
```
等下後面會介紹一個自動幫我們發布到 GitHub指令(`hexo d`)，但是上面這個指令要先設，不然沒法用。

#### Step2. 修改 _config.yml 檔案的 Deployment 設定
1. deploy git 設定
接著是修改 `_config.yml` 設定檔中，有關 deploy 的設定。
需注意這裡指的 `_config.yml` 檔案是**根目錄**的，不是 themes主題中的。下面是管網推薦。
```
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
```

- `type`：選擇部屬模式，這裡填 git
- `repo`：GitHub repository 的連結，記得將 username 修改成自己的帳號名稱
- `branch`：選擇分支，預設為 main，可以改任何分支都可以

<font color="red"> **補充1:**</font> 
- `branch` 可以選`main` 或`gh-pages`分支(就是github page)。
- 我的`master`或`main`是放hexo主程式，另一個branch 就會放hexo 產生出來的靜態網站也就是`public資料夾`內容。
- 你可以不用跟我一樣，如果可以直接用hexo 產生出來的靜態網站放進`main` or `master` 好。
- branch 就是他會幫你自動push到github 上面，只要下`hexo d` 就是deploy即可。

下面是我的設定。
```html=
deploy:
  type: git
  repo: https://github.com/chenchih/hexo-demo2022.git
  branch: gh-pages 
  #branch: main
```
下面是我github page設定，你們可以到`settings>pages`來看也沒也enable。如果你們跟我一樣請選擇你們網頁要放在哪一個branch。以我的例子，
- `gh-page`: 放我的網頁
- `main`: 放hexo主要程式，我可以在任何電腦寫文章和部屬到github
![](https://i.imgur.com/CkjGm0e.png)

<font color="blue"> **補充2:**</font> 
1. 我在還沒部署之前我會先把我的hexo主程式發布在github main branch，用以下指令 **(如果你們只有想部屬你們網頁請跳過此步)**
2. hexo 推到github 上，你會發現public資料夾不會被推上去，因為`.gitignore` 有放`public`。`Public`就是放我們靜態網頁。

    ```html
    #step1 進去hexo專案，我們現在應該都在hexo資料夾
    $cd hexo_project
    # step2 git 初始化，把此資料架進行版本控制
    git init 
    #step 3 推進github
    git remote add origin https://github.com/chenchih/hexotest.git
    git branch -M main
    git push -u origin main
    ```

2. 我們還需要改此設定，不然github page網頁會顯有問題。請到 `_config.yml`找`# URL`
```
url: https://github.com/username/
permalink: :year/:month/:day/:title/
root: /
```
- 如果你的**網域名稱或網頁**是 `username.github.io` ，請用**上面些改**你的url就好
- 如果你的**網域名稱** `username.github.io/repository-name`，請修改root設定
以我的例子我的網域名稱是:`chenchih.github.io/hexo-demo2022/`我就會改成
```
url: https://github.com/chenchih/
permalink: :year/:month/:day/:title/
root: /hexo-demo2022
```

#### Step3. 輸入部署指令
上面設定有成功，我們現在就可以開始做部署指令
使用下列指令即可部署檔案到網站上，在STEP1如果沒下那指令（`hexo-deployer-git`）就無法用下面指令。
> `$ hexo deploy`
> or或縮寫的方式
> `$ hexo d`

- 正常我們流程順序是這樣:
```
$ hexo cl    // 清除之前建立的靜態檔案 git clean
$ hexo g     // 建立靜態頁面  git generate
$ hexo d     // 部署至 GitHub deploy
```

或是合併第二、三行指令：`hexo g -d` 即可在產生靜態頁面後立刻部署。
這樣就完成部署網誌到 GitHub 了！可在個人頁面 `https://username.github.io` 確認是否有發布成功


## 總結
我來做 一個總結，我寫的很多，如果你不想看，我這裡會做一個整理所有指令和流程。我會再寫關於加一些plugin，換主體等等內容。

### step 
1. 下載hexo相關東西，如 `node.js`, `git`, `hexo-cli` 等套件
2. 初始化 Hexo 專案 `hexo init` 或 `hexo init <projectName>`
3. 進資料家安裝 npm 套件管理 `npm install` 順便說一下npm其他指令
- 列出所有安裝的套件: `npm list`
- 移除套件: `npm remove <packagename>` 或 `npm uninstall <packagename>`
- 安裝套件: `npm install <packagename>`
4. 啟動server `hexo s` or `hexo server` 
- 啟動server比較好看你網頁狀態或markdown有問題你可以馬上修改等等
- port預設是4000，手動換掉:`npm -s -p:xxx`
5. 建立文章: `hexo new post <namepost>` 
6. 產生網頁public資料夾: `hexo g` or `hexo generate`
7. 安裝`deploy-git`, 才能用命令部署到GitHub: `npm install hexo-deployer-git --save`
這很動要，之後就可以用`hexo deploy`就自動幫你deploy到github
8. 部屬到github相關設定
- Deployment 設定，就是可以自動幫你部屬到github
```
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: main 
```
- github page 網址網域
```
url: https://github.com/username
permalink: :year/:month/:day/:title/
root: /  
```
9. deploy to github: `hexo deploy` or `hexo d`

所以最常用指令就是下面這個
> `hexo cl`　＃清除你public資料夾 
> `hexo g`　＃重新產生資料夾
> `hexo d`　＃部屬到github

- hexo flow
![hexo flow](https://i.imgur.com/qtDiPQD.png)

- hexo deploy setting
![hexo deploy](https://i.imgur.com/0WlyXbn.png)
