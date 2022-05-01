# ECS FargateでReactアプリを起動する

## 手順
1. ロカールでReactアプリを作成
2. イメージ構築
3. ECRへプッシュ
4. ECS Fargateを設定

## 前提
- Node.js
- Typescript

## ロカールでReactアプリを作成
言語は適宜変更してください。
```shell
npx create-react-app <フォルダ名>
```
```shell
cd <フォルダ名>
```
```shell
npm start
```
