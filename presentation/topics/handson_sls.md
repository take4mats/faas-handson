## slsからのデプロイ

+++

おすすめのデプロイツール: Serverless Framework
- [Serverless Framework の書き方](https://serverless.com/framework/docs/providers/aws/)
- .aws/credentials: faasXX でキーを保存
- コマンド:
    - DynamoDB Local のインストール: `sls dynamodb install`
    - DynamoDB Local の起動: `sls dynamodb start --profile faasXX`
    - serverless offline の起動: `sls offline --profile faasXX` (dynamodb start も包含)
    - deploy: `sls deploy --profile studentXX`

+++

slackに張ったURLを参照
https://github.com/take4mats/faas-handson/blob/master/presentation/sls.md
