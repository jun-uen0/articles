### この記事のゴール
インターネットにサイトを公開
公開するサイト：nginxのウェルカムページ「Welcome to ngrok!」


### 環境 / 前提
下記環境にて動作確認。Ngrok以外はインストール済みを想定。
OS: macOS ver 12.1　(intel chip)
Homebrew 3.4.7
Nginx 1.21.6
Ngrok 3.0.2

### Ngrokについて
Ngrok (読：エンジーロック)
ローカルの特定のポートをWeb上に公開するツール
料金：無料 (有料版でドメインやチーム使用が可能)
公式サイト：https://ngrok.com/

### 手順
1. [Ngrok公式サイト](https://dashboard.ngrok.com/signup)でアカウント登録。メール認証を済ませる。
2. [Ngrok公式サイトのダウンロードページ](https://ngrok.com/download)に沿いNgrokをインストール
```shell
brew install ngrok/ngrok/ngrok
```
3. [Ngrok管理画面の「Getting Started > setup & installation」](https://dashboard.ngrok.com/get-started/setup)で認証トークンとコマンドを取得。実行。
```shell
ngrok config add-authtoken <token>
```
4. Nginxを起動。ローカルホスト8080にウェルカムページを表示
```shell
nginx

# http://localhost:8080/　にアクセスし、ウェルカムページが表示されているかを確認。確認が取れたら5へ
```
5. Ngrokの起動。ポート8080をWebに公開
```shell
ngrok http 8080

# 付与されたアドレスにアクセスし、Nginxのウェルカムページが表示されていいるかを確認。
```


### 参考
[Web開発の便利ツール ngrokをご紹介！ webhookを利用した開発に便利！]()https://www.youtube.com/watch?v=9UYZf-AUXhw&t=24s

[ngrokが便利すぎる](https://qiita.com/mininobu/items/b45dbc70faedf30f484e)