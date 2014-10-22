=================
LibreOfficeの利用
=================

OpenOffice/LibreOfficeの利用
============================

標準のFess環境において、Apache POI を用いた MS Office
系ドキュメントのクロールが可能です。
オフィス系ドキュメントのクロールに関して、OpenOfficeやLibreOfficeを利用して、ドキュメントからより高精度なテキスト抽出も行うことができます。

設定方法
========

JodConverter を Fess
サーバーにインストールします。http://jodconverter.googlecode.com/
から\ `jodconverter-core-3.0-beta-4-dist.zip <http://jodconverter.googlecode.com/files/jodconverter-core-3.0-beta-4-dist.zip>`__\ をダウンロードします。展開して
jar ファイルを Fess サーバーにコピーします。

::

    $ unzip jodconverter-core-3.0-beta-4-dist.zip 
    $ cp jodconverter-core-3.0-beta-4/lib/juh-3.2.1.jar \
    jodconverter-core-3.0-beta-4/lib/jurt-3.2.1.jar \
    jodconverter-core-3.0-beta-4/lib/ridl-3.2.1.jar \
    jodconverter-core-3.0-beta-4/lib/unoil-3.2.1.jar \
    jodconverter-core-3.0-beta-4/lib/jodconverter-core-3.0-beta-4.jar \
    fess-server-9.1.0/webapps/fess/WEB-INF/cmd/lib/
    $ cd fess-server-9.1.0/

次にs2robot\_extractor.diconを作成します。

::

    vi webapps/fess/WEB-INF/classes/s2robot_extractor.dicon 

s2robot\_extractor.diconは以下のような内容でjodExtractorを有効にします。

::

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE components PUBLIC "-//SEASAR//DTD S2Container 2.4//EN"
        "http://www.seasar.org/dtd/components24.dtd">
    <components>
        <component name="tikaExtractor" class="org.seasar.robot.extractor.impl.TikaExtractor"/>
        <component name="msWordExtractor"
            class="org.seasar.robot.extractor.impl.MsWordExtractor"/>
        <component name="msExcelExtractor"
            class="org.seasar.robot.extractor.impl.MsExcelExtractor"/>
        <component name="msPowerPointExtractor"
            class="org.seasar.robot.extractor.impl.MsPowerPointExtractor"/>
        <component name="msPublisherExtractor"
            class="org.seasar.robot.extractor.impl.MsPublisherExtractor"/>
        <component name="msVisioExtractor"
            class="org.seasar.robot.extractor.impl.MsVisioExtractor"/>
        <component name="pdfExtractor" class="org.seasar.robot.extractor.impl.PdfExtractor"/>
        <component name="textExtractor" class="org.seasar.robot.extractor.impl.TextExtractor"/>
        <component name="htmlExtractor" class="org.seasar.robot.extractor.impl.HtmlExtractor"/>
        <component name="xmlExtractor" class="org.seasar.robot.extractor.impl.XmlExtractor"/>
        <component name="htmlXpathExtractor"
            class="org.seasar.robot.extractor.impl.HtmlXpathExtractor">
            <initMethod name="addFeature">
                <arg>"http://xml.org/sax/features/namespaces"</arg>
                <arg>"false"</arg>
            </initMethod>
        </component>
        <component name="officeManagerConfiguration"
            class="org.artofsolving.jodconverter.office.DefaultOfficeManagerConfiguration">
        </component>
        <component name="jodExtractor"
            class="org.seasar.robot.extractor.impl.JodExtractor">
            <property name="officeManager">
                officeManagerConfiguration.setOfficeHome("/usr/lib/libreoffice")
                    .buildOfficeManager()
            </property>
        </component>
        
        <component name="extractorFactory" class="org.seasar.robot.extractor.ExtractorFactory">
            <initMethod name="addExtractor">
                <arg>{
    "application/msword",
    "application/vnd.ms-excel",
    "application/vnd.ms-powerpoint",
    "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
    "application/vnd.openxmlformats-officedocument.presentationml.presentation"
                }</arg>
                <arg>jodExtractor</arg>
            </initMethod>
    ...

設定後、通常通りにクロールしてインデックスを生成します。
