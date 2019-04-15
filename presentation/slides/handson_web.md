## Part 1 - Web 編

+++

AWS の Web コンソールを使って サーバーレスなシステムを構築しよう！

+++

その前に今回触れるFaaSやBaaSをご紹介

+++

<img src="presentation/assets/img/lambda.png" width="50%">
### AWS Lambda
- 言わずと知れたKing of FaaS
- イベントドリブン(非常駐型)でコードを実行
- 実行されたリソース分の課金/オートスケール
- GITからデプロイはできない
- トリガーは自社サービスやSDKのみ

+++

<img src="presentation/assets/img/apigw.png" width="50%">
### Amazon API Gateway
- API作成/管理サービス
- 流量制限や認証などを行う
- LambdaをAPI(HTTP)でリクエスト際は必須
- リクエスト数による従量課金/オートスケール
- 2015年7月サービス開始(Lambdaに遅れこと3ヵ月)

+++

<img src="presentation/assets/img/dynamodb.png" width="50%">
### Amazon DynamoDB
- マネージドなNoSQLデータベース
- データは3か所のAZに保存
- データ容量の増加に応じた増設作業は不要
- 使った分だけの従量課金
- 2012年1月サービス開始

<img src="presentation/assets/img/cloudwatch.png" width="50%">
### Amazon CloudWatch
- AWSリソースの死活/性能/ログ監視
- 取得メトリックをグラフ化
- メトリックからアラーム等のアクションを設定可能
- 使った分だけの従量課金
- 2009年5月サービス開始

#### システム構成

<img src="presentation/assets/img/handson_web.png" width="80%">

+++

####
+++

## Let's Try!

構築ガイド: slackに張っている URL をクリック
https://github.com/take4mats/faas-handson/blob/master/presentation/docs/webconsole.md
