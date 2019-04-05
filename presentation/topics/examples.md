## Serverless Architecture 事例

+++

## A. 従来システムのサーバーレス化
**LIFT** and Shift

+++

### 事例A-1 典型的な Web API の置き換え
- 一般的なCRUD API
<img src="presentation/assets/img/web_api.jpg" width="100%">
https://yoshidashingo.hatenablog.com/entry/serverlss-usecases-2017

+++
### 事例A-2 SPA
- S3のjsを押いて、lambdaを発火
<img src="presentation/assets/img/spa.png" width="100%">
https://yoshidashingo.hatenablog.com/entry/serverlss-usecases-2017

---

## B. FaaS ならではの事例
Lift and **SHIFT**

+++

### 事例 B-1. 非同期ジョブ
- S3の画像アップロードされたら、リサイズや切り出しを実行
<img src="presentation/assets/img/nikkei.png" width="100%">
https://yoshidashingo.hatenablog.com/entry/serverlss-usecases-2017

+++
### 事例 B-2 Webサイト監視
- CloudWatchによる定期的なトリガーでヘルスチェックを実行
<img src="presentation/assets/img/monitoring.jpg" width="100%">

+++

### 事例 B-3 オンコールシステム
- アラートをトリガーに電話を鳴らす
<img src="presentation/assets/img/oncall.png" width="100%">
https://yoshidashingo.hatenablog.com/entry/serverlss-usecases-2017

### 事例 B-4 aibo
