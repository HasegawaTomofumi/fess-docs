==============
非表示検索条件
==============

非表示検索条件
==============

画面上には検索条件の文字列を表示せずに特定の検索条件を引き回したい場合にadditionalパラメータを利用することができます。additionalの値はページングで画面が更新されてもadditionalの値は保持されます。

利用方法
--------

検索が実行される際に (たとえば、検索フォームなど) hidden フォームで
additional
の値を付加して検索を実行すると、ページングで画面遷移しても、その条件を画面に表示することなく、条件を保持することができます。
