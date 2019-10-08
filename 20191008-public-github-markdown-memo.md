## 日記的なものや作成例などの記事をgithub（等）の機能で編集、公開（しようと）した際の記録

### 個人的なメモです。いろいろ微妙かも

#### 前提条件
- スマホやPCから直接Webで書き込んでみている。git push origin masterとかしているわけではない。
- 適当にアドホックにやってみている。最適か否かはかなり怪しい。
- README.mdのように記事を公開してみようと思った。
- 実はファイルを引用したいが、結果としてあまりうまくいっているとはいいがたい。

これまでのストーリー  
手書きHTMLで生活してきたけれど、より簡単に短時間に書き込みたい。凝ったことはあんまりしたくない、
githubのREADME.mdのみのリポジトリとかも見ることが多くなったし、そんな感じでやってみている記録。

### 試したこと
- githubに直接mdを置いてみてみている。<br>例 https://github.com/gamix255/casual-text-public/blob/master/20190916-ATmega328P-with-ArduinoIDE-in-2019.md 
- github pages 経由で公開してみる。<br>
  例：https://gamix255.github.io/casual-text-public/20190916-ATmega328P-with-ArduinoIDE-in-2019.html
- 相対パスリンク
  例：[上記の文書へのリンク](/20190916-ATmega328P-with-ArduinoIDE-in-2019.md)
- ほかのファイルのインクルード（試行錯誤中）<br>
<details>
<summary> インクルードに関しての試行錯誤（JavaScriptでgist-it編）
 </summary>
<p>
https://gamix255.github.io/casual-text-public/20191008-public-github-markdown-memo の方では見えますが、
XSS防止の観点で https://github.com/gamix255/casual-text-public/blob/master/20191008-public-github-markdown-memo.md の方では表示ができません。
<script src="https://gist-it.appspot.com/https://github.com/gamix255/t/blob/master/t"></script>


</p>
</details>




### 宿題（気になること）
後で


参考
- 後で書く
