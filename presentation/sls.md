### Serverless Framework でローカルからAWSにデプロイする場合

- ここでディレクトリとファイル解説
    ```
    backend/
    ├── README.md  # このファイル！
    ├── lambda_handler.py  # lambda function がトリガーされた時に最初に読まれるファイル
    ├── package.json  # sls自体が node.js 製なので必要なライブラリを
    ├── node_modules/  # node.js ライブラリの入る場所
    ├── serverless.yml  # deploy等に必要な設定ファイル（これが sls のキモ）
    ├── migrations/  # 応用編のための
    ├── src/
    │   └── todo.py  # コアのロジックを書いたファイル（あんまり分離するボリュームじゃなかった）
    └── tests/
        └── test_sls_offline.py  # 応用編のためのテストコード
    ```

- デプロイ
    ```sh
    $ sls deploy --profile <your_profile_name> --stage <your_profile_name> --region <our_region_name>
    ```

- 出力例 ( profile_name: `t12-george`, region_name: `ap-southeast-1`, 解説を `# foobar` で )
    ```
    george@gpro2016.local$ cd 2019nttcomtraining/faas/application/backend
    george@gpro2016.local$ sls deploy --profile t12-george  # 実行！
    Serverless: Packaging service...
    Serverless: Excluding development dependencies...
    Serverless: Uploading CloudFormation file to S3...
    Serverless: Uploading artifacts...
    Serverless: Uploading service todo.zip file to S3 (1.73 KB)...
    Serverless: Validating template...
    Serverless: Updating Stack...
    Serverless: Checking Stack update progress...
    ..............
    Serverless: Stack update finished...  # ココまでくれば deploy 完了。 Congrats!
    Service Information
    service: todo
    stage: t12-george  # apigw stage name == profile name にしている
    region: ap-southeast-1  # ラクサ美味いよラクサ
    stack: todo-t12-george  # CloudFormation Stack name
    resources: 15
    api keys:
    None
    endpoints:  # 以下エンドポイントのURL報告して貰うかも。5つあることも確認
    GET - https://2m8wyq5lv3.execute-api.ap-southeast-1.amazonaws.com/t12-george/tasks
    POST - https://2m8wyq5lv3.execute-api.ap-southeast-1.amazonaws.com/t12-george/tasks
    GET - https://2m8wyq5lv3.execute-api.ap-southeast-1.amazonaws.com/t12-george/tasks/{id}
    PUT - https://2m8wyq5lv3.execute-api.ap-southeast-1.amazonaws.com/t12-george/tasks/{id}
    DELETE - https://2m8wyq5lv3.execute-api.ap-southeast-1.amazonaws.com/t12-george/tasks/{id}
    functions:
    todo: todo-function-t12-george  # あなた用の Lambda function を探す時にここの名前で
    layers:
    None
    Serverless: Removing old service artifacts from S3...  # upload packege がたまりすぎないように rotate してる
    ```

- tips: デプロイでエラーが出たら `export SLS_DEBUG='*'` してデバッグメッセージを出す。 消すときは `export SLS_DEBUG=''`


### Serverless Framework でローカルでテストする
ローカルでのテストも頑張ってみたい場合は、読んでね。ローカルに apigw, lambda, dynamodb をエミュレートして TDD できるお
（完全おまけコンテンツかな）

- java 1.8 以上をインストール
- execute sls offline
    ```sh
    $ sls offline start --profile <your_profile_name> --stage <your_profile_name> --region <our_region_name>
    ```
