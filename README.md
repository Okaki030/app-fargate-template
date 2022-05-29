# app-fargate-template
![example workflow](https://github.com/Okaki030/app-fargate-template/actions/workflows/deploy.yml/badge.svg)

## 概要
[Okaki030/terraform-fargate-template](https://github.com/Okaki030/terraform-fargate-template)でデプロイするサンプルアプリケーション。

## 使い方
CI/CDを動かすための設定を記述する。

### 1. GitHub Secretsの設定

<img width="757" alt="スクリーンショット 2022-05-28 12 32 58" src="https://user-images.githubusercontent.com/36916494/170808323-99f6aadb-e225-4128-a76d-173196dc93b1.png">

### 2. ecspressの設定ファイルを編集
自身の実行環境に合わせて、[config.yml](https://github.com/Okaki030/app-fargate-template/blob/main/ecspresso/config.yaml)のtfstateを保持するurlを編集する。

```
plugins:
  - name: tfstate
    config:
      url: s3://okawa-tfstate/template/cicd/main.tfstate # 自身の環境に合わせる
```

### 3. デプロイワークフローの編集
自身の実行環境に合わせて、[deploy.yml](https://github.com/Okaki030/app-fargate-template/blob/main/.github/workflows/deploy.yml)の`AWS_REGION`と`SYSTEM_NAME`を編集する。

```ecspress/deploy.yml
env:
  AWS_REGION: ap-northeast-1 # 自身の環境に合わせる
  SYSTEM_NAME: template # 自身の環境に合わせる
  IMAGE_TAG: ${{ github.sha }}
```

### デプロイタイミング
mainブランチへのpushをトリガーとしてアプリケーションが自動デプロイされる。

## ローカル実行
サンプルアプリケーションをローカル環境で実行する手順を記述する。

### 準備

```
$ docker-compose build
$ docker network create app
```

### 実行

```
$ docker-compose up
```

## 手動デプロイ
サンプルアプリケーションを手動でデプロイする手順を記載する。

### イメージのpush

```
$ docker build -t template-app .
$ docker tag template-app:latest {ECRリポジトリ}:latest
$ docker push {ECRリポジトリ}:latest
```

### デプロイ

```
$ SYSTEM_NAME=template IMAGE_TAG=latest AWS_REGION=ap-northeast-1 ecspresso deploy --config=config.yaml
```

### サービスの作成

```
SYSTEM_NAME=template IMAGE_TAG=latest AWS_REGION=ap-northeast-1 ecspresso create --config=config.yaml 
```
