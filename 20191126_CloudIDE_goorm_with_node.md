## CloudIDEのgoormを使ってnode環境をいじってみる。

### 個人的なメモです。

#### 前提条件
- CloudIDEを試す一環としてhttps://ide.goorm.io/ を使ってみる。
- 程よい、リポジトリをforkしてお試しする。
- あまり真面に、nodeや最近のWeb開発ワークフローを体験したことはない。


### 準備
- ABAさんのkackacのリポジトリ https://github.com/abagames/kackac をforkしておく。
- goormIDEのアカウントの作成

どちらかというと、kackacを見たことと、CodeAnywareの無料プランでコンテナを起動できなくなったことが、
動機の一つ。
OracleCloudのフリーティアも検討したが、node環境は大変なイメージもあるので
今回は、CloudIDEを試したく。この記事の時点 2019/11/26時点では、フリープランは次のような条件で提供される。  

goormIDEのフリープラン（詳しくは本家を参照のこと）
- 10GBのDISK
- 5個までのコンテナ作成
- 1個までのコンテナ実行
- 常時起動コンテナは無し

### コンテナ作成と実行手順

- リージョン（どちらでもよい）リージョンは記事時点で、オレゴン（アメリカ）とソウル（韓国）の2箇所。
- Privateコンテナ (Publicの指定もできる。その際は、コンテナギャラリーに公開されるらしい。）
- テンプレート:github
  - gamix255/kackacを選択 (コンテナの名前と説明が勝手に入る。)
- 配備(おそらくDeploy)
  - 使用されていない を選択
- ソフトウェアスタック:Node.js
  - 種類:Node.jsプロジェクト
  - OS:Ubuntu 18.04.LTS (Node10.16.3、Polymer1.9.11になる。)

上記の内容で作成する、を選択すると、10秒未満でコンテナが作成され、
コンテナの実行、を選択すると、10秒未満でコンテナが実行された。

### npm install
package.jsonがあるため、npm installから先に進める。  
#結構未知の領域のため間違ったことを書いているかも。
```
npm install
```
そして、npm runで出力を見てみたところ、開発用サーバの起動とビルドがある
```
# npm run
Scripts available in kackac via `npm run-script`:
  watch_games
    light-server -s docs -w "docs/**/* # # reload"
  watch_lib
    rollup -c -w
  build_lib_typings
    tsc --declaration --emitDeclarationOnly --target es2015 --module commonjs --outFile tmp/_bundle.d.ts src/main.ts
```


### 実行とポートフォワード（公開）
rollupは次の手順
```
#npm run watch_lib 
```
そして、開発用サーバは、次のように起動する。
```
root@goorm:/workspace/kackac3(master)# npm run watch_games

> kackac@1.0.0 watch_games /workspace/kackac3
> light-server -s docs -w "docs/**/* # # reload"

light-server is listening at http://0.0.0.0:4000
  serving static dir: docs

light-server is watching these files: docs/**/*
  when file changes,
  this event will be sent to browser: reload

```

プロジェクト→実行URLとポートで、自分専用のURLが発行されている。  
デフォルトでは3000番にポートフォワードされている。  
（Expressのデフォルト値のみたい。）、light-serverを変更するのではなく、ここ
にTCP4000宛ということで、新規のサブドメインを登録するとすぐに、外部から閲覧が可能になった。


### 感想
- rollup やnpm等、自分の日常で使わない概念が多いけれど、躓きながら、開発環境構築までは
一応終わった。
- goormIDEはPCのChromeから使った。概ね快適だった。
- この記事を書くために4回ぐらい、コンテナを壊して作り直したけれど、
合わせて1時間程度の所要時間。
- CPU使用率等、リソースが表示されているのが、goormideのチャームポイントと思う。

### 参考ページ
- rollupについて参照した。実際には前述の手順で行ったため、参考にしたのみ
　https://qiita.com/cognitom/items/e3ac0da00241f427dad6
- npmについて参照した。
 https://qiita.com/hashrock/items/15f4a4961183cfbb2658
