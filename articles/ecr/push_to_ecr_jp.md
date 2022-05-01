# DockerイメージをAWS ECRにプッシュする

### 注意事項
AWS ECRは無料ではありません。
運用を継続する予定がなければ必ず削除してください。
AWSリソースはどんなに無料枠があっても削除しておくに限ります。

### 環境 / 前提
Dockerイメージ
AWSアカウント
AWS CLI 2.5.8

### ECRについて
AWS上のDocker Hubのようなものです。
プライベートリポジトリを設けることもできます。
パブリックリポジトリにイメージを保管しDocker Hubのように使用することもできます。

### 手順
1. Dockerイメージの用意、確認
2. AWS ECRへイメージをプッシュ
3. ローカルへプルし起動確認
4. ECRイメージの削除

## 1. Dockerイメージの用意、確認
Reactに興味のある方はこちらの記事を参考にDockerイメージを作成してみてください。今回の起動確認はこちらのイメージで行います。
[ReactアプリをDockerイメージ化](https://zenn.dev/jun_uen0/articles/531b1f5e25d539)
サクッとDockerイメージを作成したい方はこちらの記事を参考にしてください。
[Nginxイメージをプルしコンテナ起動](https://zenn.dev/jun_uen0/articles/5ac2ff4cf53d15)

2. AWS ECRへイメージをプッシュ
① [ECRのコンソール](https://console.aws.amazon.com/ecr/repositories)へ移動し新しいパブリックリポジトリを作成
② プッシュコマンドを表示
③ 1番のコマンドをコピーしAWSへログイン
```shell
aws ecr-public get-login-password --region <リージョン名> | docker login --username AWS --password-stdin public.ecr.aws/~~~

Login Succeeded
```
2番は今回飛ばす。ローカルのイメージ作成についてのコマンド。既に用意してある。
④ 3番のコマンドを参考にイメージタグ付け
```shell
docker tag <用意したイメージ名>:latest public.ecr.aws/d6a4r9k9/my-ecr-repository:latest
```
確認
```shell
docker images
```

⑤ 4番のコマンドを参考にECRへイメージをプッシュ
```shell
➜  articles git:(main) ✗ docker push public.ecr.aws/d6a4r9k9/my-ecr-repository:latest
The push refers to repository [public.ecr.aws/d6a4r9k9/my-ecr-repository]
6532d1bd92d7: Pushing [========================================>          ]    181MB/223.4MB
1bfe2f2c209c: Pushing [==============================>                    ]  156.5MB/259.2MB
5bc57cb39f11: Pushed 
1f63745992bb: Pushed 
fea31d3e0c85: Pushed 
0fc8a3e8b32a: Pushed 
99307ceff565: Pushed 
5cc685c4cd61: Pushed 
6fd97e423126: Pushed 
ca58f1c44290: Pushing [==================>                                ]  188.3MB/510.5MB
957a6eed8d1f: Pushing [==========================================>        ]  123.8MB/145.5MB
85fe00380881: Pushing [==================================================>]  17.87MB
5d253e59e523: Waiting 
b9fd5db9c9a6: Waiting 
```
⑥ ECRコンソールへ戻り、リポジトリ名をクリック
イメージが無事プッシュされたことを確認

## 3. ローカルへプルし起動確認
① 先ほどECRへプッシュするためにタグ付けしたイメージを削除
```shell
docker rmi <イメージ名>
```
② ECRからURIを取得し、イメージをプル
ECRコンソール画面でURIを確認し、コピー

```shell
$ docker pull <コピーしたURI>
latest: Pulling from ~~~~~
Digest: sha256:~~~~~~~~~~~~~~~~~~~~
Status: Downloaded newer image for <コピーしたURI>
<コピーしたURI>
```
③ コンテナ起動
```shell
docker run -p 3001:3000 <コピーしたURI>
```
http://localhost:3001/　にアクセスし起動確認


## 4. ECRイメージの削除
わざわざ手順内にこの項目を載せました。
勉強のためにだけ使用したAWSリソースは都度削除しましょう。
料金のことは後から考えて、脳死で削除しておきましょう。
勝手に別のリソースを立ち上げている可能性もあります。

① ECRコンソール画面でURIを選択し削除

### 後書き
ECS Fargateの記事のために今回の記事を作成しました。
実は使用するDockerイメージがNginxのものだった場合、わざわざECRにプッシュする必要はありません。
ただ、Docker Hubに置いてないアプリのイメージを使用する場合には必ずセットで使用するリソースなので詳細させていただきました。
また、ECRリポジトリを作成する際パブリックにすることは滅多にないかもしれません。今回はローカルで確認するためにパブリックにしました。もしECSに紐づけるのであればプライベートのほうがセキュリティ的によいでしょう。業務で使用するなら必ずプライベートにする必要があります。

読んでくださった方々のお役に少しでも立つことができたなら幸いです。