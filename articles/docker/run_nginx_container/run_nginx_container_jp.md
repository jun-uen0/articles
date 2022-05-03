# Nginxイメージをプルしコンテナ起動

### 環境 / 前提
OS: MacOS (intel chip)
Docker

### バージョン等
Docker version: 20.10.12   

### 参考情報等
[nginxコンテナを起動してブラウザから確認しよう](https://snowsystem.net/container/docker/nginx/)

### Nginx公式Dockerイメージ
NginxはDocker Hunで公式のイメージを配布しています。
今回の記事ではこちらのイメージを使用します。
https://hub.docker.com/_/nginx

### 手順
1. Docker HubよりNginxの公式イメージをプル
2. コンテナ起動

## 1. Docker HubよりNginxの公式イメージをプル
最新版のNginx公式イメージをプル
```shell
docker pull nginx
```
プルできたことを確認
```
docker images
```
2. コンテナ起動
ポート3000番でリッスン、ローカルのポート80番にフォワードする
```shell
docker run -p 3000:80 nginx
```
http://localhost:3000/ にアクセスし、動作を確認
