## ハンズオン

+++

## 目標（再確認）
TODOリストアプリを作ろう！

+++

### 以下のAPI仕様に基づいて作れ

+++

## システム構成

- AWS 上に全て構築
    - アプリの配置/構成
        ```
               /-- frontend on S3 (or on localhost)
        client
               \-- API Gateway -- Lambda -- DynamoDB

                        (CloudWatch)
        ```
    - DNS, SSL/TLS cert: API-Gateway のネイティブなやつでご勘弁を

+++

詳しくは、slackに張っているURLをクリック
https://github.com/take4mats/faas-handson/blob/master/presentation/docs/app_intro.md
