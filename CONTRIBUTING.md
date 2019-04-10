# <a name="contribute-to-the-aspnet-documentation"></a>ASP.NET ドキュメントに貢献する

このドキュメントでは、[ASP.NET ドキュメント サイト](https://docs.microsoft.com/aspnet/)でホストされている記事とコード サンプルに貢献するためのプロセスを説明します。 誤字修正と新しい記事の貢献を歓迎します。

## <a name="how-to-make-a-simple-correction-or-suggestion"></a>簡単な修正や提案を行う方法

記事は、マークダウン ファイルとしてリポジトリに格納されています。 マークダウン ファイルの内容に対する簡単な変更は、ブラウザー ウィンドウの右上隅にある **[Edit]\(編集\)** リンクを選択して、ブラウザーで行います。 (幅の狭いブラウザー ウィンドウでは、**オプション** バーを展開して、**[Edit]\(編集\)** リンクを表示します。)指示に従って pull request (PR) を作成します。 PR をレビューし、受け入れるか変更を提案します。

## <a name="how-to-make-a-more-complex-submission"></a>もっと複雑な提案を行う方法

[Git と GitHub.com](https://guides.github.com/activities/hello-world/) の基本的な理解が必要です。

* 既存の記事の変更や新しい記事の作成など、行いたいことを説明した[問題](https://github.com/aspnet/AspNetDocs/issues/new)を開きます。 多くの場合、GitHub は新しいトピックの提案のアウトラインを要求します。 多くの時間を費やす前に、チームの承認を待ちます。
* フォーク、 [aspnet/AspNetDocs](https://github.com/aspnet/AspNetDocs/)リポジトリと、変更のブランチを作成します。
* 変更内容の PR をマスターに送信します。
* PR にラベル "cla-required" が割り当てられた場合、[貢献者使用許諾契約書 (CLA) を作成します](https://cla.dotnetfoundation.org/)。
* PR のフィードバックに対応します。

このプロセスで新しい記事が公開された例については、.NET Docs リポジトリの[問題 &num;67](https://github.com/dotnet/docs/issues/67) と[Pull Request &num;798](https://github.com/dotnet/docs/pull/798) を参照してください。 新しい記事は「[XML コメントによるコードの文書化](https://docs.microsoft.com/dotnet/articles/csharp/codedoc)」です。

## <a name="docs-authoring-pack-extension-in-visual-studio-code"></a>Visual Studio Code での Docs Authoring 拡張機能

Visual Studio Code を使用して ASP.NET ドキュメントに貢献する場合は、[Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) 拡張機能をインストールすることで生産性を高めることができます。 拡張機能では、Markdown の lint 処理、コードのスペル チェック、および記事のテンプレートを支援する各種のツールが提供されています。

## <a name="markdown-syntax"></a>Markdown の構文

記事は [DocFX Flavored Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html) で書かれています。これは [GitHub flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown/) のスーパーセットです。 ASP.NET のドキュメントでよく使用される UI 機能についての DFM 構文の例については、次を参照してください。[メタデータと Markdown テンプレート](https://github.com/dotnet/docs/blob/master/styleguide/template.md).NET Docs リポジトリ スタイル ガイドにします。

## <a name="folder-structure-conventions"></a>フォルダー構造の規則

マークダウン ファイルごとに、画像用のフォルダーとサンプル コード用のフォルダーが存在する場合があります。 アーティクルが場合[signalr/overview/advanced/dependency-injection.md](https://github.com/aspnet/AspNetDocs/blob/master/aspnet/signalr/overview/advanced/dependency-injection.md)、画像は[signalr/概要/高度な/依存関係のインジェクション/\_静的](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/_static)とサンプル アプリ プロジェクトファイルは[signalr/概要/高度な/依存関係のインジェクション/サンプル](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/samples)します。 内のイメージ、 *signalr/overview/advanced/dependency-injection.md*ファイルは、次のマークダウンによってレンダリングされます。

```md
![description of image for alt attribute](dependency-injection/_static/image1.png)
```

すべての画像に[代替 (alt) テキスト](https://wikipedia.org/wiki/Alt_attribute)が必要です。 代替テキストの指定に関するアドバイスについては、「[WebAIM: Alternative Text (WebAIM: 代替テキスト)](https://webaim.org/techniques/alttext/)」などのオンライン リソースを参照してください。

マークダウン ファイル名と画像ファイル名には、小文字を使用します。

## <a name="internal-links"></a>内部リンク

内部リンクでは、xref リンクでターゲット記事の `uid` を使用する必要があります (リンク テキストは、リンクされたコンテンツのタイトルに設定されます)。

```md
<xref:uid_of_the_topic>
```

記事のタイトルがリンク テキストに適さない場合は (たとえば、文の単語や語句がリンク テキストである場合)、次のように xref リンクとリンク テキストを指定します。

```md
[link text](xref:uid_of_the_topic)
```

詳細については、「[DocFX Cross Reference](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#cross-reference)」(DocFX の相互参照) を参照してください。

## <a name="images-and-screenshots"></a>画像とスクリーンショット

次の場合を除き、記事に画像を含めないでください。

* 基本的なオンボード (初心者向け) チュートリアル。
* わかりやすくするために画像が必要な場合。

このような制限により、リポジトリのサイズが小さくなります。

省略可能な手順として、ドキュメントで使用されている画像とスクリーンショットが圧縮されていることを確認します。これは、ファイルのサイズとページ読み込みのパフォーマンスに役立ちます。 一般的なツールとしては、TinyPNG ([TinyPNG Web サイト](https://tinypng.com/) または [TinyPNG API](https://tinypng.com/developers) を使用) または [Image Optimizer](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer) Visual Studio 拡張機能などがあります。

## <a name="code-snippets"></a>コード スニペット

記事には、ポイントを説明するためのコード スニペットが含まれることがよくあります。 DFM では、マークダウン ファイルにコードをコピーすること、または別のコード ファイルを参照することができます。 コードのエラーの可能性を最小限にするため、可能な限り別のコード ファイルを使用することをお勧めします。 コード ファイルは、前に説明したサンプル プロジェクトのフォルダー構造を使用してリポジトリに格納されます。

次の例では、*configuration/index.md* ファイルで使用する [DFM コード スニペットの構文](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#code-snippet)を示します。

コード ファイル全体をスニペットとして表示するには:

```md
[!code-csharp[](configuration/index/sample/Program.cs)]
```

行番号を使用してファイルの一部をスニペットとして表示するには:

```md
[!code-csharp[](configuration/index/sample/Program.cs?range=1-10,20,30,40-50]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=1-10,20,30,40-50]
```

C# のスニペットについては、[C# の領域](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region)に関する記事を参照してください。 可能な場合は常に、行番号ではなく領域を使用してください。コード ファイル内の行番号は変更されることがよくあり、Markdown での行番号の参照と同期されなくなるためです。 C# の領域は入れ子にすることができます。 外側の領域を参照している場合、内側の `#region` および `#endregion` ディレクティブはスニペットには表示されません。

C# の "snippet_Example" という名前の領域を表示するには:

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example)]
```

表示されたスニペットで選択されている行を強調表示するには (通常は黄色の背景色で表示されます):

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example&highlight=1-3,10,20-25)]
[!code-csharp[](configuration/index/sample/Program.cs?range=10-20&highlight=1-3]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=10-20&highlight=1-3]
[!code-javascript[](configuration/index/sample/UsingOptionsSample.csproj?range=10-20&highlight=1-3]
```

## <a name="test-changes-with-docfx"></a>DocFX で変更をテストする

[DocFX コマンド ライン ツール](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool)を使用して変更をテストします。このツールは、ローカルにホストされたバージョンのサイトを作成します。 DocFX では、docs.microsoft.com 用に作成されたスタイルやサイトの拡張機能は表示されません。

DocFX には次のものが必要です。

* Windows 上の .NET Framework。
* Linux または macOS 用の Mono。

### <a name="windows-instructions"></a>Windows での手順

* [DocFX リリース](https://github.com/dotnet/docfx/releases)から *docfx.zip* をダウンロードして解凍します。
* DocFX を PATH に追加します。
* コマンド シェルに移動します。、 *aspnet*を含むフォルダー、 *docfx.json*ファイルを開き、次のコマンドを実行します。

  ```console
  docfx --serve
  ```

* ブラウザーで、`http://localhost:8080/group1-dest/` に移動します。

### <a name="mono-instructions"></a>Mono での手順

* Homebrew を使用して Mono をインストールします。

  ```console
  brew install mono
  ```

* [最新バージョンの DocFX](https://github.com/dotnet/docfx/releases) をダウンロードします。
* アーカイブを *$HOME/bin/docfx* に抽出します。
* bash シェルで **docfx** の別名を 2 つ作成します。 最初の別名は、ドキュメントを構築するために使います。 2 番目の別名は、ドキュメントを構築して提供するために使います。

  ```console
  alias docfx='mono $HOME/bin/docfx/docfx.exe'
  alias docfx-serve='mono $HOME/bin/docfx/docfx.exe --serve'
  ```

* コマンド シェルに移動します。、 *aspnet*を含むフォルダー、 *docfx.json*ファイルをビルド、そのエイリアスを使用してドキュメントを提供する次のコマンドを実行して。

  ```console
  docfx-serve
  ```

* ブラウザーで、`http://localhost:8080/group1-dest/` に移動します。

## <a name="voice-and-tone"></a>スタイルとトーン

目標は、できるかぎり幅広いユーザーにわかりやすいドキュメントを作成することです。 そのため、寄稿者に従っていただきたい書き方のガイドラインが設けられています。 詳細については、次を参照してください。[とトーンのガイドライン](https://github.com/dotnet/docs/blob/master/styleguide/voice-tone.md).NET リポジトリにします。

## <a name="microsoft-writing-style-guide"></a>Microsoft 文書作成スタイル ガイド

[Microsoft 文書作成スタイル ガイド](https://docs.microsoft.com/style-guide/welcome/)では、ASP.NET Core のドキュメントを含むあらゆる形式の技術コミュニケーションに対する文書作成スタイルと用語のガイダンスが提供されています。

## <a name="redirects"></a>リダイレクト

記事を削除する、記事のファイル名を変更する、または記事を別のフォルダーに移動する場合は、記事にブックマークを設定している人が *404 Not Found* エラーを受け取らないように、リダイレクトを作成します。 [マスター リダイレクト ファイル](https://github.com/aspnet/AspNetDocs/blob/master/.openpublishing.redirection.json)にリダイレクトを追加してください。
