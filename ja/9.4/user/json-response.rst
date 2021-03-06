==================
JSONによる検索結果
==================

JSON応答による検索
==================

|Fess| の検索結果をJSONにより出力することができます。JSONにより出力するためには管理画面のクロール全般の設定でJSON応答を有効にしておく必要があります。

リクエスト
----------

JSONにより出力結果を得るためには
``http://localhost:8080/fess/json?query=検索語``
のようなリクエストを送ります。リクエストパラメータについては以下の通りです。

+----------------+------------------------------------------------------------------------------------------+
| query          | 検索語。URLエンコードして渡します。                                                      |
+----------------+------------------------------------------------------------------------------------------+
| start          | 開始する件数位置。0から始まります。                                                      |
+----------------+------------------------------------------------------------------------------------------+
| num            | 表示件数。デフォルトは20件です。100件まで表示できます。                                  |
+----------------+------------------------------------------------------------------------------------------+
| fields.label   | ラベル値。ラベルを指定する場合に利用します。                                             |
+----------------+------------------------------------------------------------------------------------------+
| callback       | JSONPを利用する場合のコールバック名。JSONPを利用しない場合は指定する必要はありません。   |
+----------------+------------------------------------------------------------------------------------------+

Table: リクエストパラメータ


レスポンス
----------

以下のようなレスポンスが返ります。

::

    {
        "response": {
            "version": 1,
            "status": 0,
            "query": "Fess",
            "execTime": 0.59,
            "pageSize": 20,
            "pageNumber": 1,
            "recordCount": 101,
            "pageCount": 6,
            "result": [
                {
                "created":"2014-05-24T15:13:29.096+0900",
                "docId":"0592263c6cae4141b3a276894e8e326d",
                "title":"Fess \u3092\u5229\u7528\u3057\u3066\u3044\u308B\u30B5\u30A4\u30C8",
                "url":"http:\u002F\u002Ffess.codelibs.org\u002Fja\u002Fusers.html",
                "score":0.7036715,
                "site":"fess.codelibs.org\u002Fja\u002Fusers.html",
                "filetype_s":"html",
                "contentDescription":" <em>fess<\u002Fem> \u5168\u822C \u5165\u9580...",
                "digest":"Fess \u5168\u822C \u5165\u9580 \u30C9\u30AD\u30E5\u30E1\u30F3 Jav...",
                "host":"fess.codelibs.org",
                "mimetype":"text\u002Fhtml",
                "contentLength":22788,
                "boost":1.0,
                "lastModified":"2014-05-22T11:09:07.000+0900",
                "id":"http:\u002F\u002Ffess.codelibs.org\u002Fja\u002Fusers.html",
                "urlLink":"http:\u002F\u002Ffess.codelibs.org\u002Fja\u002Fusers.html"
                },
    ...
            ]
        }
    }

各要素については以下の通りです。

+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| response             | ルート要素。                                                                                                                              |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| version              | フォーマットバージョン。                                                                                                                  |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| status               | レスポンスのステータス。status値は、0:正常、1:検索エラー、2または3:リクエストパラメータエラー、9:サービス停止中、-1:API種別エラーです。   |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| query                | 検索語。                                                                                                                                  |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| execTime             | 応答時間。単位は秒。                                                                                                                      |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| pageSize             | 表示件数。                                                                                                                                |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| pageNumber           | ページ番号。                                                                                                                              |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| recordCount          | 検索語に対してヒットした件数。                                                                                                            |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| pageCount            | 検索語に対してヒットした件数のページ数。                                                                                                  |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| result               | 検索結果の親要素。                                                                                                                        |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| site                 | サイト名。                                                                                                                                |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| contentDescription   | コンテンツの説明。                                                                                                                        |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| host                 | ホスト名。                                                                                                                                |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| lastModified         | 最終更新日時。                                                                                                                            |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| cache                | コンテンツの内容。                                                                                                                        |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| score                | ドキュメントのスコア値。                                                                                                                  |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| digest               | ドキュメントのダイジェスト文字列。                                                                                                        |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| created              | ドキュメントの生成日時。                                                                                                                  |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| url                  | ドキュメントのURL。                                                                                                                       |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| id                   | ドキュメントのID。                                                                                                                        |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| mimetype             | MIMEタイプ。                                                                                                                              |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| title                | ドキュメントのタイトル。                                                                                                                  |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| contentTitle         | 表示用のドキュメントのタイトル。                                                                                                          |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| contentLength        | ドキュメントのサイズ。                                                                                                                    |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| urlLink              | 検索結果としてのURL。                                                                                                                     |
+----------------------+-------------------------------------------------------------------------------------------------------------------------------------------+

Table: レスポンス情報


