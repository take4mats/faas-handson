
# APP 紹介
シンプルなTodo APPである
Viewはindex.htmlをそのまま利用
下記のAPI仕様書を読み、Backendコードを完成してほしい
言語はPython、FlameworkはFlaskとする

## API Interfaces ##
- `1. GET /tasks`
- `2. POST /tasks`
- `3. GET /tasks/{id}`
- `4. DELETE /tasks/{id}`
- `5. PUT /tasks/{id}`


### 1. List all Todo Items ###

**Definition**

`GET /tasks`

**Response**

- `200 OK` when success

```json
[
	{
        "id": "1",
        "item": "Training Preps #1",
        "is_done": false
	},
	{
	    "id": "2",
	    "item": "Training Preps #2",
        "is_done": true
    }
]
```


### 2. Insert a Todo Item ###

**Definition**

`POST /tasks`

**Arguments**

- `"item":string` context of todo item
- `"is_done":boolean` flag to specify if todo is done. default value is False

**Response**

- `201 Created` when success

```json
{
    "id": "1",
    "item": "Training Preps #1",
    "is_done": false
}
```

### 3. Get a Todo Item ###

**Definition**

`GET /tasks/<id>`

**Arguments**

- `"id":integer` identifier of todo item

**Response**

- `200 OK` when success
- `404 Not Found` if id does not exist

```json
{
    "id": "1",
    "item": "Training Preps #1",
    "is_done": false
}
```


### 4. Delete a Todo Item ###

**Definition**

`DELETE /tasks/<id>`

**Arguments**

- `"id":integer` identifier of todo item

**Response**

- `204 No Content` when success
- `404 Not Found` if id does not exist

### 5. Update a Todo Item ###

**Definition**

`PUT /tasks/<id>`

**Arguments**

- `"id":integer` identifier of todo item
- `"item":string` context of todo item
- `"is_done":boolean` flag to specify if todo is done. default value is False

**Response**

- `200 OK` when success
- `404 Not Found` if id does not exist

```json
{
    "id": "1",
    "item": "Training Preps #1",
    "is_done": false
}
```


# Usage
## 重要なパラメーター
- our_regionname: ap-southeast-1 (東京じゃなくてシンガポール)
- your_profile_name: faas01 -- faas40 (自分の番号で！間違うと楽しいです)

## recommended environment
- mac or linux (1人1台 EC2 インスタンスを提供します)
- python version: `3.6.x`
    - Lambda の runtime を python 3.6 としている
    - `2` はムリです、 `3.7` は動くかも、コードに手を加える必要があるので要相談
- Node.js version: `v8.10.0`
    - serverless framework で offline test, deploy するのに必要
    - それより新しくても動くかも

## setup
### AWS コンソールでひとつずつセットアップする場合
#### dynamoDB
- サービス -> dynamoDB -> テーブルの作成
    - テーブル名: `todo-table-faasXX-gui`
    - パーティションキー: `id`
    - 右下の`作成`をクリック

#### lambda
- サービス -> lambda -> 関数の作成
    - 一から作成
    - 関数名: `todo-function-faasXX-gui`
    - ランタイム: `python3.6`
    - 右下の`関数の作成`をクリック
- Designerの`todo-function-faasXX-gui`をクリック
    - 関数コード -> コードエントリータイプ: `Amzaon S3からのファイルのアップロード`
        - Amazon S3 のリンク URL:  `https://s3-ap-southeast-1.amazonaws.com/todo-backend-application/todo.zip`
        - ランタイム: `python3.6`
        - ハンドラ: `lambda_handler.lambda_handler`
    - 環境変数
        - `REGION_NAME: ap-southeast-1`
        - `TABLE_NAME: todo-table-faasXX-gui`
    - 実行ロール
        - IAMコンソールで`todo-function-faasXX-gui-role-XXロールを表示`をクリック
            - permissions policies -> `ポリシーをアタッチします`をクリック
            - 検索窓で`dynamoDB`を検索し、 `dynamoDBFullAccess`をチェック、右下の`ポリシーのアタッチ`をクリック
    - 右上の`保存`をクリック

