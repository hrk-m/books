本番サーバの確認
https://hrk-m.github.io/books/

## 環境構築

1. npm をインストールする

```bash
$ npm install -g gitbook-cli
```

2. GitBook をローカルで起動する

```bash
$ gitbook serve ./ ./docs
```

3. http://localhost:4000 でを開く

## 開発手順

1. `master` ブランチから、新しいブランチを切る<br />
   ex) feature/xxxx<br />
   ※[作業場所] books ディレクトリの中を修正する

2. 作業が完了したら以下のコマンドでサーバを起動し`./docs`の中を書き換える

```
$ gitbook serve ./ ./docs
```

3. 修正文を push する

4. master ブランチにマージする
