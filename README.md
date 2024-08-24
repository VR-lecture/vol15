# vol15

Git/GitHubで共同作業をしてみましょう！

## 目標
GitHubを使って，プルリクエストを作成する

## 手順

### Gitの初期設定

Gitをインストールした後は初期設定が必要です．

```sh
git config --global user.name <あなたの名前>
git conifg --global user.email <@users.noreply.github.comで終わるメールアドレス>
```

`user.name`はコミットしたときに表示される名前です．出来るだけ本名は避け，特にこだわりが無ければGitHubのIDと同じにしておくとよいでしょう．

`user.email`はコミットする時に表示されるメールアドレスです．ここでは実際に使っているメールアドレスは設定せず，GitHubが発行しているメールアドレスを使用することにします．

GitHubのメールアドレスを確認するには，[設定](https://github.com/settings/emails)を開き，下の方にある`Primary email address`に記載のある`数字+ID@users.noreply.github.com`を指定します．

次に，設定しておくとよい設定です．必須ではありませんが，ここではこの設定を有効にしているものとして進めます．

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

そして，`.ssh/id_ed25519.pub`の中身を全てコピーします．これが公開鍵と呼ばれるものです．

GitHubの[設定](https://github.com/settings/keys)を開き，SSH Keys > New SSH Keyを押して，開いた画面のテキストボックスに先ほどコピーした公開鍵をペーストします．

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


