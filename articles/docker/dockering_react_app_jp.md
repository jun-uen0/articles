# ReactアプリをDockerfile化

### バージョン
Node version: v16.13.0  
Docker version: 20.10.12   

### 参考情報等
この記事で使用したファイルをGitHub上で公開しています。
https://github.com/jun-uen0/react-dockerfile

Here’s How to Dockerize React App
https://www.bacancytechnology.com/blog/dockerize-react-app


### 手順
1. Reactアプリを作成する
2. Dockerfileを作成&起動

## 1. Reactアプリを作成
① [公式チュートリアル](https://ja.reactjs.org/docs/create-a-new-react-app.html)に従いReactアプリを作成   
② 下記コマンドを実行
```shell
npx create-react-app <アプリ名> # ※フォルダ名になります。
cd <アプリ名>
npm start
```
③ http://localhost:3000 にアクセスしReactアプリのウェルカムページが表示されることを確認

④ Ctrl + C で起動停止

## 2. Dockerfileを作成&起動
① 作成したReactアプリのルート直下に`Dockerfile`を作成、下記をコピー  
```yml
# Dockerfile

FROM node:16
WORKDIR /reactapp
ENV PATH /reactapp/node_modules/.bin:$PATH
COPY package.json ./
COPY package-lock.json ./
RUN npm i
COPY . ./
CMD ["npm", "start"]
```

② イメージのビルド
```
docker build -t <image name> . 
```
③ コンテナの起動
```shell
docker run \
    -it \
    --rm \
    -v ${PWD}:/reactapp \
    -v /reactapp/node_modules \
    -p 3000:3000 \
    -e CHOKIDAR_USEPOLLING=true \
    <image name>:latest
```
④ http://localhost:3000 にアクセスしReactアプリのウェルカムページが表示されることを確認