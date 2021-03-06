# ECS FargateのブルーグリーンデプロイをCloudFormationで実行

### まえがき
EC2に置いていたバックエンド環境をECS Fargateに移行しリソースの全てをCloudFormationでIaC化し管理することになりました。
一から負荷テスト、リリースまで行いました。この記事でも各リソースの説明からブルーグリーンデプロイの起動確認まで解説させていただきます。
AWS初心者にもわかるよう、丁寧に解説します。ただ先にお断りしておきますが、AWS初心者の方はこの記事の最後まで達するのにかなり時間がかかるかと思いますのでご了承ください。お仕事で本記事のキャッチアップが必要な方は2週間程度工数をもらった方がいいかもしれません。AWS上級者の方には少し冗長な解説になるかもしれませんが、最後までお読みいただけますと幸いです。

# 今回使用するAWSリソース
- VPC: 仮想ネットワークのこと。Wi-Fiルーターのようなものです。インターネットと違い、アクセスできる人を制限します。Wi-Fiルーターより強力で、遠くからでもアクセスできます。
- EC2: 仮想マシンのこと。遠隔で操れるコンピューターです。VPCの中にあります。
- ECS: EC2の集合体、かつDockerコンテナの管理もできるサービスのこと。
- Fargate: ECSの起動タイプのこと。EC2より便利なサーバレス。 
- CloudFormation: ファイルのこと。AWSの仮想環境の設定値が保存されています。見やすく管理しやすいです。
- IaC: 管理方法のこと。CloudFormationのように仮想環境の設定値をファイルで管理することです。("Infrastructure as Code" = 「インフラをコードで」)
- ブルーグリーンデプロイ: もしアプリがダウンしたら予備アプリをすぐさま反映させて何事もなかったかのように振る舞おうというサービス運用手法です。

### この記事のゴール
- ECS FargateアプリブルーグリーンデプロイをCloudFormationでIaC化し、実行。起動の確認。

### 前提知識
- VPC
- ECS Fargate
- CloudFormation