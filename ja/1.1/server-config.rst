==============
サーバーの設定
==============

:Date:   2009-10-10

ポートの変更
============

|Fess| がデフォルトで利用するポートは 8080 になります。
変更するには以下の手順で変更します。

Tomcat のポート変更
-------------------

|Fess| が利用している Tomcat のポートを変更します。 変更は conf/server.xml
に記述されている以下のものを変更します。

-  8080: HTTP アクセスポート

-  8005: シャットダウンポート

-  8009: AJP ポート

-  8443: SSL の HTTP アクセスポート (デフォルトは無効)

Solr の設定
-----------

標準構成では、Solr も同じ Tomcat の設定を利用しているので、Tomcat
のポートを変更した場合は、 |Fess| の Solr
サーバーの参照先情報も変更する必要があります。
webapps/fess/WEB-INF/classes/fess\_solr.dicon を変更します。

::

    <arg>"http://localhost:8080/solr"</arg>

Heap メモリーの最大値変更
=========================

インストール環境によっては以下のような OutOfMemory エラーが発生します。

::

    java.lang.OutOfMemoryError: Java heap space

発生した場合は ヒープメモリの最大値を増やしてください。
bin/setenv.[sh\|bat] に -Xmx512m のように追加します(この場合は最大値を
512M に設定)。

::

    Windowsの場合
    ...-Dpdfbox.cjk.support=true -Xmx512m

    Unixの場合
    ...-Dpdfbox.cjk.support=true -Xmx512m"

携帯端末情報の更新
==================

携帯端末情報は `ValueEngine社 <http://valueengine.jp/>`__
より提供されるものを利用しています。
最新の携帯端末情報を利用したい場合は、端末プロファイルをダウンロードして、webapps/fess/WEB-INF/classes/device/
に \_YYYY-MM-DD を取り除いて保存します。
再起動後に変更が有効になります。

::

     ProfileData_YYYY-MM-DD.csv -> ProfileData.csv
     UserAgent_YYYY-MM-DD.csv -> UserAgent.csv
     DisplayInfo_YYYY-MM-DD.csv -> DisplayInfo.csv
