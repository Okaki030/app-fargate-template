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

## 参考
[Build your Go image | Docker Documentation](https://docs.docker.com/language/golang/build-images/)
[olliefr/docker-gs-ping: A simple Go server example for Docker's "Getting Started with Docker and Go".](https://github.com/olliefr/docker-gs-ping)