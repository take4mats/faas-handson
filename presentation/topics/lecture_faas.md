# サーバーレスとFaaS概要

+++

## serverless architecture とは？
- 「 ~~サーバーが本当に不要~~ 」
- 「サーバーに直接アクセスしなくても仕事ができる」アーキテクチャ
- 究極の目標は、開発者がサーバーやインフラを気にかけずにコードに全力を注げるようにすること
- 参考
    - [CNCF Serverless Whietepaper v1.0](https://github.com/cncf/wg-serverless/tree/master/whitepapers/serverless-overview)
    - https://qiita.com/__Attsun__/items/31d4beb6dc264efc6c0f
- もたらす効果
    - スケールを気にしなくて良い（auto-scaling）
    - 従量課金

+++

## Serverless と FaaS の関係性

![](../assets/img/serverless_and_faas.png)

+++

## On-prem, IaaS, CaaS, PaaS and FaaS

![](../assets/img/faas_comparison.png)

source: [Introduction to Serverless: What is Serverless?](https://www.youtube.com/watch?v=4caavWtJLfc&feature=share)

+++

## FaaS とは？
- 関数をコードで定義するだけ
- 使用した分だけ課金される（全く起動しなければ無課金）
- イベントドリブン (従来に比べて利用の幅が広がる)
- ステートレスに書くのが通例 (何か保持するなら backend で)

+++