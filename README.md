CommonMark(日本語訳)
==========

<!--
CommonMark is a rationalized version of Markdown syntax,
with a [spec][the spec] and BSD-licensed reference
implementations in C and JavaScript.
-->
CommonMarkはMarkdown文法を整理したもので、[仕様][the spec]およびBSDライセンスの下で公開されているCとJavaScriptの実装があります。

<!--
[Try it now!](http://try.commonmark.org/)
-->
[試してみよう!](http://try.commonmark.org/)

[the spec]:  http://spec.commonmark.org/

<!--
For more details, see <http://commonmark.org>.
-->
詳細は<http://commonmark.org>をご覧ください。

<!--
This repository contains the spec itself, along with tools for
running tests against the spec, and for creating HTML and PDF versions
of the spec.
-->
このリポジトリは、仕様書と、仕様に沿っているかテストするためのツール、および仕様書をHTMLやPDFにするためのツールが含まれています。

<!--
The reference implementations live in separate repositories:
-->
リファレンス実装は別のリポジトリにあります。

- <https://github.com/commonmark/cmark> (C)
- <https://github.com/commonmark/commonmark.js> (JavaScript)

<!--
There is a list of third-party libraries
in a dozen different languages
[here](https://github.com/commonmark/CommonMark/wiki/List-of-CommonMark-Implementations).
-->
[こちら](https://github.com/commonmark/CommonMark/wiki/List-of-CommonMark-Implementations)に色々な言語で実装されたサードパーティーライブラリがあります。

<!--
Running tests against the spec
------------------------------
-->
仕様書に沿っているかテストする
------------------------------

<!--
[The spec] contains over 500 embedded examples which serve as conformance
tests. To run the tests using an executable `$PROG`:
-->
[仕様][The spec]には、適合試験を実施するための500以上の組み込みテストが含まれています。
実行可能な`$PROG`を用いてテストを実行するには、次のようにします。

    python3 test/spec_tests.py --program $PROG

<!--
If you want to extract the raw test data from the spec without
actually running the tests, you can do:
-->
実際にテストを実行することなく、仕様からテストデータを抽出したい場合は、次のようにします。

    python3 test/spec_tests.py --dump-tests

<!--
and you'll get all the tests in JSON format.
-->
こうするとすべてのテストをJSON形式で得られます。

<!--
The spec
--------
-->
仕様
--------

<!--
The source of [the spec] is `spec.txt`.  This is basically a Markdown
file, with code examples written in a shorthand form:
-->
[仕様][The spec]のソースは`spec.txt`です。
基本的にはMarkdown形式で、shorthand formで書かれたコード例が付いています。

    ```````````````````````````````` example
    Markdown source
    .
    expected HTML output
    ````````````````````````````````

<!--
To build an HTML version of the spec, do `make spec.html`.  To build a
PDF version, do `make spec.pdf`.  For both versions, you must
have the lua rock `lcmark` installed:  after installing lua and
lua rocks, `luarocks install lcmark`.  For the PDF you must also
have xelatex installed.
-->
HTML版の仕様書をビルドするには、`make spec.html`を実行してください。
PDF版の場合は`make spec.pdf`です。両方とも`lcmark`というlua rockが必要です。
luaとlua rockをインストールしたのち、`luarocks install lcmark`としてください。
PDF版の場合はxelatexもインストールする必要があります。

<!--
The spec is written from the point of view of the human writer, not
the computer reader.  It is not an algorithm---an English translation of
a computer program---but a declarative description of what counts as a block
quote, a code block, and each of the other structural elements that can
make up a Markdown document.
-->
仕様書はコンピュータによる読み取りではなく、人間の書き手からの観点で書かれています。
アルゴリズム—プログラムをただ文書化したもの—ではなく、引用やコードブロック、Markdown文書を構成する構成要素として何を含めるのかという宣言的な文書になっています。

<!--
Because John Gruber's [canonical syntax
description](http://daringfireball.net/projects/markdown/syntax) leaves
many aspects of the syntax undetermined, writing a precise spec requires
making a large number of decisions, many of them somewhat arbitrary.
In making them, we have appealed to existing conventions and
considerations of simplicity, readability, expressive power, and
consistency.  We have tried to ensure that "normal" documents in the many
incompatible existing implementations of Markdown will render, as far as
possible, as their authors intended.  And we have tried to make the rules
for different elements work together harmoniously.  In places where
different decisions could have been made (for example, the rules
governing list indentation), we have explained the rationale for
our choices.  In a few cases, we have departed slightly from the canonical
syntax description, in ways that we think further the goals of Markdown
as stated in that description.
-->
John Gruberの[文法規約](http://daringfireball.net/projects/markdown/syntax)では、正確な仕様を書くにあたって膨大な決定をする必要があるような定まっていない文法や、幾分適当なものも多く残っています。
決定をするにあたっては、私たちは簡潔性、可読性、表現力や一貫性についての検討や既存の習慣に訴えてきました。
非互換な既存のMarkdown実装で作られる多くの「通常の」文書が、可能な限り著者の意図通りに表示されるようにすることを試みてきました。
そして私たちは異なる要素が互いに調和的に働くようにルールを定めることを試みてきました。
異なる決定事項があるところでは(例えば、リストのインデントにそういったルールがあります)、私たちが選択した論拠を明確にしています。
いくつかの項目では、元の文法規約を起点としてMarkdownのさらなる到達点を考えるという形で、そこから少し逸脱しています。

<!--
For the most part, we have limited ourselves to the basic elements
described in Gruber's canonical syntax description, eschewing extensions
like footnotes and definition lists.  It is important to get the core
right before considering such things. However, we have included a visible
syntax for line breaks and fenced code blocks.
-->
ほとんどのパートでは、脚注や定義リストのような拡張を抑える、Gruberの文法規約で示されている基礎的な要素を制限しています。
こういったことを考える前にcore rightを得るのは重要です。
しかしながら、改行や囲まれたコードブロックのための明示的な文法は仕様に含まれています。

<!--
Differences from original Markdown
----------------------------------
-->
オリジナルのMarkdownとの違い
----------------------------------

<!--
There are only a few places where this spec says things that contradict
the canonical syntax description:
-->
仕様書のいくつかの箇所には元の文法規約と矛盾するようなものがあります。

<!--
-   It allows all punctuation symbols to be backslash-escaped,
    not just the symbols with special meanings in Markdown. We found
    that it was just too hard to remember which symbols could be
    escaped.
-->
-   Markdownで特別な意味を持つ記号ではない、バックスラッシュでエスケープされる全ての約物を許容しています。
     どの記号がエスケープできるのか覚えておくのがとても大変だとわかったためです。

<!--
-   It introduces an alternative syntax for hard line
    breaks, a backslash at the end of the line, supplementing the
    two-spaces-at-the-end-of-line rule. This is motivated by persistent
    complaints about the “invisible” nature of the two-space rule.
-->
-   強制改行の他の文法として、「行末にスペース2つ」ルールを補完する、行末にバックスラッシュを導入しています。
    スペース2つルールの「不可視」状態について根強い抗議が動機です。

<!--
-   Link syntax has been made a bit more predictable (in a
    backwards-compatible way). For example, `Markdown.pl` allows single
    quotes around a title in inline links, but not in reference links.
    This kind of difference is really hard for users to remember, so the
    spec allows single quotes in both contexts.
-->
-   リンクの文法が(後方互換性を保った形で)ほんの少しばかり予測可能になりました。
    例えば、`Markdown.pl`ではインラインリンクでタイトルの周りをシングルクォートで囲むことを許容していましたが、参照リンクではしていませんでした。
    この手の違いはユーザーが本当に覚えづらいので、両方ともシングルクォートが可能になっています。

<!--
-   The rule for HTML blocks differs, though in most real cases it
    shouldn't make a difference. (See the section on HTML Blocks
    for details.) The spec's proposal makes it easy to include Markdown
    inside HTML block-level tags, if you want to, but also allows you to
    exclude this. It also makes parsing much easier, avoiding
    expensive backtracking.
-->
-   ほとんどのケースでは違いはないはずですが、HTMLブロックのルールは異なっています。
    (詳細はHTMLブロックの項目を参照)
    仕様での提案はMarkdownを、HTMLブロックレベルのタグの中に入れやすくしているだけでなく、もし望むなら取り除くことも可能です。
    高級なバックトラックを避けて、パースもしやすくしています。

<!--
-   It does not collapse adjacent bird-track blocks into a single
    blockquote:
-->
-   隣り合う不等号型のブロックがただ一つの引用になってしまうのを回避しています。

        > this is two

        > blockquotes

        > this is a single
        >
        > blockquote with two paragraphs

<!--
-   Rules for content in lists differ in a few respects, though (as with
    HTML blocks), most lists in existing documents should render as
    intended. There is some discussion of the choice points and
    differences in the subsection of List Items entitled Motivation.
    We think that the spec's proposal does better than any existing
    implementation in rendering lists the way a human writer or reader
    would intuitively understand them. (We could give numerous examples
    of perfectly natural looking lists that nearly every existing
    implementation flubs up.)
-->
-   (HTMLブロックと同様に)ほとんどのリストは意図した通りに表示されるはずですが、リスト中のコンテンツについてのルールが何点か異なります。
    Choice points and differences in the subsection of List itemsについてある議論があり、これが動機となりました。
    私たちは、仕様の提案はどの既存の実装よりも人間が直感的に理解しやすい形でリストを表示できると考えています。
    (一見完璧に自然に見えるリストなのにほとんど全ての実装が表示に失敗する例をいくつも挙げられます。)

<!--
-   Changing bullet characters, or changing from bullets to numbers or
    vice versa, starts a new list. We think that is almost always going
    to be the writer's intent.
-->
-   箇条書きの記号を途中で変えたり、箇条書きから順序リストにしたり、また逆のパターンでも新しいリストが始まります。
    この方がほとんどの場合、書き手の意図に沿うものだと考えています。

<!--
-   The number that begins an ordered list item may be followed by
    either `.` or `)`. Changing the delimiter style starts a new
    list.
-->
-   順序リストを始める番号を、`.`や`)`から始められます。
    区切り記号を途中で変えると、新しいリストが始まります。

<!--
-   The start number of an ordered list is significant.
-->
-   順序リストを始める最初の番号から始まるようになります。

<!--
-   Fenced code blocks are supported, delimited by either
    backticks (```` ``` ````) or tildes (` ~~~ `).
-->
-   囲まれたコードブロックがサポートされます。区切り記号はバッククォート(```` ``` ````)かチルダ(` ~~~ `)です。

<!--
Contributing
------------
-->
支援
------------

<!--
There is a [forum for discussing
CommonMark](http://talk.commonmark.org); you should use it instead of
github issues for questions and possibly open-ended discussions.
Use the [github issue tracker](http://github.com/commonmark/CommonMark/issues)
only for simple, clear, actionable issues.
-->
[CommonMarkのためのフォーラム](http://talk.commonmark.org)があります。
github issuesの代わりに、質問や、終わりのなさそうな議論についてはこちらを使ってください。
[github issue tracker](http://github.com/commonmark/CommonMark/issues)は簡潔で、実際手をつけるべき問題についてのみ使ってください。

<!--
Authors
-------
-->
著者
-------

<!--
The spec was written by John MacFarlane, drawing on
-->
この仕様はJohn MacFarleneによって書かれ、次のような寄与がありました。

<!--
- his experience writing and maintaining Markdown implementations in several
  languages, including the first Markdown parser not based on regular
  expression substitutions ([pandoc](http://github.com/jgm/pandoc)) and
  the first markdown parsers based on PEG grammars
  ([peg-markdown](http://github.com/jgm/peg-markdown),
  [lunamark](http://github.com/jgm/lunamark))
- a detailed examination of the differences between existing Markdown
  implementations using [BabelMark 2](http://johnmacfarlane.net/babelmark2/),
  and
- extensive discussions with David Greenspan, Jeff Atwood, Vicent
  Marti, Neil Williams, and Benjamin Dumke-von der Ehe.
-->
-   正規表現によらないはじめてのMarkdown実装([pandoc](http://github.com/jgm/pandoc))やPEG文法によるはじめてのMarkdownパーサ([peg-markdown](http://github.com/jgm/peg-markdown), [lunamark](http://github.com/jgm/lunamark))を含む、いくつかのMarkdown実装を作成、実装した経験
-   [BabelMark 2](http://johnmacfarlane.net/babelmark2/)を用いた、既存のMarkdown実装との違いを調べた詳細な試験
-   David Greenspan、Jeff Atwood、Vicent Marti、Neil Williams、Benjamin Dumke-von-von der Eheとの広範な議論

<!--
Since the first announcement, many people have contributed ideas.
Kārlis Gaņģis was especially helpful in refining the rules for
emphasis, strong emphasis, links, and images.
-->
最初のアナウンスから、たくさんの人々がアイデアをくれました。
Kārlis Gaņģisは、強調やリンク、画像についてのルールの精緻化を特に助けてくれました。
