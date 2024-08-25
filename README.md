# vol15

Git/GitHubで共同作業をしてみましょう！

## 目標
GitHubを使って，プルリクエストを作成する

## 手順

### Gitの初期設定

Gitをインストールした後は初期設定が必要です．

```sh
git config --global user.name <あなたの名前>
git config --global user.email <@users.noreply.github.comで終わるメールアドレス>
```

`user.name`はコミットしたときに表示される名前です．出来るだけ本名は避け，特にこだわりが無ければGitHubのIDと同じにしておくとよいでしょう．

`user.email`はコミットする時に表示されるメールアドレスです．ここでは実際に使っているメールアドレスは設定せず，GitHubが発行しているメールアドレスを使用することにします．

GitHubのメールアドレスを確認するには，[設定](https://github.com/settings/emails)を開き，下の方にある`Primary email address`に記載のある`数字+ID@users.noreply.github.com`を指定します．

次に，設定しておくとよい設定です．必須ではありませんが，ここではこの設定を有効にしているものとして進めます．

(特に，一番上の`push.default`は有効にしないとこの先の手順でエラーが出るかもしれません)

```sh
git config --global push.default current # git push時に同じ名前のリモートブランチを作成する
git config --global init.defaultBranch main # デフォルトのブランチ名をmainに変更する
git config --global fetch.prune true # git fetchする時に常にpruneする
```

### GitHubの初期設定

GitHubとSSHという方式で通信するための設定を行います．

```sh
ssh-keygen -t ed25519
```
数回Enterを叩いて，しばらく待つと

`<ユーザー名>\.ssh\id_ed25519.pub`(Windows)

`<ユーザー名>/.ssh/id_ed25519.pub`(Mac/Linux)

というファイルが作られています．

`.pub`とある方の中身を開き，すべてコピーします．これが公開鍵と呼ばれるものです．

[設定](https://github.com/settings/keys)から，SSH Keys > New SSH Keyをクリック，先ほどコピーした公開鍵を貼り付けます．

<details>
  <summary>公開鍵って何？</summary>
  ここでは公開鍵・秘密鍵を用いた暗号化方式について説明しますが，Gitの話からは逸れるため折り畳みにしています．

  皆さんのなじみのある暗号化方式と言えば，パスワードを用いたものが多いでしょう．
  Zipファイルにパスワードを付けて送り，そのパスワードを相手に教えると自分と相手がそのファイルを開けてアクセスできるというものです．

  この方式では，

  - Zipファイルにパスワードを付ける(暗号化)
  - そのファイルを開く(復号化)

  に同じパスワードを使っています．
  これを共通鍵暗号方式といいます．今回解説する公開鍵暗号方式に比べると，

  - 処理が高速
  - アルゴリズムが容易

  であるというメリットに対し，

  - 基本的に同じパスワード(共通鍵)は使いまわせない
  - どのようにしてパスワードを相手に届けるか問題になる
    - 紙？FAX？
    - Zipファイルと同じメールで送ると，盗聴されたときに全く意味をなさなくなる...

  というデメリットも存在していました．
  
  そこで，文書を暗号化する暗号化のための鍵，そして暗号化された文書を複合化するための鍵を別々にしてしまう，という方式が考案されました．これが公開鍵暗号方式です．

  送信者は，最初に秘密鍵を使って文書を暗号化します．秘密と銘打ってあるだけあり，この人以外は知りえてはならない鍵です．

  そして受信者は，暗号化されたファイルと，送信者の持つ公開鍵を受け取ります．公開鍵を使い，復号すると，無事文書の中身が開ける，という仕組みです．

  公開鍵は，秘密鍵と紐づいており，誰しもが閲覧できる状態になっていることが望ましいです．

  今回，GitHubとこの公開鍵暗号方式でやり取りを行うことになっています．そのため，GitHubには予め自分の公開鍵を知っておいてもらわなければ，我々の発信した暗号化された内容を読み取ることが出来ないのです．
</details>

---

このレポジトリをクローン(ダウンロード)してください．

```sh
git clone git@github.com:VR-lecture/vol15
```

クローン後，ブランチを作ってみましょう．

> [!WARNING]
> この時，ほかの人とブランチ名が被らないようにしましょう！

```sh
git switch -c <あなたのID>
```

ブランチを作ったら，`<あなたのID>.md`のようなファイルを新しく作成し，その中に自分の自己紹介を書いてください．

自己紹介を書くときは，メモ帳，Visual Studio Code, Vimなどのお好きなテキストエディタを使いましょう．

出来たら，コミットしてみましょう．

```sh
git add .
git commit -m "自己紹介を追加"
```

コミットが終わったら，変更内容をリモートレポジトリに反映するためにプッシュという操作をします．

```sh
git push
```

ここまでの設定・操作が上手くいっていれば，このページを開いたときに黄色いダイアログが表示されるはずです！

