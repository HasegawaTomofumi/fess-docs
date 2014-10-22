======================================
Solrのダイナミックフィールドの利用方法
======================================

Solr のダイナミックフィールド
=============================

Solr
は対象ドキュメントを項目(フィールド)ごとに登録するためにスキーマを定義されています。Fess
で利用する Solr のスキーマは solr/core1/conf/schema.xml
に定義されています。title や content
など標準のフィールドと、自由にフィールド名を定義できるダイナミックフィールドが定義されています。Fess
の schema.xml
で利用できるダイナミックフィールドは以下のものになります。詳細なパラメータ値については
Solr のドキュメントを参照してください。

::

        <dynamicField name="*_s" type="string" indexed="true" stored="true"/>
        <dynamicField name="*_t" type="text" indexed="true" stored="true"/>
        <dynamicField name="*_b" type="boolean" indexed="true" stored="true"/>
        <dynamicField name="*_i" type="int" indexed="true" stored="true"/>
        <dynamicField name="*_l" type="long" indexed="true" stored="true"/>
        <dynamicField name="*_f" type="float" indexed="true" stored="true"/>
        <dynamicField name="*_d" type="double" indexed="true" stored="true"/>
        <dynamicField name="*_ti" type="tint" indexed="true" stored="true"/>
        <dynamicField name="*_tl" type="tlong" indexed="true" stored="true"/>
        <dynamicField name="*_tf" type="tfloat" indexed="true" stored="true"/>
        <dynamicField name="*_td" type="tdouble" indexed="true" stored="true"/>
        <dynamicField name="*_tdt" type="tdate" indexed="true" stored="true"/>
        <dynamicField name="*_pi" type="pint" indexed="true" stored="true"/>
        <dynamicField name="*_pl" type="plong" indexed="true" stored="true"/>
        <dynamicField name="*_pf" type="pfloat" indexed="true" stored="true"/>
        <dynamicField name="*_pd" type="pdouble" indexed="true" stored="true"/>
        <dynamicField name="*_pdt" type="pdate" indexed="true" stored="true"/>
        <dynamicField name="*_si" type="sint" indexed="true" stored="true"/>
        <dynamicField name="*_sl" type="slong" indexed="true" stored="true"/>
        <dynamicField name="*_sf" type="sfloat" indexed="true" stored="true"/>
        <dynamicField name="*_sd" type="sdouble" indexed="true" stored="true"/>
        <dynamicField name="*_dt" type="date" indexed="true" stored="true"/>

利用方法
========

ダイナミックフィールドを利用する場面が多いのはデータベースクロールなどでデータストアクロール設定で登録するなどだと思います。データベースクロールでダイナミックフィールドに登録する方法は、スクリプトに
other\_t = hoge のように記述することで hoge カラムのデータを Solr の
other\_t フィールドに入れることができます。

次にダイナミックフィールドに保存されたデータを Solr から取り出すためには
webapps/fess/WEB-INF/classes/app.dicon
に利用するフィールドを追加する必要があります。以下のように other\_t
を追加します。

::

        <component name="queryHelper" class="jp.sf.fess.helper.impl.QueryHelperImpl">
           <property name="responseFields">new String[]{"id", "score", "boost",
                "contentLength", "host", "site", "lastModified", "mimetype",
                "tstamp", "title", "digest", "url", "other_t" }</property>
        </component>

上記の設定で Solr から値を取得できているので、ページ上に表示するために
JSP
ファイルを編集します。管理画面にログインして、デザインを表示します。検索結果の表示は検索結果ページ（コンテンツ）で表示されるので、この
JSP ファイルを編集します。other\_t の値を表示したい箇所で
${f:h(doc.other\_t)} とすることで登録した値を表示することができます。
