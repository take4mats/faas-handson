# スコアを競ってみよう！
負荷試験をして、全部通れば終わりです。

## 手順
- ec2にログイン
- 試験ツールのディレwクトリに移動
    - `cd ~/gatling-charts-highcharts-bundle-2.3.0`
- 試験ツール実行
    - `bash bin/gatling.sh -s HandsOnRequest`

## 試験結果の確認 (暫定)
- 条件
    - 試験結果がすべて `OK` で、 `KO` (=NGの意味) が無いこと

- 出力サンプル: 以下のような標準出力から OK そうか確認してください。 (web server からレポートも確認できるが、いまはNW的に許可していない。手元に html file を scp して見てもらっても構わない)
    ```
    ================================================================================
    2019-04-08 01:54:33                                          61s elapsed
    ---- Requests ------------------------------------------------------------------
    > Global                                                   (OK=1201   KO=0     )
    > request get list                                         (OK=1200   KO=0     )
    > request post                                             (OK=1      KO=0     )

    ---- request get list ----------------------------------------------------------
    [##########################################################################]100%
            waiting: 0      / active: 0      / done:1200
    ---- request post --------------------------------------------------------------
    [##########################################################################]100%
            waiting: 0      / active: 0      / done:1
    ================================================================================

    Simulation computerdatabase.HandsOnRequest completed in 60 seconds
    Parsing log file(s)...
    Parsing log file(s) done
    Generating reports...

    ================================================================================
    ---- Global Information --------------------------------------------------------
    > request count                                       1201 (OK=1201   KO=0     )
    > min response time                                     46 (OK=46     KO=-     )
    > max response time                                    324 (OK=324    KO=-     )
    > mean response time                                    69 (OK=69     KO=-     )
    > std deviation                                         22 (OK=22     KO=-     )
    > response time 50th percentile                         66 (OK=66     KO=-     )
    > response time 75th percentile                         73 (OK=73     KO=-     )
    > response time 95th percentile                         88 (OK=88     KO=-     )
    > response time 99th percentile                        148 (OK=148    KO=-     )
    > mean requests/sec                                 20.017 (OK=20.017 KO=-     )
    ---- Response Time Distribution ------------------------------------------------
    > t < 800 ms                                          1201 (100%)
    > 800 ms < t < 1200 ms                                   0 (  0%)
    > t > 1200 ms                                            0 (  0%)
    > failed                                                 0 (  0%)
    ================================================================================

    Reports generated in 1s.
    Please open the following file: /home/ec2-user/gatling-charts-highcharts-bundle-2.3.0/results/handsonrequest-1554688411952/index.html
    ```

## KO がある場合 (= エラーが有る)
- ログ見たりいろいろして対処して、OK になったら教えてください。

## 更新予定
- 結果が slack 通知されたり dashboard 表示されたり

