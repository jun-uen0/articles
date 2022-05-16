# Reactで動画再生アプリを作成

### 前提
ローカルの動画か、なければYouTubeなどでも可


<!-- # 動画再生ライブラリのインストール
```shell
npm install react-player # or yarn add react-player
```
参考：https://www.npmjs.com/package/react-player

# MKV拡張子を読み込み可能にする
react-app-env.d.tsはTypeScript特有の型定義を行うファイル。
グローバルに適応される。ここでは読み込みたいファイルの拡張子を指定している。
`src/react-app-env.d.ts`
```ts
declare module '*.mkv' {
  const src: string;
  export default src;
}
``` -->

```shell
npm i antd
```
```shell
npm i jol-player --save
```

### 参考
[React x Typescriptでローカルの動画を再生する](https://qiita.com/ko-izumi/items/983eb9421350a5d080f3)
[What is the react-app-env.d.ts in a react typescript project for](https://stackoverflow.com/questions/67262914/what-is-the-react-app-env-d-ts-in-a-react-typescript-project-for)
[A Simple, beautiful and powerful react player](https://reactjsexample.com/a-simple-beautiful-and-powerful-react-player)