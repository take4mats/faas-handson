## slsからのデプロイ

+++

slackに張ったURLを参照


+++

おすすめのデプロイツール: Serverless Framework
- [Serverless Framework の書き方](https://serverless.com/framework/docs/providers/aws/)
- .aws/credentials: studentXX でキーを保存
- コマンド:
    - DynamoDB Local のインストール: `sls dynamodb install`
    - DynamoDB Local の起動: `sls dynamodb start --profile studentXX`
    - serverless offline の起動: `sls offline --profile studentXX` (dynamodb start も包含)
    - deploy: `sls deploy --profile studentXX`

---
