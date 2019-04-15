# Section FaaS
Hello, I'm gonna tell you about `serverless` and `FaaS` today.

- presentation: check out [from here! (GitPitch)](https://gitpitch.com/take4mats/faas-handson?p=presentation)
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
- 0910 講義開始
- 10min 休憩
- 1010-1140: ハンズオン Part1 (web) 1.5h
- 1140-1240: 昼休み
- 1240−1340: ハンズオン Part2 (infra as code)
- 10min 休憩
- 1350-1600: ハンズオン Part3 (challenge) (10min 休憩含む)
- 1600-1630: 解説、業務紹介
- 1630-1730: 5日間の振り返り？, 例の 15min work

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
- 1. Webコンソールから作る
    - lambda 作成
    - apigw は指示通り作ってもらう
    - dynamodb も指示通り
    - 動作確認
        - curl や frontend で動作確認してもらう

- 2. slsから作る
    - なにかwebコンソールで作ったものにプラスする？（or 負荷試験対応のみでも）
    - slsが動作する踏み台サーバ40台
    - ポチっとデプロイ
    - 動作確認
        - curl か frontend で動作確認してもらう

- 3. 負荷をかけてみる
    - 負荷試験の話 (gatling) スライドを挟もう **松田**
    - gatlingで負荷かてみる
    - 何が悪いか考えてみてくれ
