---
ms.openlocfilehash: 56ee26dd77bb1b678b54b6776741f6547889fa08
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040419"
---
<a name="1140--2015-06-30"></a>1.14.0/2015 年 6 月 30 日
==================

## <a name="core"></a>コア
  * 使用されていない removeAttrs メソッドの削除
  * URL メソッドの正規表現の置換
  * $.extend で上書きされる $.ajax の不正な URL パラメーターの削除
  * 入れ子になった [cancel submit]\(送信のキャンセル\) ボタンの処理の改善
  * インデントの修正
  * ノーマライザーを共有するように attributeRules および dataRules をリファクタリング
  * 数値入力で値を数値に変換する dataRules メソッド
  * プロトコルの相対 URL を使用できるように URL メソッドを更新
  * 非推奨の $.format プレースホルダーの削除
  * jQuery 1.7 以降の on/off の使用および destroy メソッドの追加
  * $.inArray に対する IE8 の .indexOf の互換性を変更
  * Opera Mini の undefined に対して NaN 値をキャストするように変更
  * required メソッド内での値のトリミングの停止
  * 無効になった要素のマッチングに :disabled セレクターを使用するように変更
  * フィールドの再検証防止のため一部のキーボード キーを除外
  * DOM 全体でのラジオ ボタン/チェックボックス要素の検索を無効化
  * 不正な rule メソッドに対してスローされるエラーの改善
  * 数値検証エラーの修正
  * whatwg 仕様への参照の修正
  * カスタムの入力セットの検証時に無効な要素へフォーカス
  * カスタムの highlight メソッドを使用する場合に要素スタイルをリセット
  * エラー ID のドル記号のエスケープ
  * "無効なフィールドおよび読み取り専用フィールドの無視" の取り消し
  * Luhn アルゴリズムに関するコメントのリンクの更新

## <a name="additionals"></a>追加のメソッド
  * アドレスのタイムゾーンに関する問題への dateITA の追加
  * 拡張メソッドを "メソッド." のみに修正
  * 受け入れメソッドを "." のみとマッチングするように修正
  * 1 桁の時間を使用できるように time メソッドを修正
  * notEqualTo メソッドの不正なテストのドロップ
  * notEqualTo メソッドの追加
  * `$` による適切な jQuery 参照の使用
  * iban メソッドの無用になった正規表現チェックの削除
  * ブラジルの CPF 数

## <a name="localization"></a>ローカリゼーション
  * messages_tr.js の更新
  * messages_sr_lat.js の更新
  * スペイン語 (ペルー) (ES PE) の追加
  * グルジア語 (ქართული、ge) の追加
  * カタロニア語翻訳のタイポの修正
  * フィンランド語 (fi) 翻訳の改善
  * アルメニア語 (hy_AM) ロケールの追加
  * イタリア語 (it) 翻訳への currency メソッドの追加
  * bn_BD ロケールの追加
  * zh ロケールの更新
  * イタリア語メッセージの末尾のピリオドの削除

<a name="1131--2014-10-14"></a>1.13.1/2014 年 10 月 14 日
==================

## <a name="core"></a>コア
  * autoCreateRanges の値に 0 を使用できるように変更
  * すべての validationTargetFor 要素に無視設定を適用
  * min/max/rangelength メソッドでの値のトリミングの無効化
  * ID/名前を errorsFor でセレクターとして使用する前にエスケープ
  * focusCleanup オプションの明示的な既定値
  * describedby マッチャーの RegExp の誤りの修正
  * 無効なフィールドおよび読み取り専用フィールドの無視
  * エスケープされた ID が describedby に格納されるように ID のエスケープを改善
  * submitHandler の戻り値を使用したフォームの送信の許可/禁止

## <a name="additionals"></a>追加のメソッド
  * postalcodeBR メソッドの追加
  * パラメーターが文字列の場合の pattern メソッドの修正


<a name="1130--2014-07-01"></a>1.13.0/2014 年 7 月 1 日
==================

## <a name="all"></a>すべて
* プラグイン UMD ラッパーの追加

## <a name="core"></a>コア
* エラーのない aria-describedby および空白の非表示エラーの考慮
* dateISO の RegExp の改善
* click イベントのデリゲートへのラジオ ボタン/チェックボックスの追加
* ラベル以外の要素に対する aria-describedby の使用
* ラジオ ボタン/チェックボックスに focusin、focusout、keyup も登録
* rangelength 属性値の正規化の修正
* type が "number" のフィールドも処理するように elementValue メソッドを修正
* IE8(?) のサポートのために文字列に対して配列表記ではなく charAt を使用するように変更

## <a name="localization"></a>ローカリゼーション
* rangelength メソッドのスロバキア語翻訳の修正
* フィンランド語メソッドの追加
* ガリシア語の数値検証メッセージの修正
* スペイン語の number メソッド検証メッセージの修正
* ガリシア語 (GL) の追加
* min メソッドおよび max メソッドのフランス語メッセージの修正

## <a name="additionals"></a>追加のメソッド
* statesUS メソッドの追加
* DST のバグを処理するように dateITA メソッドを修正
* ペルシャ語の date メソッドの追加
* postalCodeCA メソッドの追加
* postalcodeIT メソッドの追加

<a name="1120--2014-04-01"></a>1.12.0/2014 年 4 月 1 日
==================

