# Locustを使った負荷テスト

### 環境 / 前提
ECS Fargate (負荷テストに使用します。決して必要ではありません。ご自身のアプリで試してください)
DockerとComposeファイルを使用します。

### バージョン
使用したアプリ、パッケージマネージャのバージョン
OS: MacOS (intel chip)
Node version: v16.13.0  
Docker version: 20.10.12
Locust (本記事でインストール手順を紹介します)

### 参考情報等
[docker compose ECS integrationでlocustクラスタをさくっと起動する](https://dev.classmethod.jp/articles/provision-locust-cluster-with-docker-compose-ecs-integration/)

### Locustについて
筆者は今回初めての負荷テストとなります。世の中にはJMeterなどさまざまな負荷テストツールがあるそうですが、今回はLocustを採用しました。理由はLocustの調査も兼ねて負荷テストを行うためです。
誰も使ったことがなく、多くの企業が採用しているため、調べる必要がありました。よければそのまま継続して使用します。

### 手順
1. Composeファイルの作成

## 1. Composeファイルの作成