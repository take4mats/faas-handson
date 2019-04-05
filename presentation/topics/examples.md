## Serverless Architecture 事例

- パターン
    - 従来のシステムのサーバーレス化
    - 全く違う発想の、FaaSだからこそできるような事例
- 事例
    - aiboとか良いよね
    - 動画、画像のエンコード (いろんな画質で動画が見られるのは売れでこんなものがあるからだよ、など)


+++

## パターンA. 従来のシステムのサーバーレス化
**LIFT** and Shift

+++

### 事例 A-1. 典型的な Web API の置き換え
- APIGW, Lambda, DynamoDB
<img src="presentation/assets/img/web_api.jpg" width="50%">
---

## パターンB. FaaS ならではの事例
Lift and **SHIFT**

+++

### 事例 B-1. hoge
- https://yoshidashingo.hatenablog.com/entry/serverlss-usecases-2017 らへんから
    - SPA
    - 非同期ジョブ（S3にuploadされた動画、画像、CSVを加工するなど）
    - 監視・通知（cloudwatch eventからトリガーされて電話やslack通知など）
    - Azureの例
    - Alexaのバックエンドとして
    - lambda@edge
        - 公式ドキュメントが「想定する使い方」をまとめてくれていて一番いいかも
        - キャッシュヒット率を向上させるためのクエリパラメータの整列
        - コンテンツベースの動的オリジンの選択
        - とにかく cloudfront に計算機能を add-on するような感じ。