* ARIA テスト ([3d5658e](https://github.com/jzaefferer/jquery-validation/commit/3d5658e9e4825fab27198c256beed86f0bd12577)) の追加
* スペイン語 (アルゼンチン) のローカリゼーション メッセージの追加。 ([7b30beb](https://github.com/jzaefferer/jquery-validation/commit/7b30beb8ebd218c38a55d26a63d529e16035c7a2))
* "es" および "es_AR" のメッセージに不足していたピリオドの追加。 ([a2a653c](https://github.com/jzaefferer/jquery-validation/commit/a2a653cb68926ca034b4b09d742d275db934d040))
* インドネシア語 (ID) のローカリゼーションの追加 ([1d348bd](https://github.com/jzaefferer/jquery-validation/commit/1d348bdcb65807c71da8d0bfc13a97663631cd3a))。
* NIF、NIE、CIF のスペイン語ドキュメント番号検証の追加 ([#830](https://github.com/jzaefferer/jquery-validation/issues/830), [317c20f](https://github.com/jzaefferer/jquery-validation/commit/317c20fa9bb772770bb9b70d46c7081d7cfc6545))
* リモートの ajax 要求のコンテキストへの現在のフォームの追加 ([0a18ae6](https://github.com/jzaefferer/jquery-validation/commit/0a18ae65b9b6d877e3d15650a5c2617a9d2b11d5))
* その:IBAN メソッドの末尾の空白文字を更新 ([#970](https://github.com/jzaefferer/jquery-validation/issues/970)、 [347b04a](https://github.com/jzaefferer/jquery-validation/commit/347b04a7d4e798227405246a5de3fc57451d52e1))
* BIC メソッド:正規表現を向上させる{1}が常に冗長です。 gh-744 ([5cad6b4](https://github.com/jzaefferer/jquery-validation/commit/5cad6b493575e8a9a82470d17e0900c881130873)) の終了
* Bower:パッケージ登録用の Bower.json の追加 ([e86ccb0](https://github.com/jzaefferer/jquery-validation/commit/e86ccb06e301613172d472cf15dd4011ff71b398))
* jQuery.noConflict との互換性のため "jQuery" に対するドルの参照を変更しました。 gh-754 ([2049afe](https://github.com/jzaefferer/jquery-validation/commit/2049afe46c1be7b3b89b1d9f0690f5bebf4fbf68)) の終了
* コア:エラー一覧のエントリに"method"フィールドを追加 ([89a15c7](https://github.com/jzaefferer/jquery-validation/commit/89a15c7a4b17fa2caaf4ff817f09b04c094c3884))
* コア:Data-msg 属性を使用した汎用メッセージのサポートが追加されました ([5bebaa5](https://github.com/jzaefferer/jquery-validation/commit/5bebaa5c55c73f457c0e0181ec4e3b0c409e2a9d))
* コア:値が 0 の属性 (例: min = '0') ([#854](https://github.com/jzaefferer/jquery-validation/issues/854)、 [9dc0d1d](https://github.com/jzaefferer/jquery-validation/commit/9dc0d1dd946b2c6178991fb16df0223c76162579))
* コア:非推奨の $.format の無効化 ([#755](https://github.com/jzaefferer/jquery-validation/issues/755)、 [bf3b350](https://github.com/jzaefferer/jquery-validation/commit/bf3b3509140ea8ab5d83d3ec58fd9f1d7822efc5))
* コア:複数のエラー クラスのサポートの修正 ([c1f0baf](https://github.com/jzaefferer/jquery-validation/commit/c1f0baf36c21ca175bbc05fb9345e5b44b094821))
* コア:無視された要素にイベントを無視 ([#700](https://github.com/jzaefferer/jquery-validation/issues/700)、 [a864211](https://github.com/jzaefferer/jquery-validation/commit/a86421131ea69786ee9e0d23a68a54a7658ccdbf))
* コア:ElementValue メソッドの改善 ([6c041ed](https://github.com/jzaefferer/jquery-validation/commit/6c041edd21af1425d12d06cdd1e6e32a78263e82))
* コア:Element() ハンドルが無視される要素を正しくください。 ([3f464a8](https://github.com/jzaefferer/jquery-validation/commit/3f464a8da49dbb0e4881ada04165668e4a63cecb))
* コア:DataRules 解析 W3C HTML5 仕様のスタイルを切り替える ([460fd22](https://github.com/jzaefferer/jquery-validation/commit/460fd22b6c84a74c825ce1fa860c0a9da20b56bb))
* コア:省略可能で成功をトリガーが、他の成功検証コントロール ([#851](https://github.com/jzaefferer/jquery-validation/issues/851)、 [f93e1de](https://github.com/jzaefferer/jquery-validation/commit/f93e1deb48ec8b3a8a54e946a37db2de42d3aa2a))
* コア:代わりにプレーンな要素を使用してラップ要素をもう一度 ([03cd4c9](https://github.com/jzaefferer/jquery-validation/commit/03cd4c93069674db5415a0bf174a5870da47e5d2))
* コア: remote が最後に実行されるように変更 ([#711](https://github.com/jzaefferer/jquery-validation/issues/711)、[ad91b6f](https://github.com/jzaefferer/jquery-validation/commit/ad91b6f388b7fdfb03b74e78554cbab9fd8fca6f))
* デモ:マルチパートのデモでは、適切なオプションを使用します。 ([#1025](https://github.com/jzaefferer/jquery-validation/issues/1025)、[070edc7](https://github.com/jzaefferer/jquery-validation/commit/070edc7be4de564cb74cfa9ee4e3f40b6b70b76f))
* 追加のメソッドでの $/jQuery の使用箇所の修正。 #839 の修正 ([#839](https://github.com/jzaefferer/jquery-validation/issues/839)、[59bc899](https://github.com/jzaefferer/jquery-validation/commit/59bc899e4586255a4251903712e813c21d25b3e1))
* 中国語の翻訳の改善 ([1a0bfe3](https://github.com/jzaefferer/jquery-validation/commit/1a0bfe32b16f8912ddb57388882aa880fab04ffe))
* aria-required の初回実装 ([bf3cfb2](https://github.com/jzaefferer/jquery-validation/commit/bf3cfb234ede2891d3f7e19df02894797dd7ba5e))
* ローカリゼーション: 受け入れ値を拡張へ変更しました。 #771 の修正および gh-793 の終了。 ([#771](https://github.com/jzaefferer/jquery-validation/issues/771)、[12edec6](https://github.com/jzaefferer/jquery-validation/commit/12edec66eb30dc7e86756222d455d49b34016f65))
* メッセージ:アイスランド語のローカリゼーションの追加 ([dc88575](https://github.com/jzaefferer/jquery-validation/commit/dc885753c8872044b0eaa1713cecd94c19d4c73d))
* メッセージ:"Bg"、"fr"および"sr"のメッセージに不足していたピリオドを追加します。 ([adbc636](https://github.com/jzaefferer/jquery-validation/commit/adbc6361c377bf6b74c35df9782479b1115fbad7))
* メッセージ:Create messages_sr_lat.js ([f2f9007](https://github.com/jzaefferer/jquery-validation/commit/f2f90076518014d98495c2a9afb9a35d45d184e6))
* メッセージ:Messages_tj.js ([de830b3](https://github.com/jzaefferer/jquery-validation/commit/de830b3fd8689a7384656c17565ee92c2878d8a5))
* メッセージ:Sr_lat の翻訳の修正、不足している領域を追加 ([880ba1c](https://github.com/jzaefferer/jquery-validation/commit/880ba1ca545903a41d8c5332fc4038a7e9a580bd))
* メッセージ:Messages_sr.js を更新、修正領域が不足している ([10313f4](https://github.com/jzaefferer/jquery-validation/commit/10313f418c18ea75f385248468c2d3600f136cfb))
* メソッド:通貨の他のメソッドを追加 ([1a981b4](https://github.com/jzaefferer/jquery-validation/commit/1a981b440346620964c87ebdd0fa03246348390e))
* メソッド:StripHTML の区切り記号削除へのスマート クォートの追加 ([aa0d624](https://github.com/jzaefferer/jquery-validation/commit/aa0d6241c3ea04663edc1e45ed6e6134630bdd2f))
* メソッド:DateITA メソッドをサマータイムのエラーを修正 ([279b932](https://github.com/jzaefferer/jquery-validation/commit/279b932c1267b7238e6652880b7846ba3bbd2084))
* メソッド:メソッド (チリ) のカルチャ (ES-CL) のローカライズ ([cf36b93](https://github.com/jzaefferer/jquery-validation/commit/cf36b933499e435196d951401221d533a4811810))
* メソッド:HTML5 正規表現を使用し email2 メソッドを削除するメールの更新 ([#828](https://github.com/jzaefferer/jquery-validation/issues/828)、 [dd162ae](https://github.com/jzaefferer/jquery-validation/commit/dd162ae360639f73edd2dcf7a256710b2f5a4e64))
* メソッドのパターン:HTML5 実装はこれらのいずれかに含めないため、区切り記号を削除します。 ([37992c1](https://github.com/jzaefferer/jquery-validation/commit/37992c1c9e2e0be8b315ccccc2acb74863439d3e))
* 長さのチェックを行うようにクレジット カード検証を制限しました。 gh-772 の 終了 ([f5f47c5](https://github.com/jzaefferer/jquery-validation/commit/f5f47c5c661da5b0c0c6d59d169e82230928a804))
* messages_ko.js の更新および gh-715 の終了 ([5da3085](https://github.com/jzaefferer/jquery-validation/commit/5da3085ff02e0e6ecc955a8bfc3bb9a8d220581b))
* messages_pt_BR.js の更新。 gh-782 の終了 ([4bf813b](https://github.com/jzaefferer/jquery-validation/commit/4bf813b751ce34fac3c04eaa2e80f75da3461124))
* 新しいプレフィックスを受け付けるように phonesUK および mobileUK を更新しました。 gh-750 の終了 ([d447b41](https://github.com/jzaefferer/jquery-validation/commit/d447b41b830dee984be21d8281ec7b87a852001d))
* 9 桁の郵便番号の検証。 gh-726 の終了 ([165005d](https://github.com/jzaefferer/jquery-validation/commit/165005d4b5780e22d13d13189d107940c622a76f))
* phoneUS:N11 を追加します。 gh-861 の終了 ([519bbc6](https://github.com/jzaefferer/jquery-validation/commit/519bbc656bcb26e8aae5166d7b2e000014e0d12a))
* aria-invalid 値をクリアするように resetForm を変更しました ([4f8a631](https://github.com/jzaefferer/jquery-validation/commit/4f8a631cbe84f496ec66260ada52db2aa0bb3733))
* valid():すべての要素を確認します。 #791 を修正し、valid() で最初の (無効な) 要素のみが検証されるように変更 ([#791](https://github.com/jzaefferer/jquery-validation/issues/791)[6f26803](https://github.com/jzaefferer/jquery-validation/commit/6f268031afaf4e155424ee74dd11f6c47fbb8553))

<a name="1111--2013-03-22"></a>1.11.1/2013 年 3 月 22 日
==================

  * range メソッドのパラメーターも数値に変換するように修正しました。 gh-702 の終了
  * PHP の使用箇所のほとんどを mockjax ハンドラーに置換しました。 いくつかのデモのクリーンアップを行い、新しい masked-input プラグインに更新しました。 PHP には captcha のデモを残しています。 #662 の修正
  * ミルクのデモから強調表示のインライン コードを削除しました。 ソースが正常に動作することを確認しました。
  * テンプレートの内容を jQuery コンストラクターへ渡す前に空白をトリミングするように dynamic-totals のデモを修正
  * min/max の検証を修正しました。 gh-666 を終了しました。 #648 の修正
  * ルールとして表示され、ルールによる更新中に例外の原因となっていた "メッセージ" を修正 ("追加") しました。 gh-670 の終了および #624 の修正
  * 韓国語 (ko) のローカリゼーションを追加しました。 gh-671 の終了
  * より多くの無効な郵便番号を除外するように英国の postcode メソッドを改善しました。 #682 の終了
  * messages_sv.js を更新しました。 #683 の終了
  * Grunt のリンクをプロジェクト Web サイトに変更しました。 #684 の終了
  * 他のすべてのメソッドがフィールドに適用されてから最後に実行されるように、リモート メソッドを一覧の最後に移動しました。 #679 の修正
  * plugin.json の説明を更新し "検証" という語句を追加
  * タイポの修正
  * jQuery ローダーをローダー自体のパスを使用するように修正しました。 入れ子になったデモを修正しました。
  * ノード モジュール "phantomjs" でのインストール時に PhantomJS 1.8 を使用するよう grunt-contrib-qunit を更新
  * 0 または 1 ではなくブール値を返すように valid() を変更しました。 #109 の修正 - valid() でブール値が返されない

<a name="1110--2013-02-04"></a>1.11.0/2013年 2 月 4 日
==================

  * `min`、`max`、`range` 規則の数値としてのクリアを削除しました。 #455 を修正しました。 gh-528 を終了しました。
  * 既存のラベルの更新 - #430 の修正および gh 436 の終了
  * 少なくとも IE8 および 9 で -bash が一致内容と置換されるグループ補間が行われないように、$.validator.format を修正しました。 #614 の修正
  * mimeType の正規表現の修正
  * MIT にのみプラグイン マニフェストを追加してヘッダーを更新し、不要なデュアルライセンス (jQuery など) を削除しました。
  * ヘブライ語のメッセージ:修正プログラムの gh 568 の文の最後のドット削除
  * require_from_group 検証をフランス語に翻訳しました。 gh-573 を修正しました。
  * グループを配列または文字列に設定できるように変更 - #479 の修正
  * 複数の MIME の種類でスペースを削除
  * いくつかの日付検証および JS 構文エラーを修正しました。
  * メタデータ プラグインのサポートを削除し、data-rule- および data-msg- (907467e8 で追加) プロパティに置き換えました。
  * 有効な URL パターンとして sftp を追加
  * マレー語 (my) のローカリゼーションの追加
  * localization/messages_hu.js の更新
  * focusin/focusout ポリフィルを削除しました。 #542 の修正 - IE9 で jquery.validate を追加すると focusin イベントおよび focusout イベントが妨害される
  * ローカリゼーション:フィンランド語翻訳のタイポの修正
  * 有効から無効に戻った際に無効のアイコンを表示するように RTM デモを修正
  * 入力が速すぎる場合に ajax 呼び出しを実行不可能にしていた、リモート関数で値が返されるのが早すぎる問題を修正しました。 リモート検証で常に最新の値が検証されるように変更しました。
  * #244 の修正を取り消しました。 #521 の修正 - テキストがフィールドに入力されるとすぐに電子メールの検証が行われていました。

<a name="1100--2012-09-07"></a>1.10.0/2012 年 9 月 7 日
===================

  * コミュニティからのフィードバックに基づいて nowhitespace、phoneUS、phoneUK、mobileUK のフランス語文字列を修正しました。
  * 台湾の言語は中国語 (zh) であり地域は台湾 (TW) であることから、ISO_3166-1 標準 (http://en.wikipedia.org/wiki/ISO_3166-1)) に従って language_REGION のファイルの名前を変更
  * 特に英国の電話番号について正規表現パターンを最適化しました。
  * 各ファイルに言語名を追加し、エストニア語、グルジア語、ウクライナ語、中国語の言語コードの名前を ISO 639 標準 (http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)) に従って変更
  * クロアチア語 (HR) のローカリゼーションの追加
  * 既存のフランス語翻訳を編集し、追加のメソッドについてフランス語翻訳を追加しました。
  * data 属性でのカスタム エラー メッセージの指定に関する変更に統合
  * 英国の携帯電話番号を新しい番号に合わせて更新しました。 #154 の修正
  * テストが設定された成功呼び出しに要素を追加しました。 #60 の修正
  * 追加の time メソッドの正規表現を修正しました。 #131 の修正
  * resetForm で form 要素の古い previousValue がクリアされるようになりました。 #312 の修正
  * require_from_group にチェックボックス テストを追加し、elementValue を使用するように require_from_group を変更しました。 #359 の修正
  * jQuery 1.5.2 以降の dataFilter の応答に関する問題を修正しました。 #405 の修正
  * jQuery Mobile のデモを追加しました。 #249 の修正
  * 正確性のために findByName の最適化を解除しました。 #82 の修正 - IE7 での $.validator.prototype.findByName による中断
  * 米国の郵便番号のサポートおよびテストを追加しました。 #90 の修正
  * タブまたは空の要素に対する検証が省略されるように、keyup の lastElement を lastActive に変更しました。 #244 の修正
  * stripHtml から番号除去を削除しました。 #2 の修正
  * 無効/有効のリモート検証での無効なカウントを修正しました。 #286 の修正
  * デモのインデックスに file_input へのリンクを追加
  * 古い 受け入れメソッドを追加の拡張メソッドに移行し、標準ブラウザーの mimetype フィルタリングを処理する新しい受け入れメソッドを追加しました。 #287 の修正および #369 の無効化
  * onfocusout が [false] に設定された場合に blur イベントを無効化しました。 テストを追加しました。
  * ラジオ ボタンおよびチェックボックスの値の問題を修正しました。 #363 の修正
  * rangeWords のテストを追加し、メソッドの正規表現およびバインドを修正しました。 #308 の修正
  * TinyMCE デモを修正しデモ ページにリンクを追加しました。 #382 の修正
  * min/max のローカリゼーション メッセージを変更しました。#273 の修正
  * 既定の空白の type 属性に関する問題を修正するため、テキスト入力タイプの疑似セレクターを追加しました。 テストおよびいくつかのテスト マークアップを追加しました。 #217 の修正
  * dynamic-totals デモのデリゲート バグを修正しました。 #51 の修正
  * 英数字検証コントロールの誤ったメッセージの修正
  * required 属性に対する間違った false チェックの削除
  * 非 HTML5 ブラウザーの required 属性を修正しました。 #301 の修正
  * メソッド "require_from_group" および "skip_or_fill_minimum" の追加
  * スウェーデン語の ISO コードを正しいものに変更
  * HTML5 DOCTYPE を使用するようにデモ HTML ファイルを更新
  * 先頭にゼロのない 10 進数の正規表現の問題を修正しました。 新しいメソッド テストを追加しました。 #41 の修正
  * 文字列値のみを正規化する (複数選択の配列値は操作しない) elementValue メソッドを導入しました。 #116 の修正
  * 動的に追加された送信ボタンのサポートを追加し、テスト ケースを更新しました。 validateDelegate を使用するように変更しました。 PR #9 のコード
  * テスト フィクスチャの不適切な二重引用符の修正
  * 上限を除外ではなく含めるように maxWords メソッドを修正しました。 #284 の修正
  * ドイツ語の範囲検証コントロール メッセージの文法ミスを修正しました。 #315 の修正
  * errorClass オプションでの複数のクラス名の処理を修正しました。 Max Lynch によりテストしました。 #280 の修正
  * $.validator.format を必須とするように jQuery.format の使用方法を修正しました。 #329 の修正
  * "すべての" 英国の電話番号と英国の郵便番号用のメソッド
  * メソッドのパターン:文字列パラメーターを RegExp に変換します。 問題 #223 の修正
  * ドイツ語のローカリゼーション ファイルの文法ミス
  * メッセージへのエストニア語のローカリゼーションの追加
  * themerollered デモに関するツールヒントの改善
  * qSA を満たす属性がない入力フィールドへの type="text" の追加
  * ツールヒントを使用してオーバーレイをエラーとして表示するように themerollered デモを更新しました。
  * 最新の jQuery UI を (新しい jQuery バージョンと合わせて) 使用するように themerollered デモを更新しました。 ページのロード速度を改善するためにコードを移動させました。
  * 分割されていた日本語の min のエラー メッセージを修正しました。
  * フォーム プラグインを最新バージョンに更新しました。 ajaxSubmit デモを拡張しました。
  * classRuleSettings から、ローカライズされたメソッドに移行されていない dateDE および numberDE メソッドを削除
  * submitHandler コールバックへの送信イベントの受け渡し
  * #219 の修正 - dependency-callback または dependency-expression が設定された要素の valid() を修正しました。
  * 最新リリースのみが zip 形式化されるように dist dir を削除してビルドを改善

<a name="190"></a>1.9.0
---
* バスク語 (EU) のローカリゼーションの追加
* スロベニア語 (SL) のローカリゼーションの追加
* 問題 #127 の修正 - フィンランド語の翻訳で ; の代わりに : が使用されている
* ロシア語のローカリゼーションでの軽微な構文の問題の修正
* HTML5 入力タイプのサポートの追加および #97 の修正
* フォームに novalidate 属性を設定し type 属性を読み取るようにすることで HTML5 のサポートを改善しました。
* error 要素からすべてのクラスを削除し showLabel() を修正しました。 settings.validClass のみを削除しました。 #151 の修正
* 追加のメソッドに、任意の正規表現の検証を行う "pattern" を追加しました。
* 末尾のピリオド (RFC では有効ですがこのメソッドでは不適切) を許可しないように email メソッドを改善しました。 #143 の修正
* min と max メッセージが入れ替わっていたスウェーデン語およびノルウェー語の翻訳を修正しました。 #181 の修正
* #184 の修正 - resetForm: lastElement の設定を解除する必要がある
* #71 の修正 - 既存の time メソッドの改善および 12 時間 AM/PM 形式用の time12h メソッドの追加
* #177 の修正 - 単一のラジオ ボタンまたはチェックボックス入力に関する検証の修正
* #189 の修正- :hidden 要素が既定で無視されるようになりました
* #194 の修正 - jQuery 1.6 以降では属性として必須 - .attr の代わりに .prop を使用
* #47、#39、#32 の修正 - クレジット カード番号に、スペースおよびダッシュ (多くのユーザーがスペースを入力します) を含めることができるようになりました。

<a name="181"></a>1.8.1
---
* タイ語 (TH) のローカリゼーションの追加および #85 の修正
* ベトナム語 (VI) のローカリゼーションの追加 (協力: Ngoc)
* 問題 #78 を修正しました。 必須検証では同一グループのラジオ ボタンすべてにエラー/有効なスタイル設定が適用されます。
* form.elements は jQuery 1.6 でのサポートが終了したため使用しないでください。 これには多くのバグが含まれています (IE6 - 8: form.elements === form)。

<a name="180"></a>1.8.0
---
* NL ローカリゼーションを改善 (http://plugins.jquery.com/node/14120))
* グルジア語 (GE) のローカリゼーションの追加 (協力: Avtandil Kikabidze)
* セルビア語 (SR) のローカリゼーションの追加 (協力: Aleksandar Milovac)
* 追加のメソッドへの ipv4 および ipv6 の追加 (協力: Natal Ngétal)
* 日本語 (JA) のローカリゼーションの追加 (協力: Bryan Meyerovich)
* カタロニア語 (CA) のローカリゼーションの追加 (協力: Xavier de Pedro)
* for-in にループに不足していた var ステートメントの修正
* 書式設定されたメッセージの処理が正しく行われないリモート検証を修正 (https://github.com/jzaefferer/jquery-validation/issues/11))
* jQuery 1.5.1 との後方互換性を維持したままこの互換性のバグを修正

<a name="17"></a>1.7
---
* リトアニア語 (LT) のローカリゼーションの追加
* ギリシャ語 (EL) のローカリゼーションの追加 (http://plugins.jquery.com/node/12319))
* ラトビア語 (LV) のローカリゼーションの追加 (http://plugins.jquery.com/node/12349))
* ヘブライ語 (HE) のローカリゼーションの追加 (http://plugins.jquery.com/node/12039))
* スペイン語 (ES) のローカリゼーションの修正 (http://plugins.jquery.com/node/12696))
* jQuery UI の themerolled デモの追加
* cmxform.js の削除
* 不足していた 4 つのセミコロンの修正 (http://plugins.jquery.com/node/12639)
* additional-methods.js の phone-method の名前を phoneUS に変更
* additional-methods.js への phoneUK メソッドおよび mobileUK メソッドの追加 (http://plugins.jquery.com/node/12359))
* 単一要素で rules-method を使用する場合に複数のフォームを変更できないようにする詳細拡張オプション (http://plugins.jquery.com/node/12411))
* jQuery 1.4.2 との後方互換性を維持したままこの互換性のバグを修正

<a name="16"></a>1.6
---
* アラビア語 (AR)、ポルトガル語 (PTPT)、ペルシャ (FA)、フィンランド語 (FI)、ブルガリア語 (ブラジル) のローカリゼーションの追加
* スウェーデン語 (SE) の ローカリゼーションの更新 (HTML の ISO 文字がいくつか不足していました)
* message 引数の空の文字列と undefined を適切に処理するように $.validator.addMethod を修正
* 2 つの意図しないグローバル変数の修正
* リッチテキスト エディターでの語句のカウントに合わせて、カウント前に HTML を削除するように (additional-methods.js の) min/max/rangeWords を拡張
* DE、NL、PT にローカライズしたメソッドを追加し、dateDE メソッドと numberDE メソッドを削除 (代わりに date メソッドと number メソッドでは messages_de.js および methods_de.js を使用してください)
* リモート フォーム送信の同期の修正 (協力: Matas Petrikas)
* クリック時も (ブラウザーに応じて option または select を使用) 検証を行うように対話形式の select 検証を改善しました。select 要素で click イベントがトリガーされない Safari では機能しません。 http://plugins.jquery.com/node/11520 を修正しました。
* 最新のフォーム プラグイン (2.36) に更新し、 http://plugins.jquery.com/node/11487 を修正
* equalTo ターゲットの変更時に再検証するようにこのターゲットの blur イベントにバインドし、 http://plugins.jquery.com/node/11450 を修正
* jQuery の val() メソッドに select 値の取得を委任することで select 検証を簡略化し、 http://plugins.jquery.com/node/11239 を修正
* 数字の既定のメッセージを修正 (http://plugins.jquery.com/node/9853))
* キャッシュされたリモート メッセージの問題を修正 (http://plugins.jquery.com/node/11029 と http://plugins.jquery.com/node/9351))
* additional-methods.js の不足していたセミコロンを修正 (http://plugins.jquery.com/node/9233))
* メッセージ内の置換パラメーターの自動検出を追加し、書式設定機能を提供する必要性を解消 (http://plugins.jquery.com/node/11195))
* Sizzle が一因となっていた :filled/:blank の問題の修正 (http://plugins.jquery.com/node/11144))
* additional-methods.js への integer メソッドの追加 (http://plugins.jquery.com/node/9612))
* セレクター内部で有効にするためにエスケープの必要な文字列が for 属性に含まれる errorsFor メソッドの修正 (http://plugins.jquery.com/node/9611))

<a name="155"></a>1.5.5
---
* http://plugins.jquery.com/node/8659 の修正
* messages_cs.js の末尾のコンマの修正

<a name="154"></a>1.5.4
---
* リモート メソッドのバグの修正 (http://plugins.jquery.com/node/8658))

<a name="153"></a>1.5.3
---
* wrapper オプションに一致するすべての先祖要素が選択されていた wrapper オプションに関係するバグの修正 (http://plugins.jquery.com/node/7624))
* 最新の jQuery UI アコーディオンを使用するように multipart デモを更新
* additionalMethods.js への dateNL および time メソッドの追加
* 繁体字中国語 (台湾、tw) およびカザフ語 (KK) のローカリゼーションの追加
* jQuery.format (旧 String.format) から jQuery.validator.format への移行。jQuery.format は非推奨となり、1.6 で削除されます (詳細については http://code.google.com/p/jquery-utils/issues/detail?id=15 を参照)
* messages_pl.js および messages_ptbr.js の除去 (1.4 で削除された max/min/rangeValue に対して定義されたままになっていたメッセージ)
* 複数要素の有効なプラグイン メソッドのブール値のロジックの欠陥を修正し、すべての要素について結果のブール値が true の場合に有効であることが必須とされました (http://plugins.jquery.com/node/8481))
* 拡張機能の $$.validator.addmethod:。3 番目未定義メッセージ引数は、既存のメッセージ (を上書きしません。 http://plugins.jquery.com/node/8443)
* SubmitHandler オプションの機能強化:上のイベントの送信ボタンが取得され、送信ボタンをクリックしますが、submitHandler の呼び出し前に、フォームに挿入し、後; は削除使用すると、送信ボタンのまま (を保持します。 http://plugins.jquery.com/node/7183#comment-3585)
* 検証後に有効な要素すべてにクラスを追加する validClass オプション (既定で "有効") の追加 (http://dev.jquery.com/ticket/2205))
* テストを含む creditcardtypes メソッドの additionalMethods.js への追加 (http://dev.jquery.com/ticket/3635))
* クライアント側で定義されているメッセージを使用して、サーバー側メッセージを文字列として、または有効な場合は true、無効な場合は false として許可するようにリモート メソッドを改善 (http://dev.jquery.com/ticket/3807))
* Drupal スタイルのコンマ区切り値一覧も受け入れるように受け入れメソッドを改善 (http://plugins.jquery.com/node/8580))

<a name="152"></a>1.5.2
---
* additional-methods.js で maxWords、minWords、rangeWords のメッセージに $.format への呼び出しを追加
* jQuery の val() と同様にキャリッジ リターン (\r) を除外するようメソッドに渡される値を修正
* スロバキア語 (sk) のローカリゼーションの追加
* jQuery UI タブの統合に関するデモの追加
* tabs デモへの selects-grouping の例の追加demo (2 番目のタブの [birthdate]\(生年月日\) フィールドを参照)

<a name="151"></a>1.5.1
---
* invalid-form イベントではなく invalidHandler オプションを使用するように marketo デモを更新
* TinyMCE 統合の例の追加
* ウクライナ語 (ua) のローカリゼーションの追加
* トリミングされた値を処理するように長さの検証を修正 (検証前のトリミングが削除された 1.5 の不具合の再発)
* 1.2.6 と 1.3 の両方との互換性に関する各種の小さな修正

<a name="15"></a>1.5
---
* パスワードの変更後に confirm-password フィールドを検証するように basic デモを改善
* トリミングされていない入力値を最初のパラメーターとして検証メソッドへ渡すように基本の検証を修正し、適宜必要な変更を行いました。トリミングを使用する既存のカスタム メソッドは分割されました。
* ノルウェー語 (no)、イタリア語 (it)、ハンガリー語 (hu)、ルーマニア語 (ro) のローカリゼーションの追加
* 固定の # 3195:スウェーデン語のローカリゼーションの 2 つの問題
* 固定 #3503:メッセージ プロパティを受け入れる拡張 rules: を使用して指定の規則を使用して要素にカスタム メッセージを追加 ("add", {メッセージ: {0} 必要。"Required! " } }); を使用して要素に add カスタム メッセージを指定するために使用します
* 固定の # 3356:#2908 meta オプションを使用する場合の回帰
* 固定の # 3370:追加された ignoreTitle オプションを title 属性からのメッセージの読み取りをスキップする設定は、Google ツールバーの問題を回避するのに役立ちます既定値は false の互換性
* #3516 の:リモート検証が含まれている場合でも、トリガー invalid-form イベント
* bind("invalid-form", function() {}) のショートカットとしての invalidHandler オプションの追加
* Safari での ajaxSubmit-integration デモの読み込みインジケーターの問題の修正 (まず本文に追加してから非表示にする)
* クレジットカード検証のテストの追加および既定のメッセージの改善
* $.ajax をパラメーターとして通すオプション (URL プロパティに加えて $.ajax でサポートされるそれ以外のすべてのプロパティを含む URL 文字列またはオプションのいずれか) を受け入れるようにリモート検証を拡張

<a name="14"></a>1.4
---
* ドキュメントの順序で要素を検証し type=image 入力を無視するように #2931 を修正
* noConflict のすべての使用バリエーションと完全な互換性のために $ および jQuery 変数の使用を修正
* class="{required:true,messages:{required:'required field'}}" 形式でメタデータによりカスタム メッセージを有効にして #2908 を実装し、demo/custom-messages-metadata-demo.html を追加
* 非推奨のメソッド minValue (min)、maxValue (max)、rangeValue (rangevalue)、minLength (minlength)、maxLength (maxlength)、rangeLength (rangelength) の削除
* 固定の #2215 回帰:現在の要素がすべてに対してのみ表示解除の呼び出し
* 検証をキャンセルする画像ボタンを有効にして #2989 を実装
* IE で maxlength=0 が誤って検証される問題の修正
* チェコ語 (cs) のローカリゼーションの追加
* validator.resetForm() の validator.submitted をリセットし、必要な場合に完全なリセットを有効化
* ルール (0、undefined、空の文字列) の読み取り時に誤りのある属性すべてを省略して maxlength 用の解決策の一部 (0 の場合) を削除し、#3035 を修正
* オランダ語 (nl) のローカリゼーションの追加 (#3201)

<a name="13"></a>1.3
---
* フォームが無効な場合のみトリガーされるように invalid-form イベントを修正
* スペイン語 (es)、ロシア語 (ru)、ポルトガル語 (ブラジル) (ptbr)、トルコ語 (tr)、ポーランド語 (pl) のローカリゼーションの追加
* 複数の属性を追加および削除しやすいように removeAttrs プラグインを追加
* groups: { arbitraryGroupName: "fieldName1 fieldName2[, fieldNameN" } により、複数の要素で単一のメッセージを表示する groups オプションを追加
* (静的な) ルールの追加および削除用に rules() を拡張: rules("add", "method1[, methodN]"/{method1:param[, method_n:param]}) および rules("remove"[, "method1[, method_n]")
* スペース区切りのメソッドの文字列リストを受け入れるように rules オプションを拡張 (例: {birthdate: "required date"})
* インライン ルールによるチェック ボックス グループの検証を修正するには。ルールが最初の要素で指定されている限り、グループはようになりました適切で検証される をクリックします
* 明示的なパラメーターがブール値の false であるルールすべてを無視するようにして #2473 を修正(例: required:false は同一でも required を指定していない場合 (これまでは required:true として処理されていました))
* 変更されたパッチ修正からの固定 # 2424:依存関係の不一致を返すメソッドは、他のルールをもはや; 評価を停止しません。それでも、成功がオプションのフィールドに適用されません。
* トリミングされた値を使用しないように URL および電子メール検証を修正
* 数字とダッシュのみを受け入れるようにクレジットカード検証を修正 ("asdf" は無効なクレジットカード番号)
* (class="cancel" で) キャンセル ボタンでボタンと入力要素の両方を許可
* #2215 の:表示と、要素と UI sideeffects 与えずフォームを検証する抽出された validator.checkForm をチェック中の視覚的な副次的な影響をこれ以上メッセージを非表示の一部として表示解除の呼び出しに固定のメッセージの表示
* AIR との互換性のため関数を使用したカスタム セレクター (:blank、:filled、:unchecked) の書き直し

<a name="121"></a>1.2.1
-----

* 検証プラグインとデリゲート プラグインのバンドル化 (この変更にかかわらず常に必須)
* 同期を適切に実行できるように ajaxQueue プラグインのパーツを追加してリモート検証を改善 (その他のプラグインは不要)
* pendingRequest を 0 未満に設定できないように stopRequest を修正
* min/max を range に、minlength/maxlength を rangelength に変換できるよう、既定値が false の jQuery.validator.autoCreateRanges プロパティを追加しました。これにより、1.2 での範囲の自動作成による問題が基本的に修正されました。
* フィールドが空白の場合に何も強調表示しないように (成功をトリガーしないように) optional-methods を修正
* 強調表示の必要がない場合でも "何もしない" コールバックを強制する代わりに、強調表示/強調表示解除オプションで false/null を使用可能に修正
* エラーをスローせずに undefined を返す、要素が選択されていない validate() 呼び出しの修正
* デモを改善し、メタデータをルールを指定するクラス/属性に置き換え
* リモート検証でカスタム メッセージが使用されていない場合のエラーを修正
* ドメイン ラベルおよびトップ ラベルを必須とするように電子メールと URL の検証を変更
* TLD を必須とするように (実際にはドメイン ラベルを必須とするように) URL と電子メールの検証を修正しました。バージョン 1.2 (TLD は任意) は url2 および email2 としてその他へ移行されました。
* テキスト領域を使用して複数行のテンプレートおよび文字列補間を格納して、IE6/7 での dynamic-totals デモを修正しテンプレート作成を改善
* パスワード フィールドを省略可能にする [Email password]\(電子メール パスワード\) リンクを含むログイン フォームの例の追加
* 2 つのフィールドに対する単一のメッセージの例により dynamic-totals デモを拡張

<a name="12"></a>1.2
---

* AJAX-captcha 検証の例の追加 (http://psyrens.com/captcha/) に基づく)
* remember-the-milk デモの追加 (RTM チームから許可をいただきました)
* marketo デモの追加 (協力: Glen Lipka)
* ajax 検証のサポートの追加。メソッド "リモート" を参照してください。サーバー側では、有効な要素の場合は JSON または true、無効な場合は false または文字列が返されます。文字列はメッセージとして使用されます。
* 強調表示をカスタマイズできるように、既定で要素の errorClass を切り替える強調表示と強調表示解除のオプションを追加
* 検証コントロール API を使用せずにプログラムでフォームおよびフィールドを簡単にチェックできるように、valid() プラグイン メソッドを追加
* 要素のルールの読み取りおよび書き込みを行う rules() プラグイン メソッドの追加 (現在は読み取り専用)
* メール メソッドの正規表現の置換 (協力: Scott Gonzalez。 http://projects.scottsplayground.com/email_address_validation/ を参照)
* パフォーマンスを改善し開発者が使用しやすくするため、デリゲートのみを使用するようにイベントのアーキテクチャを再編成 (jquery.delegate.js を必須化)
* インラインから http://docs.jquery.com/Plugins/Validation へのドキュメントの移行 - すべてのメソッドに対話型の例を追加
* 検証を完全に動的にするため validator.refresh() を削除
* minValue、maxValue、rangeValue の名前を min、max、range に変更し古い名前を非推奨とする (1.3 で削除予定)
* minLength、maxLength、rangeLength の名前を minlength、maxlength、rangelength 変更し古い名前を非推奨とする (1.3 で削除予定)
* min と max を range に、minlength と maxlength を rangelength にマージする機能の追加
* パラメーターとして関数を指定できるように動的なルール パラメーターのサポートを追加 (例: minlength の場合、要素の検証時に呼び出し)
* 何も表示しない場合に null または空の文字列をメッセージとして指定できるようになりました (marketo デモを参照)
* ルールのオーバー ホールします。ルール オプション、メタデータ、クラス (新) および (新規)、属性の組み合わせを今すぐがサポートは、詳細については rules() を参照してください。

<a name="112"></a>1.1.2
---

* URL メソッドの正規表現の置換 (協力: Scott Gonzalez。 http://projects.scottsplayground.com/iri/ を参照)
* ユニコード文字を適切に処理するように email メソッドを改善
* エラー コンテナーがフォームの送信時だけでなくすべての要素が有効な場合も表示されるように修正
* String.format を jQuery.format に変更 (jQuery 名前空間に移行)
* 大文字と小文字両方の拡張を受け入れるように受け入れメソッドを修正
* 特定のフォームで検証コントロール インスタンスを 1 つのみ作成し、この 1 つのインスタンスが常に返されるように validate() プラグイン メソッドを修正 (複数回のイベントのバインドを防止)
* デバッグ モードのコンソール ログのレベルを "エラー" から "警告" に変更

<a name="111"></a>1.1.1
-----

* 無効な XHTML を修正して jQuery 1.1.4 以降での IE のラベル作成エラーを防止
* 固定と強化された String.format:グローバル検索と置換、配列引数の処理の改善
* フォーム要素ではなく状態を格納する検証コントロール オブジェクトを使用するようにキャンセル ボタンの処理を修正
* "複雑な" 名前を処理するように名前セレクターを修正 (例: 角かっこが含まれる ("list[]"))
* 検証から除外するボタンおよび無効化要素の追加
* 新しい要素にハンドラーを追加できるように、更新する要素イベント ハンドラーを移動
* 長い最上位レベルのドメインを使用できるように電子メール検証を修正 (例: ".travel")
* valid() から form() への showErrors() の移動
* validator.size() の追加: 現在のエラーの数を返します
* submitHandler へのアクセスを簡易化するため、スコープとして検証コントロールを使用してこのメソッドを呼び出す (例: errorsFor(Element) を使用したエラー ラベルの検索)
* jQuery 1.1.x および 1.2.x との互換性

<a name="11"></a>1.1
---

* (チェックボックスおよびラジオ ボタンの) blur、keyup、click に検証が追加されました。 event オプションを置き換えました。
* resetForm の修正
* custom-methods デモの修正

<a name="10"></a>1
---

* 区切り記号を含む適切な 10 進数をチェックできるように number および numberDE メソッドを改善
* ルールが設定された要素のみがチェックする (それ以外の場合はすべての要素に成功オプションが適用されます)
* クレジットカード番号メソッドの追加 (協力: Brian Klug)
* ignore オプションの追加。 たとえば、検証から要素を除外する場合、ignore: "[@type=hidden]" という式を使用します。 既定値は none ですが、送信ボタンとリセット ボタンは常に無視されます。
* 柔軟な String.format ヘルパーを用意し、メッセージとしての関数を大きく改善
* ランタイム カスタム メッセージを提供し、メッセージとして関数を受け入れ
* successList からのルールが設定されていない要素の除外の修正
* custom-method デモを修正し、エラー数を示すメッセージでアラートを置き換え
* submitHandler の使用時のフォーム送信防止を修正
* 要素 ID への依存関係が完全に削除されました。ただし、入力へエラー ラベルをリンクするためにこれらの ID は引き続き使用されています (存在する場合)。 この削除は、内部 errorList で、id:message ペアを含むオブジェクトではなく {名前, メッセージ, 要素} を含む配列を使用することで実現しました。
* 単純な文字列としての単純なルール指定のサポートの追加 (例: "required" は {required: true} と同じです)
* 機能の追加:ErrorClass を簡単に、ラベル フィールド/コンテナーまたはフィールドのラベルのスタイルを設定すること、無効なフィールドの親要素に追加します。
* 機能の追加: focusCleanup - 有効にすると、無効な要素にフォーカスされた場合に、常にその要素から errorClass が削除され、すべてのエラー メッセージが非表示になります。
* フィールドが正常に検証されたことを示す成功オプションの追加
* Opera の選択の問題の修正 (属性の衝突の回避)
* IE での非表示要素へのフォーカスの問題の修正
* クラスが "cancel" の送信ボタンの検証を省略する機能の追加
* title 属性よりプラグイン オプション メッセージを優先し、Google ツールバーの潜在的な問題を修正
* 実際の送信イベントの処理時のみ submitHandler が呼び出され、無効なフォームにのみ validator.form() で false が返されます
* ぼかしへのフォーカスの問題を防ぐため、無効な要素は送信時または validator.focusInvalid() 経由でのみフォーカスされるようになりました
* IE6 エラー コンテナーのレイアウトの問題が解決されました
* errorElement オプションでのエラー要素のカスタマイズ
* フォームの新しい入力を検索する validator.refresh() の追加
* ファイル拡張子をチェックする受け入れ検証メソッドの追加
* 値が空白の要素を選択する ":blank" と値を含む要素を選択する ":filled" の 2 つのカスタム式を追加し (ともに空白を除外します)、依存関係機能を改善
* ResetForm() メソッドの検証コントロールを追加します。(使用可能な場合は、フォーム プラグインを使用して) 各フォーム要素をリセット、無効な要素クラスの削除、およびすべてのエラー メッセージを非表示になります
* validator.showErrors() のドキュメントの修正
* 任意の HTML をメッセージとして渡せるように、text() ではなく html() を常に使用するようにエラー ラベルの作成を修正
* 指定されたエラー クラスを使用するようにエラー ラベルの作成を修正
* 追加の依存関係の機能:メソッドの引数として文字列 (jquery式) と関数の両方を受け入れる必要があります。
* 頻度の高いエラー メッセージの表示のカスタマイズの強化。通常のメッセージを使用し、追加のコンテナーの表示/非表示独自のメカニズム (中に、既定のハンドラーに委任することで、メッセージの表示を完全に置き換える(既定の below 要素) ではなく、生成されたラベルの配置をカスタマイズします。
* IE (エラー コンテナー) および Opera (メタデータ) の 2 つの大きなバグの修正
* 空白のフィールドを有効として受け入れるように検証メソッドを変更 (例外: required メソッドおよび equalTo メソッド)
* "min"、"max"、"length" の名前を "minLength"、"maxLength"、"rangeLength" に変更
* "minValue"、"maxValue"、"rangeValue" の追加
* さまざまなイベントをサポートするため API を簡素化しました。 既定値の送信は無効にできます。 イベントが指定されている場合、(フォーム全体ではなく) 各要素に適用されます。 keyup 検証と送信検証の組み合わせの非常に簡単に設定できるようになりました
* プラグイン設定でのメッセージの定義時の "ルールごとに 1 つのメッセージ" のサポートを追加
* 一部の親要素にメタデータをラップするサポートを追加しました。 その他のプラグインでメタデータを使用する場合でも有用です。
* リファクタリング後のテストとデモ:デモの向上、ファイル数の削減
* 強化されたドキュメント:メソッドの例については、その他の参考の基本を説明するテキスト
