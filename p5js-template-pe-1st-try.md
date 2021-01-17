## VS Code＋nodejs用の公開されているテンプレートを初めて展開するときの手順

### 個人的な作業記録です。

あまりVS Codeにもnodejsについても詳しくないため、誤りが含まれているかもしれませんが、
自分用のメモとして記載しています。以下の手順は無保証です。

- 利用する（公開されている）テンプレート
  - https://fal-works.github.io/p5js-templates/ja/
    - https://github.com/fal-works/p5js-template-pe
  - 環境や、前提となるソフトウェアのインストールの仕方
    - OS:Windows10 Pro
    - VS Code:2021年1月16日時点のものをZIPファイルからインストール（1.52.1）
    - node.js:Scoop経由でインストール 
    - git for windowsは導入済み

### Scoopのインストール(nodeのインストールに利用する。)

```PowerShell
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
```
を行った後に

```PowerShell
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```
をやっておく。ダウンロードしたものをいきなり実行したくない場合には上の通りには実行できない。

### node.jsのインストール

```PowerShell
PS C:\Users\username> scoop search node
'main' bucket:
    eventstore (20.10.0) --> includes 'EventStore.ClusterNode.exe'
    node-chakracore (10.13.0)
    nodejs-lts (14.15.4)
    nodejs (15.6.0)
    sliksvn (1.12.0) --> includes 'svn-populate-node-origins-index.exe'

PS C:\Users\username>
PS C:\Users\username> scoop install nodejs-lts
Installing '7zip' (19.00) [64bit]
7z1900-x64.msi (1.7 MB) [=====================================================================================] 100%
Checking hash of 7z1900-x64.msi ... ok.
Extracting 7z1900-x64.msi ... done.
Linking ~\scoop\apps\7zip\current => ~\scoop\apps\7zip\19.00
Creating shim for '7z'.
Creating shortcut for 7-Zip (7zFM.exe)
'7zip' (19.00) was installed successfully!
Installing 'nodejs-lts' (14.15.4) [64bit]
node-v14.15.4-win-x64.7z (16.4 MB) [==========================================================================] 100%
Checking hash of node-v14.15.4-win-x64.7z ... ok.
Extracting node-v14.15.4-win-x64.7z ... done.
Linking ~\scoop\apps\nodejs-lts\current => ~\scoop\apps\nodejs-lts\14.15.4
Persisting bin
Persisting cache
Running post-install script...
'nodejs-lts' (14.15.4) was installed successfully!
```

### VS Codeのインストール

- https://code.visualstudio.com/#alt-downloads から、対応しているアーキテクチャのzipを選択してダウンロードし任意の場所に展開。

### Templateの展開とローカルへのclone

1. `https://github.com/fal-works/p5js-template-pe`の`Use this template`を選択
2. テンプレートからの生成画面が表示される。  
リポジトリ名を入力`p5js-pe-practice`(とした)、Privateを選択した上で`Create repository from template`を選択
3. Git Bashを起動し、リポジトリをCloneして、npm install  
``` bash
$ cd your_local_repository_path # Cドライブ直下のworkなら/c/work
$ git clone https://github.com/your_account/p5js-pe-practice.git
$ cd p5js-pe-practice
$ npm install
npm notice created a lockfile as package-lock.json. You should commit this file.
added 116 packages from 67 contributors and audited 116 packages in 29.956s

13 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```
###  VS CodeのExtensionをインストール:ESlintとprettier
テンプレートの提供元の手順とVS Codeの入れ方が違うせいかうまくいかなかったのでひとまず下記の手順で導入
- VS Codeを起動し、Extension（拡張機能）のアイコンを押し、`dbaeumer.vscode-eslint`を入力してインストール
- VS Codeを起動し、Extension（拡張機能）のアイコンを押し、`esbenp.prettier-vscode`を入力してインストール
- VS CodeでCloneしたフォルダを開いて、Script.jsを編集し、View→Probrems(CTRL+SHIFT+m)を選択すると  
`ESLint is disabled since its execution has not been approved or denied yet. Use the light bulb menu to open the approval dialog.`の表示が出ているので、右クリックして承認する。

### その後。

Runメニューの`Start Debugging`や`Run Start Without Debugging`でプレビューが見られなかったため、`.VS Code/lounch.json`の設定の中のURL（ローカルホストでサーバが上がっていることになっている。）をコメントにしたうえで、`"file": "${workspaceRoot}/index.html"`を追加。（この編集を行っている途中でもLintが効いて少し感動。）  
Debugger for Chromeを入れた方が良いかもと思っている。