#### API Gateway
- サービス -> API Gateway
    ==ここから事前に作成済み==
    - `+APIの作成`をクリック
        - Choose the protocol: `REST`
        - 新しいAPIの作成: `新しいAPI`
        - 名前と説明
            - API名: `todo-api-faasXX-gui`
            - 説明: `適当にどうぞ`
            - エンドポイントタイプ: `エッジ最適化`
        - 右下の`作成`をクリック

    ==ここまで事前に作成済み==
    - /を選択し、アクション -> リソースの作成
        - プロキシリソースとして設定: `チェックしない`
        - リソース名: `tasks`
        - リソースパス: `tasks`
        - API Gateway CORS を有効にする: `チェックしない`
        - `リソースの作成`をクリック
    - /tasksを選択し、アクション -> メソッドの追加
        - 以下を作成
           - GET
               - 統合タイプ: `lambda関数`
               - lambdaプロキシ統合の使用: `チェックする`
               - lambdaリージョン: `ap-southeast-1`
               - lambda関数: `todo-function-faasXX-gui`
               - デフォルトタイムアウトの使用: `チェックする`
           - POST
               - 統合タイプ: `lambda関数`
               - lambdaプロキシ統合の使用: `チェックする`
               - lambdaリージョン: `ap-southeast-1`
               - lambda関数: `todo-function-faasXX-gui`
               - デフォルトタイムアウトの使用: `チェックする`    - /tasksを選択し、アクション -> リソースの作成
        - プロキシリソースとして設定: `チェックしない`
        - リソース名: `{id}`
        - リソースパス: `{id}`
        - API Gateway CORS を有効にする: `チェックしない`
        - `リソースの作成`をクリック
    - /{id}を選択し、アクション -> メソッドの追加
        - 以下を作成
           - GET
               - 統合タイプ: `lambda関数`
               - lambdaプロキシ統合の使用: `チェックする`
               - lambdaリージョン: `ap-southeast-1`
               - lambda関数: `todo-function-faasXX-gui`
               - デフォルトタイムアウトの使用: `チェックする`
           - PUT
               - 統合タイプ: `lambda関数`
               - lambdaプロキシ統合の使用: `チェックする`
               - lambdaリージョン: `ap-southeast-1`
               - lambda関数: `todo-function-faasXX-gui`
               - デフォルトタイムアウトの使用: `チェックする`
           - DELETE
               - 統合タイプ: `lambda関数`
               - lambdaプロキシ統合の使用: `チェックする`
               - lambdaリージョン: `ap-southeast-1`
               - lambda関数: `todo-function-faasXX-gui`
               - デフォルトタイムアウトの使用: `チェックする`

#### デプロイ
-  アクション -> APIのデプロイ
    - デプロイされるステージ: `新しいステージ`
    - ステージ名: faasXX-gui
    - ステージの説明: `適当`
    - デプロイメントの説明: `適当`
    - `デプロイ`をクリック

#### テスト
- postman/curlなんでもいいから動作を試してみて

### Serverless Framework でローカルからAWSにデプロイする場合
レクチャー by george

- clone this git repository to your local environment (mac or linux おすすめ)

- 作業はすべてサブディレクトリの `faas/application/backend` で実施
    ```sh
    $ cd faas/application/backend
    ```

- と、言いつつ AWS-SDK の整備 (EC2でない場合)
    - aws_access_key_id, aws_secret_access_key を web console で確認
    - 確認箇所: web console にログイン > `IAM` サービス > ユーザー > 自分のユーザー名 > `認証情報` タブ > `アクセスキーの作成` ボタン > アクセスキーID と シークレットアクセスキー をメモ or ダウンロード ※閉じると閲覧不可. その際は作り直しが必要

- `~/.aws/credentials` に 下記のように書く.
  ```
  [<your_profile_name>]
  aws_access_key_id = <your_access_key_id>
  aws_secret_access_key = <your_secret_access_key>
  ```

- aws-sdk のインストール
  ```sh
  $ npm install -g aws-sdk
  ```

- Serverless Framework のインストール
    ```sh
    $ npm install -g serverless
    $ source ~/.bashrc
    $ sls -v
    バージョンが出ればOK
    ```

- コードの利用に必要なパッケージのインストール
    ```
    $ npm install
    ```

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
