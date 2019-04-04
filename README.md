# Section FaaS
Hello, I'm gonna tell you about `serverless` and `FaaS` today.

- presentation: check out [from here! (GitPitch)](https://gitpitch.com/iwashi/2019nttcomtraining/master?p=faas/presentation)
  - if the above link is broken, find by yourself based on below pattern:
    ```
    https://gitpitch.com/$user/$repo/$branch?p=$dir/$subdir
    ```
  - NOTE: the repository must be `public`.  If not, give up to see this through GitPitch.
  - or to see raw data, go to subdir `/presentation`.

- sample code: check out the subdir `/sample-code`


---

## 当日のタイムライン
- 0900 opening
- 0930 講義開始
- 1030 環境セットアップ
- 1100 ハンズオン開始
    - webコンソールから 1h
    - (1200-1300 昼休み)
    - sls から 1h
    - トラシュー 2h
- 1600 ハンズオン終了
- 1600-1730 振り返り、業務紹介、QA

## 講義内容
講義担当 **伊藤**, sub: 松田 etc.
- 自己紹介
- サーバーレス、FaaSとは
- オンプレからSaaSまでの比較
- 代表的なサービス事例: lambda, azurefunction, gcf
- 事例 (外部イベントとかで見てきた事例など)
    - パターン
        - 従来のシステムのサーバーレス化
        - 全く違う発想の、FaaSだからこそできるような事例
    - 事例
        - aiboとか良いよね
        - 動画、画像のエンコード (いろんな画質で動画が見られるのは売れでこんなものがあるからだよ、など)

## ハンズオン内容
- 1. Webコンソールから作る (60m: 1100-1200 含む10分休憩) **伊藤**
    - lambda 作成
        - コードはzip をupload
    - apigw は指示通り作ってもらう
    - dynamodb も指示通り
    - cloudwatchの使い方講座
        - ログ検索方法
        - グラフのつくり方(metric)
    - 動作確認
        - curl か frontend で動作確認してもらう

- 2. slsから作る (infrastructure as code を体験) (60m: 1300-1400　含む10分休憩) **松田**
    - なにかwebコンソールで作ったものにプラスする？（or 負荷試験対応のみでも）
    - slsが動作する踏み台サーバ40台
    - ポチっとデプロイ
    - 動作確認
        - curl か frontend で動作確認してもらう

- 3. 負荷をかけてみる (120m: 1400-1600 含む10分*2休憩)
    - 負荷試験の話 (gatling) スライドを挟もう **松田**
    - gatlingで負荷かてみる
        - もちろんコケる
    - 何が悪いか考えてみてくれ
        - ハマるのは、どこが悪さしているか読みづらい、autoscaleしていない
    - さて直してみよう
        - 一旦 ggks
    - 答え合わせ
        - on-demand
        - reserved capacity unit 莫大
        - auto-scaleだけでも本当はいいよ。ただスケールアウトするには時間かかる

- クロージング **松田**
    - 業務紹介も場合によってはココで