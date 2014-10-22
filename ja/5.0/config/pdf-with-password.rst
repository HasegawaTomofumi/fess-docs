=====================
パスワード付きPDF対応
=====================

暗号化されたPDFの対応
=====================

パスワードが設定されたPDFを検索対象にするためには設定ファイルで対象ファイルのパスワードを登録しておく必要があります．

設定
====

まず、webapps/fess/WEB-INF/classes/s2robot\_extractor.dicon
を以下のように作成します。 今回は，test\_〜.pdf というファイルに pass
というパスワードが設定されている場合です．
対象ファイルが複数ある場合は，addPassword で複数設定します．

::

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE components PUBLIC "-//SEASAR//DTD S2Container 2.4//EN"
        "http://www.seasar.org/dtd/components24.dtd">
    <components>
        <component name="tikaExtractor" class="org.seasar.robot.extractor.impl.TikaExtractor"/>
        <component name="msWordExtractor" class="org.seasar.robot.extractor.impl.MsWordExtractor"/>
        <component name="msExcelExtractor" class="org.seasar.robot.extractor.impl.MsExcelExtractor"/>
        <component name="msPowerPointExtractor" class="org.seasar.robot.extractor.impl.MsPowerPointExtractor"/>
        <component name="msPublisherExtractor" class="org.seasar.robot.extractor.impl.MsPublisherExtractor"/>
        <component name="msVisioExtractor" class="org.seasar.robot.extractor.impl.MsVisioExtractor"/>
        <component name="pdfExtractor" class="org.seasar.robot.extractor.impl.PdfExtractor">
            <initMethod name="addPassword">
                <!-- 正規表現で対象ファイルのパスを指定 -->
                <arg>".*test_.*.pdf"</arg>
                <!-- パスワード -->
                <arg>"pass"</arg>
            </initMethod>
        </component>
        <component name="textExtractor" class="org.seasar.robot.extractor.impl.TextExtractor"/>
        <component name="htmlExtractor" class="org.seasar.robot.extractor.impl.HtmlExtractor"/>
        <component name="xmlExtractor" class="org.seasar.robot.extractor.impl.XmlExtractor"/>
        <component name="htmlXpathExtractor" class="org.seasar.robot.extractor.impl.HtmlXpathExtractor">
            <initMethod name="addFeature">
                <arg>"http://xml.org/sax/features/namespaces"</arg>
                <arg>"false"</arg>
            </initMethod>
        </component>

        <component name="extractorFactory" class="org.seasar.robot.extractor.ExtractorFactory">
            <initMethod name="addExtractor">
                <arg>{
    "application/xml",
    "application/xhtml+xml",
    "application/rdf+xml",
    "text/xml",
    "text/xml-external-parsed-entity"
                }</arg>
                <arg>xmlExtractor</arg>
            </initMethod>
            <initMethod name="addExtractor">
                <arg>{
    "text/html"
                }</arg>
                <arg>xmlExtractor</arg>
            </initMethod>
            <initMethod name="addExtractor">
                <arg>{
    "application/pdf"
                }</arg>
                <arg>pdfExtractor</arg>
            </initMethod>
            <initMethod name="addExtractor">
                <arg>{
    "image/svg+xml",
    "application/x-tika-msoffice",
    "application/vnd.visio",
    "application/vnd.ms-powerpoint",
    "application/vnd.ms-excel",
    "application/vnd.ms-excel.sheet.binary.macroenabled.12",
    "application/msword",
    "application/vnd.ms-outlook",
    "application/x-tika-ooxml",
    "application/vnd.openxmlformats-officedocument.presentationml.presentation",
    "application/vnd.ms-powerpoint.presentation.macroenabled.12",
    "application/vnd.openxmlformats-officedocument.presentationml.template",
    "application/vnd.openxmlformats-officedocument.presentationml.slideshow",
    "application/vnd.ms-powerpoint.slideshow.macroenabled.12",
    "application/vnd.ms-powerpoint.addin.macroenabled.12",
    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
    "application/vnd.ms-excel.sheet.macroenabled.12",
    "application/vnd.openxmlformats-officedocument.spreadsheetml.template",
    "application/vnd.ms-excel.template.macroenabled.12",
    "application/vnd.ms-excel.addin.macroenabled.12",
    "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
    "application/vnd.ms-word.document.macroenabled.12",
    "application/vnd.openxmlformats-officedocument.wordprocessingml.template",
    "application/vnd.ms-word.template.macroenabled.12",
    "application/x-asp",
    "application/rtf",
    "text/plain",
    "application/vnd.sun.xml.writer",
    "application/vnd.oasis.opendocument.text",
    "application/vnd.oasis.opendocument.graphics",
    "application/vnd.oasis.opendocument.presentation",
    "application/vnd.oasis.opendocument.spreadsheet",
    "application/vnd.oasis.opendocument.chart",
    "application/vnd.oasis.opendocument.image",
    "application/vnd.oasis.opendocument.formula",
    "application/vnd.oasis.opendocument.text-master",
    "application/vnd.oasis.opendocument.text-web",
    "application/vnd.oasis.opendocument.text-template",
    "application/vnd.oasis.opendocument.graphics-template",
    "application/vnd.oasis.opendocument.presentation-template",
    "application/vnd.oasis.opendocument.spreadsheet-template",
    "application/vnd.oasis.opendocument.chart-template",
    "application/vnd.oasis.opendocument.image-template",
    "application/vnd.oasis.opendocument.formula-template",
    "application/x-vnd.oasis.opendocument.text",
    "application/x-vnd.oasis.opendocument.graphics",
    "application/x-vnd.oasis.opendocument.presentation",
    "application/x-vnd.oasis.opendocument.spreadsheet",
    "application/x-vnd.oasis.opendocument.chart",
    "application/x-vnd.oasis.opendocument.image",
    "application/x-vnd.oasis.opendocument.formula",
    "application/x-vnd.oasis.opendocument.text-master",
    "application/x-vnd.oasis.opendocument.text-web",
    "application/x-vnd.oasis.opendocument.text-template",
    "application/x-vnd.oasis.opendocument.graphics-template",
    "application/x-vnd.oasis.opendocument.presentation-template",
    "application/x-vnd.oasis.opendocument.spreadsheet-template",
    "application/x-vnd.oasis.opendocument.chart-template",
    "application/x-vnd.oasis.opendocument.image-template",
    "application/x-vnd.oasis.opendocument.formula-template",
    "image/bmp",
    "image/gif",
    "image/jpeg",
    "image/png",
    "image/tiff",
    "image/vnd.wap.wbmp",
    "image/x-icon",
    "image/x-psd",
    "image/x-xcf",
    "application/zip",
    "application/x-tar",
    "application/x-gtar",
    "application/x-gzip",
    "application/x-bzip",
    "application/x-bzip2",
    "application/java-vm",
    "audio/mpeg",
    "application/x-midi",
    "audio/midi",
    "audio/basic",
    "audio/x-wav",
    "audio/x-aiff",
    "application/mbox",
    "text/calendar",
    "text/css",
    "text/csv",
    "text/directory",
    "text/dns",
    "text/ecmascript",
    "text/enriched",
    "text/example",
    "text/javascript",
    "text/parityfec",
    "text/prs.fallenstein.rst",
    "text/prs.lines.tag",
    "text/red",
    "text/rfc822-headers",
    "text/richtext",
    "text/rtf",
    "text/rtp-enc-aescm128",
    "text/rtx",
    "text/sgml",
    "text/t140",
    "text/tab-separated-values",
    "text/troff",
    "text/ulpfec",
    "text/uri-list",
    "text/vnd.abc",
    "text/vnd.curl",
    "text/vnd.curl.dcurl",
    "text/vnd.curl.mcurl",
    "text/vnd.curl.scurl",
    "text/vnd.dmclientscript",
    "text/vnd.esmertec.theme-descriptor",
    "text/vnd.fly",
    "text/vnd.fmi.flexstor",
    "text/vnd.graphviz",
    "text/vnd.in3d.3dml",
    "text/vnd.in3d.spot",
    "text/vnd.iptc.newsml",
    "text/vnd.iptc.nitf",
    "text/vnd.latex-z",
    "text/vnd.motorola.reflex",
    "text/vnd.ms-mediapackage",
    "text/vnd.net2phone.commcenter.command",
    "text/vnd.si.uricatalogue",
    "text/vnd.sun.j2me.app-descriptor",
    "text/vnd.trolltech.linguist",
    "text/vnd.wap.si",
    "text/vnd.wap.sl",
    "text/vnd.wap.wml",
    "text/vnd.wap.wmlscript",
    "text/x-asm",
    "text/x-c",
    "text/x-diff",
    "text/x-fortran",
    "text/x-java-source",
    "text/x-pascal",
    "text/x-setext",
    "text/x-uuencode",
    "text/x-vcalendar",
    "text/x-vcard",
    "application/x-sh"
                }</arg>
                <arg>tikaExtractor</arg>
            </initMethod>
        </component>

    </components>

次に、webapps/fess/WEB-INF/classes/s2robot\_rule.dicon
に以下を編集します。

::

    ...
        <component name="fsFileRule" class="org.seasar.robot.rule.impl.RegexRule" >
            <property name="ruleId">"fsFileRule"</property>
            <property name="responseProcessor">
                <component class="org.seasar.robot.processor.impl.DefaultResponseProcessor">
                    <property name="transformer">fessFileTransformer</property>
                </component>
            </property>
            <property name="allRequired">true</property>
            <initMethod name="addRule">
                <arg>"url"</arg>
                <arg>"file:.*"</arg>
            </initMethod>
            <initMethod name="addRule">
                <arg>"mimeType"</arg>
                <!-- Supported MIME type -->
                <arg>
      "(application/xml"
    + "|application/xhtml+xml"
    + "|application/rdf+xml"
    + "|application/pdf"
    + "|text/xml"
    + "|text/xml-external-parsed-entity"
    + "|text/html)"
                </arg>
            </initMethod>
        </component>
    ...

上記を設定したら、Fess
を起動してクロールを実行してください。基本的な利用方法は特に変わりません。
