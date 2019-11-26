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

### npm
後ほど書く。

### 実行とポートフォワード（公開）
後ほど書く。

### 感想
後ほど書く（けど、概ね快適だった。。）
