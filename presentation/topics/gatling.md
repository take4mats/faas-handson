# Gatling
![gatling_icon]()

---

- Scala でシナリオを書く web や API の負荷試験ツールです
- 公式：https://gatling.io/　
- git：https://github.com/gatling/gatling
- 有償版もありますが、無償版でも十分使えます
- Jmeter なんて使ってる人には激しく柔軟に見えるツール
- シナリオのtipsとかは公式にも色々載っている

---

## インストール
v2.3.1 で動作確認済

- java 1.8 以上が必要
- インストール: 無償版の zip を公式からダウンロードして、展開する

- ディレクトリツリー : EC2上では `/home/ec2-user/gatling/` の部分
    ```
    gatling
    ├── bin
    │   └── gatling.sh  # built-in execution script
    ├── conf
    │   ├── logback.xml  # debug log setting
    │   └── gatling.conf  # performance tuning
    ├── lib
    │   └── zinc
    ├── results
    │   └── my-scenario1-1528429451035  # generated result html items
    │       ├── index.html
    │       ├── js
    │       └── style
    ├── target
    │   └── test-classes
    │       └── computerdatabase
    │           └── advanced
    └── user-files
        ├── bodies
        ├── data
        │   └── mydata.csv  # input parameters
        ├── log
        └── simulations
            ├── myproject  # your test scenario by scala here
            └── computerdatabase
    ```

---

## 実行方法
- `bash gatling.sh -s <ClassName>` で自分のシナリオを指定実行できる（ `-s` 以降を指定しなければインタラクティブに選択肢からシナリオを決定）
    ```sh
    $ cd gatling
    $ ./bin/gatling.sh -s computerdatabase.MySimulation
    ```
- クラス名はシナリオファイルの先頭の方を見ればわかる。以下の例なら `computerdatabase.my_test_24h`:
    ```scala
    package computerdatabase

    import io.gatling.core.Predef._
    import io.gatling.http.Predef._
    import scala.concurrent.duration._

    class my_test_24h extends Simulation {
        ...
    }
    ```

---

## シナリオの書き方

シナリオはscalaで書きます。
公式のサンプルシナリオとかtipsとかも参照して取り組んでみてください。

+++

### できそうなこと
経験を元に
- method: 一通りの GET, PUT POST, DELETE, etc.
- 順番にページ遷移できたり, APIレスポンスを次のAPIリクエストに使ったりも可能
- 負荷（rps: request per second）は一定 (constant) にも、段階的にアップ (RampUp) も可能
- 時間も hours, minutes, seconds で指定可能
- 1シナリオで Aという動作パターンのクライアント, Bというそれ を定義し、並行して実行も可能
- csv にデータをもたせて（例えば宛先 x id とか）、順に実行、ランダムに実行、再利用有無の指定なども可能

---

## レポート
結構カックイイ静的 html ファイルを吐いてくれるので、webサーバなく index.html を開けば閲覧可能
![gatling_report]()

+++

頑張るとこんな事もできるよ（画面はデモで）

---

使ってみよう！？