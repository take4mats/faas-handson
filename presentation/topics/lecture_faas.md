# サーバーレスとFaaS概要

+++

## serverless architecture とは？
- 「 ~~サーバーが本当に不要~~ 」
- 「サーバーに直接アクセスしなくても仕事ができる」アーキテクチャ
- 究極の目標は、開発者がサーバーやインフラを気にかけずにコードに全力を注げるようにすること
- もたらす効果
    - スケールを気にしなくて良い（auto-scaling）
    - 従量課金

+++

## Serverless と FaaS の関係性

![serverless_and_faas](presentation/assets/img/serverless_and_faas.png)

+++

## On-prem, IaaS, CaaS, PaaS and FaaS

![faas_comparison](presentation/assets/img/faas_comparison.png)

source: [Introduction to Serverless: What is Serverless?](https://www.youtube.com/watch?v=4caavWtJLfc&feature=share)

+++

## FaaS とは？
- 関数をコードで定義するだけ
- 使用した分だけ課金される（全く起動しなければ無課金）
- イベントドリブン (従来に比べて利用の幅が広がる)
- ステートレスに書くのが通例 (何か保持するなら backend で)

+++
