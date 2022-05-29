# app-fargate-template

## アプリケーション実行手順
### 準備

```
$ docker-compose build
$ docker network create app
```

### 実行

```
$ docker-compose up
```

## CI/CD設定手順
### Actions secretsの設定

<img width="757" alt="スクリーンショット 2022-05-28 12 32 58" src="https://user-images.githubusercontent.com/36916494/170808323-99f6aadb-e225-4128-a76d-173196dc93b1.png">

## 手動デプロイ
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

## 参考
[Build your Go image | Docker Documentation](https://docs.docker.com/language/golang/build-images/)
[olliefr/docker-gs-ping: A simple Go server example for Docker's "Getting Started with Docker and Go".](https://github.com/olliefr/docker-gs-ping)
