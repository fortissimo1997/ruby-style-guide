# はじめに

> ロールモデルが重要なのだ。 <br>
> -- アレックス・マーフィー巡査 / ロボコップ

Rubyディベロッパーとして、私は常にあることに悩まされてきました -
Pythonにはプログラミングスタイルのすばらしい基準
([PEP-8][])
がある一方で、
Rubyにはコーディングスタイルやベストプラクティスに関する公式のガイドがこれまで存在してきませんでした。
私にはスタイルは重要なことだとしか思われないのにです。
Rubyが持っているような素晴らしいハッカーコミュニティは、
誰もが羨むようなドキュメントを作り出す力があるはずなのにです。

このガイドは、私達の社内製Rubyコーディング規約から生まれました
(著者は[私](https://github.com/bbatsov))。
しかし仕事をするうちに、自分の仕事はRubyコミュニティの人たち全員に興味を持ってもらえるものではないかと思い始めました。
また、内製コーディング規約といったものをこの惑星はこれ以上必要としていないのではないかとの思いもありました。
そうではない、コミュニティ駆動の、コミュニティに認められた、
Rubyのための慣習、語法、スタイル規定は、
確実にRubyコミュニティに有益たりえると確信したのです。

このガイドを公開して以来、私は世界中の優れたRubyコミュニティのメンバーから、
たくさんのフィードバックを受けています。
全ての提案、サポートに感謝します！
お互いに、また全てのRubyディベロッパーにとって有益なリソースを、
一緒に作ることができています。

また、もしあなたがRailsのことに興味があるなら、
こちらの補足も確認してみてください。
[Ruby on Rails Style Guide][rails-style-guide].

# The Ruby Style Guide

このRubyスタイルガイドでおすすめしているベストプラクティスは、実在のRubyプログラマが他の実在のRubyプログラマのために、メンテナンスしやすいコードを書いていくためのものです。
実社会での使われ方を反映したスタイルガイドは、実社会で使われるし、
たとえそれがどんなに素晴らしい理想であっても、
利用者が拒絶するようなスタイルに固執するスタイルガイドは結局全く使われなくなる危険性があります。

このガイドは、関連するルールごとにいくつかのセクションに分かれています。
ルールの後ろにその根拠も付け加えるように努めています
(そのような根拠が省略されているときは、自明のものと判断したとお考えください)。

私はこれら全てのルールをどこからともなく考えついたわけではありません -
これらのほとんどは、私の職業SEとしての長い経験と、
Rubyコミュニティのメンバーからの意見や提案、
また、["Programming Ruby 1.9"][pickaxe]や、
["The Ruby Programming Language"][trpl]のような、
様々な評価の高いRubyプログラミング関連資料に基づいています。

Rubyコミュニティ内でもスタイルについての統一見解が存在しないという領域もいくらか存在します
(文字列リテラルの引用記号、ハッシュリテラルの内側のスペース、複数行のメソッドチェーンのドットの位置、などなど)。
そのようなシナリオでは、いずれの有力なスタイルも許容されるので、
どれを選んで、一貫して用いるかはあなた次第です。

新たな慣習が生まれたり、Ruby自身が変化することで慣習が時代遅れになったりしたことに従いながら、このガイドは時代とともに進化してきました。

多くのプロジェクトは、それ自身のコーディング規約を持っています
(しばしばこのガイドを基に生成されています)。
ルールの衝突が発生した場合は、
そのプロジェクトにおいては、プロジェクト固有のガイドを優先してください。

PDFやHTMLのコピーはこのガイドを使って作成できます
[Transmuter][]。

[RuboCop][]は、
このスタイルガイドに基づいたコード分析器です。

以下の言語の翻訳が利用可能です:

* [中国語(簡体)](https://github.com/JuanitoFatas/ruby-style-guide/blob/master/README-zhCN.md)
* [中国語(繁体)](https://github.com/JuanitoFatas/ruby-style-guide/blob/master/README-zhTW.md)
* [フランス語](https://github.com/porecreat/ruby-style-guide/blob/master/README-frFR.md)
* [ドイツ語](https://github.com/arbox/ruby-style-guide/blob/master/README-deDE.md)
* [日本語](https://github.com/fortissimo1997/ruby-style-guide/blob/japanese/README.ja.md)
* [韓国語](https://github.com/dalzony/ruby-style-guide/blob/master/README-koKR.md)
* [ポルトガル語](https://github.com/rubensmabueno/ruby-style-guide/blob/master/README-PT-BR.md)
* [ロシア語](https://github.com/arbox/ruby-style-guide/blob/master/README-ruRU.md)
* [スペイン語](https://github.com/alemohamad/ruby-style-guide/blob/master/README-esLA.md)
* [ベトナム語](https://github.com/scrum2b/ruby-style-guide/blob/master/README-viVN.md)

## 目次

* [レイアウト](#レイアウト)
* [構文](#構文)
* [命名規則](#命名規則)
* [コメント](#コメント)
  * [注釈](#注釈)
* [クラスとモジュール](#クラスとモジュール)
* [例外](#例外)
* [コレクション](#コレクション)
* [文字列](#文字列)
* [正規表現](#正規表現)
* [パーセントリテラル](#パーセントリテラル)
* [メタプログラミング](#メタプログラミング)
* [雑則](#雑則)
* [ツール](#ツール)

## レイアウト

> ほとんどすべての人が、彼ら自身のものを除くすべてのスタイルが
> 醜くて、読むに耐えないと確信している。
> 「彼ら自身のものを除く」を除けば、おそらく正しいのだが…
> -- Jerry Coffin (インデントについて)

* <a name="utf-8"></a>
  ソースファイルのエンコーディングには`UTF-8`を用いましょう。
<sup>[[link](#utf-8)]</sup>

* <a name="spaces-indentation"></a>
  インデントには **スペース** 2つを用いましょう(別名ソフトタブ)。 ハードタブを用いてはいけません。
<sup>[[link](#spaces-indentation)]</sup>

  ```Ruby
  # 悪い例 - 4つのスペース
  def some_method
      do_something
  end

  # 良い例
  def some_method
    do_something
  end
  ```

* <a name="crlf"></a>
  Unix-styleの改行にしましょう。
(*BSD/Solaris/Linux/OS X ユーザーはデフォルトで設定されています。
  Windows ユーザーは特に注意が必要です。)
<sup>[[link](#crlf)]</sup>

  * もしGitを使っていれば、プロジェクトにWindowsの改行が紛れ込まないように、以下の設定を追加したほうがよいかもしれません:

    ```bash
    $ git config --global core.autocrlf true
    ```

* <a name="no-semicolon"></a>
  命令文や式の区切りに`;`を用いてはいけません。
  当然、１行につき式１つにしましょう。
<sup>[[link](#no-semicolon)]</sup>

  ```Ruby
  # 悪い例
  puts 'foobar'; # 余分なセミコロンです

  puts 'foo'; puts 'bar' # ２つの式が１行にあります

  # 良い例
  puts 'foobar'

  puts 'foo'
  puts 'bar'

  puts 'foo', 'bar' # putsの場合はこれも可です
  ```

* <a name="single-line-classes"></a>
  本文のないクラスは１行のフォーマットが好まれます。
<sup>[[link](#single-line-classes)]</sup>

  ```Ruby
  # 悪い例
  class FooError < StandardError
  end

  # 悪くない例
  class FooError < StandardError; end

  # 良い例
  FooError = Class.new(StandardError)
  ```

* <a name="no-single-line-methods"></a>
  １行のメソッドは避けましょう。
  この用法は実際にはよく見かけるものではあるのですが、
  構文に奇妙な点があるため、使用は望ましくないです。
  仮に使うとしても、
  １行メソッドに含めるのは多くとも式１つまでにすべきです。
<sup>[[link](#no-single-line-methods)]</sup>

  ```Ruby
  # 悪い例
  def too_much; something; something_else; end

  # 悪くない例 - 最初の ; は必要です
  def no_braces_method; body end

  # 悪くない例 - ２つ目の ; は任意です
  def no_braces_method; body; end

  # 悪くない例 - 文法上は正しいです、ただし; がない記述は少し読みづらいです
  def some_method() body end

  # 良い例
  def some_method
    body
  end
  ```

  本文が空のメソッドはこのルールの例外です。

  ```Ruby
  # 良い例
  def no_op; end
  ```

* <a name="spaces-operators"></a>
  演算子の前後、コンマ、コロン、セミコロンの後ろ、`{`の前後、`}`の前にはスペースを入れましょう。
  スペースはRubyのインタープリタには(ほとんどの場合)重要ではありませんが、
  スペースの適切な使用は、読みやすいコードを書くための鍵です。
<sup>[[link](#spaces-operators)]</sup>

  ```Ruby
  sum = 1 + 2
  a, b = 1, 2
  1 > 2 ? true : false; puts 'Hi'
  [1, 2, 3].each { |e| puts e }
  class FooError < StandardError; end
  ```

  演算子についてただひとつの例外は、指数演算子です:

  ```Ruby
  # 悪い例
  e = M * c ** 2

  # 良い例
  e = M * c**2
  ```

  `{` と `}` については多少の解説が必要でしょう。
  ブロック、ハッシュリテラル、そして文字列埋め込み式にそれぞれ使われるからです。
  ハッシュリテラルでは、２つのスタイルが許容できます。

  ```Ruby
  # 良い例 - スペースを { の後と } の前に入れる
  { one: 1, two: 2 }

  # 良い例 - スペースを { の後と } の前に入れない
  {one: 1, two: 2}
  ```

  １つ目の書き方は、わずかながら少し読みやすいです(そして、ほぼ間違いなく一般的なRubyコミュニティで人気があります)。
  ２つ目の書き方は、ブロックとハッシュを視覚的に差別化できるという点で有利です。
  どちらでも片方を採用すれば、常に同じ方式を採用しましょう。

* <a name="no-spaces-braces"></a>
  `(`、 `[`の後と、`]`、 `)`の前にはスペースは入れません。
<sup>[[link](#no-spaces-braces)]</sup>

  ```Ruby
  some(arg).other
  [1, 2, 3].size
  ```

* <a name="no-space-bang"></a>
  `!`の後にはスペースは入れません。
<sup>[[link](#no-space-bang)]</sup>

  ```Ruby
  # 悪い例
  ! something

  # 良い例
  !something
  ```

* <a name="no-space-inside-range-literals"></a>
  範囲リテラルの内側にスペースは入れません。
<sup>[[link](#no-space-inside-range-literals)]</sup>

    ```Ruby
    # 悪い例
    1 .. 3
    'a' ... 'z'

    # 良い例
    1..3
    'a'...'z'
    ```

* <a name="indent-when-to-case"></a>
  `when`は`case`と同じ深さに揃えましょう。
  多くの人が同意できないのを知っていますが、
  このスタイルは"The Ruby Programming Language"、"Programming Ruby"
  双方で確立されたものなのです。
<sup>[[link](#indent-when-to-case)]</sup>

  ```Ruby
  # 悪い例
  case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
  end

  # 良い例
  case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration > 120
    puts 'Too long!'
  when Time.now.hour > 21
    puts "It's too late"
  else
    song.play
  end
  ```

* <a name="indent-conditional-assignment"></a>
  条件式を変数に代入するときは、
  条件分岐のインデントは普段と同じ基準で揃えましょう。
<sup>[[link](#indent-conditional-assignment)]</sup>

  ```Ruby
  # 悪い例 - かなり複雑です
  kind = case year
  when 1850..1889 then 'Blues'
  when 1890..1909 then 'Ragtime'
  when 1910..1929 then 'New Orleans Jazz'
  when 1930..1939 then 'Swing'
  when 1940..1950 then 'Bebop'
  else 'Jazz'
  end

  result = if some_cond
    calc_something
  else
    calc_something_else
  end

  # 良い例 - 何が行われているか明らかです
  kind = case year
         when 1850..1889 then 'Blues'
         when 1890..1909 then 'Ragtime'
         when 1910..1929 then 'New Orleans Jazz'
         when 1930..1939 then 'Swing'
         when 1940..1950 then 'Bebop'
         else 'Jazz'
         end

  result = if some_cond
             calc_something
           else
             calc_something_else
           end

  # 良い例 (少しだけ幅の効率がよいです)
  kind =
    case year
    when 1850..1889 then 'Blues'
    when 1890..1909 then 'Ragtime'
    when 1910..1929 then 'New Orleans Jazz'
    when 1930..1939 then 'Swing'
    when 1940..1950 then 'Bebop'
    else 'Jazz'
    end

  result =
    if some_cond
      calc_something
    else
      calc_something_else
    end
  ```

* <a name="empty-lines-between-methods"></a>
  メソッド定義式の間には空行をいれ、
  メソッド同士は論理的なかたまりに分けましょう。
<sup>[[link](#empty-lines-between-methods)]</sup>

  ```Ruby
  def some_method
    data = initialize(options)

    data.manipulate!

    data.result
  end

  def some_method
    result
  end
  ```

* <a name="no-trailing-params-comma"></a>
  メソッド呼び出しの最後の引数の後ろのコンマは避けましょう。
  引数が複数行にわかれていない時は、特に避けましょう。
<sup>[[link](#no-trailing-params-comma)]</sup>

  ```Ruby
  # 悪い例 - 簡単に引数を移動・追加・削除できますが、それでもお奨めできません。
  some_method(
               size,
               count,
               color,
             )

  # 悪い例
  some_method(size, count, color, )

  # 良い例
  some_method(size, count, color)
  ```

* <a name="spaces-around-equals"></a>
  メソッドの引数に初期値を割り当てるとき、
  `=`演算子の周りにはスペースを入れましょう。
<sup>[[link](#spaces-around-equals)]</sup>

  ```Ruby
  # 悪い例
  def some_method(arg1=:default, arg2=nil, arg3=[])
    # do something...
  end

  # 良い例
  def some_method(arg1 = :default, arg2 = nil, arg3 = [])
    # do something...
  end
  ```

  いくつかのRuby本は最初のスタイルを提案していますが、
  ２つ目の方が、実用的により優れています
  (そして、少し読みやすいかもしれません)。

* <a name="no-trailing-backslash"></a>
  `\`を用いた行の継続は可能であれば避けましょう。
  可能であればというのは、つまり、文字列連結以外のすべての場合でです。
<sup>[[link](#no-trailing-backslash)]</sup>

  ```Ruby
  # 悪い例
  result = 1 - \
           2

  # 良い例 (しかしそれでも地獄のように醜い)
  result = 1 \
           - 2

  long_string = 'First part of the long string' \
                ' and second part of the long string'
  ```

* <a name="consistent-multi-line-chains"></a>
  一貫した複数行のメソッドチェーンのスタイルを採用しましょう。
  Rubyコミュニティには2つのよく使われるスタイル - 先頭に`.`を付けるもの (Option A)、
  末尾に`.`を付けるもの (Option B) - があり、
  どちらも良いと考えられています。
<sup>[[link](#consistent-multi-line-chains)]</sup>

  * **(Option A)** メソッドチェーンを次の行へつなげる時は、
    `.`は次の行に置きましょう。

    ```Ruby
    # 悪い例 - ２行目を理解するのに１行目を調べなければなりません
    one.two.three.
      four

    # 良い例 - ２行目で何が行われているかすぐに理解できます
    one.two.three
      .four
    ```

  * **(Option B)** メソッドチェーンを次の行につなげる時は、
    式が続くことを示すように最初の行に`.`を置きましょう。

    ```Ruby
    # 悪い例 - メソッドチェーンが続いているかを知るには、次の行を読む必要があります
    one.two.three
      .four

    # 良い例 - 最初の行を越えて式が続くか一目瞭然です
    one.two.three.
      four
    ```

  双方のスタイルのメリットに関する議論は[こちら](https://github.com/bbatsov/ruby-style-guide/pull/176)
  で見ることができます。

* <a name="no-double-indent"></a>
  メソッド呼び出しが複数行に及ぶときは、引数は揃えましょう。
  １行の長さの制約のために、引数を揃えるのに適していない時は、
  最初の引数以降をインデント１つ分で揃えるスタイルも許容できます。
<sup>[[link](#no-double-indent)]</sup>

  ```Ruby
  # 初期状態 (１行がとても長いです)
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com', from: 'us@example.com', subject: 'Important message', body: source.text)
  end

  # 悪い例 (インデントが倍)
  def send_mail(source)
    Mailer.deliver(
        to: 'bob@example.com',
        from: 'us@example.com',
        subject: 'Important message',
        body: source.text)
  end

  # 良い例
  def send_mail(source)
    Mailer.deliver(to: 'bob@example.com',
                   from: 'us@example.com',
                   subject: 'Important message',
                   body: source.text)
  end

  # 良い例 (普通のインデントです)
  def send_mail(source)
    Mailer.deliver(
      to: 'bob@example.com',
      from: 'us@example.com',
      subject: 'Important message',
      body: source.text
    )
  end
  ```

* <a name="align-multiline-arrays"></a>
  複数行に及ぶ配列は、要素を揃えましょう。
<sup>[[link](#align-multiline-arrays)]</sup>

  ```Ruby
  # 悪い例 - インデント１つです
  menu_item = ["Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
    "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"]

  # 良い例
  menu_item = [
    "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
    "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"
  ]

  # 良い例
  menu_item =
    ["Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
     "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"]
  ```

* <a name="underscores-in-numerics"></a>
  可読性のため、大きな数値にはアンダースコアをつけましょう。
<sup>[[link](#underscores-in-numerics)]</sup>

  ```Ruby
  # 悪い例 - 0はいくつありますか？
  num = 1000000

  # 良い例 - 人の頭でもより簡単に解析できます
  num = 1_000_000
  ```

* <a name="rdoc-conventions"></a>
  APIドキュメントを書くなら、RDocとその規約に従いましょう。
  コメント行と`def`の間に空行を入れてはいけません。
<sup>[[link](#rdoc-conventions)]</sup>

* <a name="80-character-limits"></a>
  １行は80字までにしましょう。
<sup>[[link](#80-character-limits)]</sup>

* <a name="no-trailing-whitespace"></a>
  行末のスペースは避けましょう。
<sup>[[link](#no-trailing-whitespace)]</sup>

* <a name="newline-eof"></a>
  ファイルの終端には改行を入れましょう。
<sup>[[link](#newline-eof)]</sup>

* <a name="no-block-comments"></a>
  ブロックコメントは使ってはいけません。
  前にスペースが入ると機能しませんし、
  通常のコメントと違い、簡単に見分けが付きません。
<sup>[[link](#no-block-comments)]</sup>

  ```Ruby
  # 悪い例
  == begin
  comment line
  another comment line
  == end

  # 良い例
  # comment line
  # another comment line
  ```

## 構文

* <a name="double-colons"></a>
  `::`は、定数(クラスやモジュールも含みます)や
  コンストラクタ(例えば`Array()`や`Nokogiri::HTML()`)を参照するときにのみ使いましょう。
  通常のメソッド呼び出しでは`::`の使用は避けましょう。
<sup>[[link](#double-colons)]</sup>

  ```Ruby
  # 悪い例
  SomeClass::some_method
  some_object::some_method

  # 良い例
  SomeClass.some_method
  some_object.some_method
  SomeModule::SomeClass::SOME_CONST
  SomeModule::SomeClass()
  ```

* <a name="method-parens"></a>
  引数があるとき、`def`は`()`と共に使いましょう。
  引数がない場合は`()`は除きましょう。
<sup>[[link](#method-parens)]</sup>

   ```Ruby
   # 悪い例
   def some_method()
     # 本文省略
   end

   # 良い例
   def some_method
     # 本文省略
   end

   # 悪い例
   def some_method_with_parameters param1, param2
     # 本文省略
   end

   # 良い例
   def some_method_with_parameters(param1, param2)
     # 本文省略
   end
   ```

* <a name="no-for-loops"></a>
  `for`は、どうしても使わなければいけない明確な理由が明言できる人以外は、使ってはいけません。
  多くの場合は代わりにイテレータを使うべきです。
  `for`は`each`をつかって実装されています(だから、より遠回しです)が、
  `for`は(`each`と違い)新しいスコープを導入せず、
  そのブロック内で定義された変数は、ブロックの外からも見えます。
<sup>[[link](#no-for-loops)]</sup>

  ```Ruby
  arr = [1, 2, 3]

  # 悪い例
  for elem in arr do
    puts elem
  end

  # elemはルーブの外からも参照できることに注意しましょう
  elem # => 3

  # 良い例
  arr.each { |elem| puts elem }

  # elemはeachブロックの外からは参照できません
  elem # => NameError: undefined local variable or method `elem'
  ```

* <a name="no-then"></a>
  `then`は複数行にまたがる`if/unless`では使ってはいけません。
<sup>[[link](#no-then)]</sup>

  ```Ruby
  # 悪い例
  if some_condition then
    # 本文省略
  end

  # 良い例
  if some_condition
    # 本文省略
  end
  ```

* <a name="same-line-condition"></a>
  複数行にまたがる`if/unless`では、条件式は常に`if/unless`と同じ行に置きましょう。
<sup>[[link](#same-line-condition)]</sup>

  ```Ruby
  # 悪い例
  if
    some_condition
    do_something
    do_something_else
  end

  # 良い例
  if some_condition
    do_something
    do_something_else
  end
  ```

* <a name="ternary-operator"></a>
  三項演算子(`?:`)を`if/then/else/end`構文よりも優先的に使いましょう。
  そちらの方がより一般的だし、あきらかに簡潔です。
<sup>[[link](#ternary-operator)]</sup>

  ```Ruby
  # 悪い例
  result = if some_condition then something else something_else end

  # 良い例
  result = some_condition ? something : something_else
  ```

* <a name="no-nested-ternary"></a>
  三項演算子の１つの分岐には１つだけ式を入れましょう。
  つまり、三項演算子はネストしてはいけません。
  そのようなケースでは`if/else`の方がよいです。
<sup>[[link](#no-nested-ternary)]</sup>

  ```Ruby
  # 悪い例
  some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

  # 良い例
  if some_condition
    nested_condition ? nested_something : nested_something_else
  else
    something_else
  end
  ```

* <a name="no-semicolon-ifs"></a>
  `if x; ...`を使ってはいけません。代わりに三項演算子を使いましょう。
<sup>[[link](#no-semicolon-ifs)]</sup>

  ```Ruby
  # 悪い例
  result = if some_condition; something else something_else end

  # 良い例
  result = some_condition ? something : something_else
  ```

* <a name="use-if-case-returns"></a>
  `if`や`case`が式で、値を返すという事実を活用しましょう。
<sup>[[link](#use-if-case-returns)]</sup>

  ```Ruby
  # 悪い例
  if condition
    result = x
  else
    result = y
  end

  # 良い例
  result =
    if condition
      x
    else
      y
    end
  ```

* <a name="one-line-cases"></a>
  １行の`case`文では`when x then ...`を使いましょう。
  代わりの表現である`when x: ...`は、Ruby 1.9で廃止されました。
<sup>[[link](#one-line-cases)]</sup>

* <a name="no-when-semicolons"></a>
  `when x; ...`を使ってはいけません。前のルールを見てください。
<sup>[[link](#no-when-semicolons)]</sup>

* <a name="bang-not-not"></a>
  `not`の代わりに`!`を使いましょう。
<sup>[[link](#bang-not-not)]</sup>

  ```Ruby
  # 悪い例 - 演算子優先順位のため、()が必要になります
  x = (not something)

  # 良い例
  x = !something
  ```

* <a name="no-bang-bang"></a>
  `!!`は避けましょう。
<sup>[[link](#no-bang-bang)]</sup>

  ```Ruby
  # 悪い例
  x = 'test'
  # obscure nil check
  if !!x
    # body omitted
  end

  x = false
  # 二重否定はbooleanとして役に立ちません。
  !!x # => false

  # 良い例
  x = 'test'
  unless x.nil?
    # body omitted
  end
  ```

* <a name="no-and-or-or"></a>
  `and`と`or`の使用は禁止です。使うべき理由がないです。
   常に、代わりに`&&`と`||`を使いましょう。
<sup>[[link](#no-and-or-or)]</sup>

  ```Ruby
  # 悪い例
  # boolean式
  if some_condition and some_other_condition
    do_something
  end

  # 制御構文
  document.saved? or document.save!

  # 良い例
  # boolean式
  if some_condition && some_other_condition
    do_something
  end

  # 制御構文
  document.saved? || document.save!
  ```

  留意しなければならないのは、このルールには例外([条件式中の安全な代入](#safe-assignment-in-condition))があるということです。

* <a name="no-multiline-ternary"></a>
  複数行にまたがる三項演算子`?:`は避けましょう; 代わりに`if/unless`を使いましょう。
<sup>[[link](#no-multiline-ternary)]</sup>

* <a name="if-as-a-modifier"></a>
  本文が１行のときは、`if/unless`修飾子を利用するのが好まれます。
  他の良い代替案としては`&&/||`を使った制御構文があります。
<sup>[[link](#if-as-a-modifier)]</sup>

  ```Ruby
  # 悪い例
  if some_condition
    do_something
  end

  # 良い例
  do_something if some_condition

  # もう１つの良い例
  some_condition && do_something
  ```

* <a name="no-multiline-if-modifiers"></a>
  複数行に渡るような些細とは言えない規模のブロックに`if/unless`修飾子を用いるのは避けましょう。
<sup>[[link](#no-multiline-if-modifiers)]</sup>

  ```Ruby
  # 悪い例
  10.times do
    # 複数行のbody省略
  end if some_condition

  # 良い例
  if some_condition
    10.times do
      # 複数行のbody省略
    end
  end
  ```

* <a name="unless-for-negatives"></a>
  否定形のときは`if`より`unless`が好まれます。(もしくは`||`構文を使いましょう)。
<sup>[[link](#unless-for-negatives)]</sup>

  ```Ruby
  # 悪い例
  do_something if !some_condition

  # 悪い例
  do_something if not some_condition

  # 良い例
  do_something unless some_condition

  # もう１つの良い例
  some_condition || do_something
  ```

* <a name="no-else-with-unless"></a>
  `unless`を`else`付きで使ってはいけません。
  肯定条件を先にして書き換えましょう。
<sup>[[link](#no-else-with-unless)]</sup>

  ```Ruby
  # 悪い例
  unless success?
    puts 'failure'
  else
    puts 'success'
  end

  # 良い例
  if success?
    puts 'success'
  else
    puts 'failure'
  end
  ```

* <a name="no-parens-if"></a>
  `if/unless/while/until`構文では`()`の使用は避けましょう。
<sup>[[link](#no-parens-if)]</sup>

  ```Ruby
  # 悪い例
  if (x > 10)
    # body omitted
  end

  # 良い例
  if x > 10
    # body omitted
  end
  ```

* <a name="no-multiline-while-do"></a>
  複数行の`while/until`では、`while/until condition do`を使ってはいけません。
<sup>[[link](#no-multiline-while-do)]</sup>

  ```Ruby
  # 悪い例
  while x > 5 do
    # 本文省略
  end

  until x > 5 do
    # 本文省略
  end

  # 良い例
  while x > 5
    # 本文省略
  end

  until x > 5
    # 本文省略
  end
  ```

* <a name="while-as-a-modifier"></a>
  本文が１行のときは、`while/until`修飾子を利用しましょう。
<sup>[[link](#while-as-a-modifier)]</sup>

  ```Ruby
  # 悪い例
  while some_condition
    do_something
  end

  # 良い例
  do_something while some_condition
  ```

* <a name="until-for-negatives"></a>
  否定形のときは、`while`よりも`until`の方が好まれます。
<sup>[[link](#until-for-negatives)]</sup>

  ```Ruby
  # 悪い例
  do_something while !some_condition

  # 良い例
  do_something until some_condition
  ```

* <a name="infinite-loop"></a>
  無限ループが必要な時は、`while/until`の代わりに`Kernel#loop`を用いましょう。
<sup>[[link](#infinite-loop)]</sup>

  ```Ruby
  # 悪い例
  while true
    do_something
  end

  until false
    do_something
  end

  loop do
    do_something
  end
  ```

* <a name="loop-with-break"></a>
  後判定ループの場合、`begin/end/until`や`begin/end/while`より、`break`付きの`Kernel#loop`が好まれます。
<sup>[[link](#loop-with-break)]</sup>

  ```Ruby
  # 悪い例
  begin
    puts val
    val += 1
  end while val < 0

  # 良い例
  loop do
    puts val
    val += 1
    break unless val < 0
  end
  ```

* <a name="no-dsl-parens"></a>
  内部DSL(例えばRake、Rails、RSpec)や、
  Rubyで「キーワード」と認識されているメソッド(例えば`attr_reader` や`puts`)や、
  アトリビュートにアクセスするメソッドでは、
  引数の周りの`()`を省略しましょう。
  それ以外のすべてのメソッドでは、メソッド呼び出しの時に括弧を付けましょう。
<sup>[[link](#no-dsl-parens)]</sup>

  ```Ruby
  class Person
    attr_reader :name, :age

    # 省略
  end

  temperance = Person.new('Temperance', 30)
  temperance.name

  puts temperance.age

  x = Math.sin(y)
  array.delete(e)

  bowling.score.should == 0
  ```

* <a name="no-braces-opts-hash"></a>
  暗黙のオプションハッシュの外側の`{}`は省略しましょう。
<sup>[[link](#no-braces-opts-hash)]</sup>

  ```Ruby
  # 悪い例
  user.set({ name: 'John', age: 45, permissions: { read: true } })

  # 良い例
  user.set(name: 'John', age: 45, permissions: { read: true })
  ```

* <a name="no-dsl-decorating"></a>
  内部DSLの一部として使われるメソッドの引数では、外側の`()`、`{}`は省略しましょう
<sup>[[link](#no-dsl-decorating)]</sup>

  ```Ruby
  class Person < ActiveRecord::Base
    # 悪い例
    validates(:name, { presence: true, length: { within: 1..10 } })

    # 良い例
    validates :name, presence: true, length: { within: 1..10 }
  end
  ```

* <a name="no-args-no-parens"></a>
  引数のないメソッド呼び出しの`()`は省略しましょう。
<sup>[[link](#no-args-no-parens)]</sup>

  ```Ruby
  # 悪い例
  Kernel.exit!()
  2.even?()
  fork()
  'test'.upcase()

  # 良い例
  Kernel.exit!
  2.even?
  fork
  'test'.upcase
  ```

* <a name="single-action-blocks"></a>
  ブロック内で呼び出されるメソッドがただ１つである場合、簡略化されたproc呼び出しを用いましょう。
<sup>[[link](#single-action-blocks)]</sup>

  ```Ruby
  # 悪い例
  names.map { |name| name.upcase }

  # 良い例
  names.map(&:upcase)
  ```

* <a name="single-line-blocks"></a>
  １行のブロックでは`do...end`より`{...}`の方が好まれます。
  複数行のブロックでは`{...}`は避けましょう
  (複数行のメソッドチェーンは常に醜いです)。
  制御構文(的な用法)やメソッド定義(的な用法)では常に`do...end`を使いましょう
  (例えばRakefilesや特定のDSLなど)
  メソッドチェーンでの`do...end`は避けましょう。
<sup>[[link](#single-line-blocks)]</sup>

  ```Ruby
  names = %w(Bozhidar Steve Sarah)

  # 悪い例
  names.each do |name|
    puts name
  end

  # 良い例
  names.each { |name| puts name }

  # 悪い例
  names.select do |name|
    name.start_with?('S')
  end.map { |name| name.upcase }

  # 良い例
  names.select { |name| name.start_with?('S') }.map(&:upcase)
  ```

  `{...}`を用いた複数行のメソッドチェーンをOKと主張する人もいるかもしれないが、
  自問してみてほしい - そのコードは本当に読みやすいだろうか？
  また、そのブロックの中はメソッドに切り出すことはできないのか？

* <a name="block-argument"></a>
  単に他のブロックに引数を渡すだけのブロックリテラルを避けるため、
  ブロック引数を明示することを検討しましょう。
  ただしブロックが`Proc`に変換されることでのパフォーマンスに気をつけましょう。
<sup>[[link](#block-argument)]</sup>

  ```Ruby
  require 'tempfile'

  # 悪い例
  def with_tmp_dir
    Dir.mktmpdir do |tmp_dir|
      Dir.chdir(tmp_dir) { |dir| yield dir }  # block just passes arguments
    end
  end

  # 良い例
  def with_tmp_dir(&block)
    Dir.mktmpdir do |tmp_dir|
      Dir.chdir(tmp_dir, &block)
    end
  end

  with_tmp_dir do |dir|
    puts "dir is accessible as parameter and pwd is set: #{dir}"
  end
  ```

* <a name="no-explicit-return"></a>
  制御構文上不要な`return`は避けましょう。
<sup>[[link](#no-explicit-return)]</sup>

  ```Ruby
  # 悪い例
  def some_method(some_arr)
    return some_arr.size
  end

  # 良い例
  def some_method(some_arr)
    some_arr.size
  end
  ```

* <a name="no-self-unless-required"></a>
  不要な`self`は避けましょう (`self`のアクセサへの書き込みでのみ必要です)。
<sup>[[link](#no-self-unless-required)]</sup>

  ```Ruby
  # 悪い例
  def ready?
    if self.last_reviewed_at > self.last_updated_at
      self.worker.update(self.content, self.options)
      self.status = :in_progress
    end
    self.status == :verified
  end

  # 良い例
  def ready?
    if last_reviewed_at > last_updated_at
      worker.update(content, options)
      self.status = :in_progress
    end
    status == :verified
  end
  ```

* <a name="no-shadowing"></a>
  当然の帰結として、ローカル変数でメソッドをシャドウイングするのは、
  それらが等価なものでない限り避けましょう。
<sup>[[link](#no-shadowing)]</sup>

  ```Ruby
  class Foo
    attr_accessor :options

    # ok
    def initialize(options)
      self.options = options
      # options と self.options はここでは等価
    end

    # 悪い例
    def do_something(options = {})
      unless options[:when] == :later
        output(self.options[:message])
      end
    end

    # 良い例
    def do_something(params = {})
      unless params[:when] == :later
        output(options[:message])
      end
    end
  end
  ```

* <a name="safe-assignment-in-condition"></a>
  代入部分を`()`で囲まずに、`=`の返り値を条件式に用いてはいけません。
  これは、Rubyistの中では *条件式内での安全な代入* としてとても有名です。
<sup>[[link](#safe-assignment-in-condition)]</sup>

  ```Ruby
  # 悪い例 (+ 警告が出ます)
  if v = array.grep(/foo/)
    do_something(v)
    ...
  end

  # 良い例 (MRIはこれでも文句を言いますが、RuboCopでは問題ありません)
  if (v = array.grep(/foo/))
    do_something(v)
    ...
  end

  # 良い例
  v = array.grep(/foo/)
  if v
    do_something(v)
    ...
  end
  ```

* <a name="self-assignment"></a>
  利用できるときには省略された自己代入演算子を用いましょう。
<sup>[[link](#self-assignment)]</sup>

  ```Ruby
  # 悪い例
  x = x + y
  x = x * y
  x = x**y
  x = x / y
  x = x || y
  x = x && y

  # 良い例
  x += y
  x *= y
  x **= y
  x /= y
  x ||= y
  x &&= y
  ```

* <a name="double-pipe-for-uninit"></a>
  変数がまだ初期化されていないときにだけ初期化したいのであれば、`||=`を使いましょう。
<sup>[[link](#double-pipe-for-uninit)]</sup>

  ```Ruby
  # 悪い例
  name = name ? name : 'Bozhidar'

  # 悪い例
  name = 'Bozhidar' unless name

  # 良い例 - nameがnilかfalseの場合のみ、Bozhidarで初期化します
  name ||= 'Bozhidar'
  ```

* <a name="no-double-pipes-for-bools"></a>
  boolean変数には`||=`を用いてはいけません
  (現在の値が`false`であったときに何が起こるか考えてみましょう)。
<sup>[[link](#no-double-pipes-for-bools)]</sup>

  ```Ruby
  # 悪い例 - たとえenabledがfalseでもtrueが入ります
  enabled ||= true

  # 良い例
  enabled = true if enabled.nil?
  ```

* <a name="double-amper-preprocess"></a>
  値が入っているかわからない変数の前処理のは`&&=`を用いましょう。
  `&&=`を使えば変数が存在するときのみ値を変更するので、
  存在確認に用いている不要な`if`を除去できます。
<sup>[[link](#double-amper-preprocess)]</sup>

  ```Ruby
  # 悪い例
  if something
    something = something.downcase
  end

  # 悪い例
  something = something ? something.downcase : nil

  # ok
  something = something.downcase if something

  # 良い例
  something = something && something.downcase

  # より良い例
  something &&= something.downcase
  ```

* <a name="no-case-equality"></a>
  case等価演算子`===`の露骨な使用は避けましょう。
  その名が示す通り、`case`の条件判定で用いられており、
  その外で用いられると混乱のもとになります。
<sup>[[link](#no-case-equality)]</sup>

  ```Ruby
  # 悪い例
  Array === something
  (1..100) === 7
  /something/ === some_string

  # 良い例
  something.is_a?(Array)
  (1..100).include?(7)
  some_string =~ /something/
  ```

* <a name="eql"></a>
  `==`で用が足りるなら`eql?`は使わないようにしましょう。
  `eq?`で実現されている、より厳密な等価性が必要になることは、実際には稀です。
<sup>[[link](#eql)]</sup>

  ```Ruby
  # 悪い例 - eql? は 文字列に対する == と同じです
  "ruby".eql? some_str

  # good
  "ruby" == some_str
  1.0.eql? x # eql? はFixnumとFloatの1を識別したいのであれば意味があります
  ```

* <a name="no-cryptic-perlisms"></a>
  Perlスタイルの(`$:`や`$;`などのような)特別な変数の使用は避けましょう。
  それらは極めて暗号的なので、ワンライナー以外での利用は推奨できません。
  `English`ライブラリから提供される人にやさしいエイリアスを用いましょう。
<sup>[[link](#no-cryptic-perlisms)]</sup>

  ```Ruby
  # 悪い例
  $:.unshift File.dirname(__FILE__)

  # 良い例
  require 'English'
  $LOAD_PATH.unshift File.dirname(__FILE__)
  ```

* <a name="parens-no-spaces"></a>
  メソッド名と引数の始まりの`(`の間にスペースを入れてはいけません。
<sup>[[link](#parens-no-spaces)]</sup>

  ```Ruby
  # 悪い例
  f (3 + 2) + 1

  # 良い例
  f(3 + 2) + 1
  ```

* <a name="parens-as-args"></a>
  メソッドの最初の引数が開き括弧で始まるならば、
  常にメソッド呼び出しに括弧を用いましょう。
  例えば次のように書きます
`f((3 + 2) + 1)`。
<sup>[[link](#parens-as-args)]</sup>

* <a name="always-warn-at-runtime"></a>
  Rubyインタープリタを走らせるときは、常に`-w`オプションを付けましょう。
  これまでのルールのどれかを忘れてしまった時に警告を出してくれます！
<sup>[[link](#always-warn-at-runtime)]</sup>

* <a name="no-nested-methods"></a>
  ネストしたメソッド定義は行ってはいけません - 代わりにラムダを用いましょう。
  ネストしたメソッド定義は実際には外側のメソッドと同じスコープ(例えばclass)でメソッドを生成します。
  そのうえ、そのようにネストしたメソッドは、そのメソッドを含んでいるメソッドがが呼び出されるたびに再定義されるでしょう。
<sup>[[link](#no-nested-methods)]</sup>

  ```Ruby
  # 悪い例
  def foo(x)
    def bar(y)
      # 本文略
    end

    bar(x)
  end

  # 良い例 - 前の例と同じですが、foo呼び出し時にのbar再定義がおこりません
  def bar(y)
    # 本文略
  end

  def foo(x)
    bar(x)
  end

  # こちらも良い例
  def foo(x)
    bar = ->(y) { ... }
    bar.call(x)
  end
  ```

* <a name="lambda-multi-line"></a>
  １行の本文を持つラムダには新しいリテラルを持ちましょう。
  `lambda`は複数行にまたがるときに使いましょう。
<sup>[[link](#lambda-multi-line)]</sup>

  ```Ruby
  # 悪い例
  l = lambda { |a, b| a + b }
  l.call(1, 2)

  # 正しい例、ですがギクシャクしています
  l = ->(a, b) do
    tmp = a * 7
    tmp * b / 50
  end

  # 良い例
  l = ->(a, b) { a + b }
  l.call(1, 2)

  l = lambda do |a, b|
    tmp = a * 7
    tmp * b / 50
  end
  ```

* <a name="stabby-lambda-with-args"></a>
  stabby lambdaを定義するときは、引数の周りの括弧は省略しないようにしましょう。
<sup>[[link](#stabby-lambda-with-args)]</sup>

  ```Ruby
  # bad
  l = ->x, y { something(x, y) }

  # good
  l = ->(x, y) { something(x, y) }
  ```

* <a name="proc"></a>
  `Proc.new`より`proc`を好みます。
<sup>[[link](#proc)]</sup>

  ```Ruby
  # 悪い例
  p = Proc.new { |n| puts n }

  # 良い例
  p = proc { |n| puts n }
  ```

* <a name="proc-call"></a>
  lambdaやprocの呼び出しには`proc[]`や`proc.()`より`proc.call()`を使いましょう。
<sup>[[link](#proc-call)]</sup>

  ```Ruby
  # 悪い例 - 列挙型のアクセスに似ているように見えます
  l = ->(v) { puts v }
  l[1]

  # こちらも悪い例 - 珍しい構文です
  l = ->(v) { puts v }
  l.(1)

  # 良い例
  l = ->(v) { puts v }
  l.call(1)
  ```

* <a name="underscore-unused-vars"></a>
  使わないブロック引数やローカル変数の先頭には`_`を付けましょう。
  単に`_`を用いるのも許容されます
  (少し説明不足ではありますが)。
  この記法を使うことで、
  RubyインタープリタやRubocopのような対応しているツールでは
  変数を使っていないという警告を抑制できます。
<sup>[[link](#underscore-unused-vars)]</sup>

  ```Ruby
  # 悪い例
  result = hash.map { |k, v| v + 1 }

  def something(x)
    unused_var, used_var = something_else(x)
  end

  # 良い例
  result = hash.map { |_, v| v + 1 }

  def something(x)
    _, used_var = something_else(x)
  end
  ```

* <a name="global-stdout"></a>
  `STDOUT/STDERR/STDIN`の代わりに`$stdout/$stderr/$stdin`を用いましょう。
  `STDOUT/STDERR/STDIN`は定数であり、
  Rubyでの定数は、実際は再代入できます(つまりリダイレクトに使えます)が、
  もし実行するとインタープリタからの警告が出ます。
<sup>[[link](#global-stdout)]</sup>

* <a name="warn"></a>
  `$stderr.puts`の代わりに`warn`を用いましょう。
  簡潔さや明快さもさることながら、
  `warn`は必要であれば警告を抑制することができます
  (警告レベルを`-W0`を用いて0に設定することによって実現できます)。
<sup>[[link](#warn)]</sup>

* <a name="sprintf"></a>
  あまりに暗号めいている`String#%`メソッドよりも`sprintf`や`format`を使いましょう。
<sup>[[link](#sprintf)]</sup>

  ```Ruby
  # 悪い例
  '%d %d' % [20, 10]
  # => '20 10'

  # 良い例
  sprintf('%d %d', 20, 10)
  # => '20 10'

  # 良い例
  sprintf('%{first} %{second}', first: 20, second: 10)
  # => '20 10'

  format('%d %d', 20, 10)
  # => '20 10'

  # 良い例
  format('%{first} %{second}', first: 20, second: 10)
  # => '20 10'
  ```

* <a name="array-join"></a>
  あまりに暗号めいている`Array#*`メソッドよりも`Array#join`を使いましょう。
<sup>[[link](#array-join)]</sup>

  ```Ruby
  # 悪い例
  %w(one two three) * ', '
  # => 'one, two, three'

  # 良い例
  %w(one two three).join(', ')
  # => 'one, two, three'
  ```

* <a name="splat-arrays"></a>
  配列かどうかわからない変数を配列とみなして処理したいときは、
  明示的に`Array`かどうかチェックするよりも、`[*var]`や`Array()`を使いましょう。
<sup>[[link](#splat-arrays)]</sup>

  ```Ruby
  # 悪い例
  paths = [paths] unless paths.is_a? Array
  paths.each { |path| do_something(path) }

  # 良い例
  [*paths].each { |path| do_something(path) }

  # 良い例 (そして少し読みやすいです)
  Array(paths).each { |path| do_something(path) }
  ```

* <a name="ranges-or-between"></a>
  ロジックを使って複雑な比較を行うよりも、
  可能な限り`Range`や`Comparable#between?`を用いましょう。
<sup>[[link](#ranges-or-between)]</sup>

  ```Ruby
  # 悪い例
  do_something if x >= 1000 && x <= 2000

  # 良い例
  do_something if (1000..2000).include?(x)

  # 良い例
  do_something if x.between?(1000, 2000)
  ```

* <a name="predicate-methods"></a>
  `==`を明示した比較よりも判定メソッドを用いましょう。
  数値の比較はOKです。
<sup>[[link](#predicate-methods)]</sup>

  ```Ruby
  # 悪い例
  if x % 2 == 0
  end

  if x % 2 == 1
  end

  if x == nil
  end

  # 良い例
  if x.even?
  end

  if x.odd?
  end

  if x.nil?
  end

  if x.zero?
  end

  if x == 0
  end
  ```

* <a name="no-non-nil-checks"></a>
  boolean値を扱わない限り、明示的な`nil`でないかの検査は避けましょう。
<sup>[[link](#no-non-nil-checks)]</sup>

  ```Ruby
  # 悪い例
  do_something if !something.nil?
  do_something if something != nil

  # 良い例
  do_something if something

  # 良い例 - boolean値を扱うとき
  def value_set?
    !@some_boolean.nil?
  end
  ```

* <a name="no-BEGIN-blocks"></a>
  `BEGIN`ブロックの使用は避けましょう。
<sup>[[link](#no-BEGIN-blocks)]</sup>

* <a name="no-END-blocks"></a>
  `END`ブロックを使ってはいけません。代わりに`Kernel#at_exit`を使いましょう。
<sup>[[link](#no-END-blocks)]</sup>

  ```ruby
  # 悪い例

  END { puts 'Goodbye!' }

  # 良い例

  at_exit { puts 'Goodbye!' }
  ```

* <a name="no-flip-flops"></a>
  フリップフロップの使用は避けましょう。
<sup>[[link](#no-flip-flops)]</sup>

* <a name="no-nested-conditionals"></a>
  制御構文で条件式のネストは避けましょう。
<sup>[[link](#no-nested-conditionals)]</sup>

  不正なデータを弾きたいときはガード節を使いましょう。
  ガード節とは、できるだけ素早く関数から抜けられるようにと
  関数の先頭に置かれている条件文のことです。

  ```Ruby
  # 悪い例
  def compute_thing(thing)
    if thing[:foo]
      update_with_bar(thing)
      if thing[:foo][:bar]
        partial_compute(thing)
      else
        re_compute(thing)
      end
    end
  end

  # 良い例
  def compute_thing(thing)
    return unless thing[:foo]
    update_with_bar(thing[:foo])
    return re_compute(thing) unless thing[:foo][:bar]
    partial_compute(thing)
  end
  ```

  ループ内では条件判定ブロックよりも`next`が好まれます。
  ```Ruby
  # 悪い例
  [0, 1, 2, 3].each do |item|
    if item > 1
      puts item
    end
  end

  # 良い例
  [0, 1, 2, 3].each do |item|
    next unless item > 1
    puts item
  end
  ```
* <a name="map-find-select-reduce-size"></a>
  `collect`より`map`、`detect`より`find`、`find_all`より`select`
  `inject`より`reduce`、`length`より`size`を使いましょう。
  これは絶対のルールではないです。
  別名のほうが可読性に優れているなら、
  そちらを使っていただいて構いません。
  韻を踏んでいるほうのメソッド名はSmalltalkから引き継いできたもので、
  他のプログラミング言語でそこまで一般的ではないです。
  `find_all`よりも`select`が推奨されるのは、
  `reject`との相性がよいことと、
  メソッド名から挙動を推察することも容易だからです。
<sup>[[link](#map-find-select-reduce-size)]</sup>

* <a name="count-vs-size"></a>
  `size`の代わりに`count`を用いてはいけません。
  `Array`以外の`Enumerable`オブジェクトでは、
  `count`を使うと要素数の計算のためにコレクション全体を走査してしまいます。
<sup>[[link](#count-vs-size)]</sup>

  ```Ruby
  # 悪い例
  some_hash.count

  # 良い例
  some_hash.size
  ```

* <a name="flat-map"></a>
  `map`と`flatten`の組み合わせの代わりに、`flat_map`を用いましょう。
  これは深さが２以上の配列には適用できません。
  すなわち、`users.first.songs == ['a', ['b','c']]`のときは、
  `flat_map`より`map + flatten`を用いましょう。
  `flatten`は配列を全て平坦にするのに対し、`flat_map`は配列を１次元だけ平坦にします。
<sup>[[link](#flat-map)]</sup>

  ```Ruby
  # 悪い例
  all_songs = users.map(&:songs).flatten.uniq

  # 良い例
  all_songs = users.flat_map(&:songs).uniq
  ```

* <a name="reverse-each"></a>
  `reverse.each`の代わりに`reverse_each`を用いましょう。
  何故なら、`Enumerable`をincludeしているクラスの側で、
  より効率のよい実装が行われていることがあるからです。
  最悪、クラスが特殊化を行っていない場合でも、`Enumerable`から継承される一般的な実装は、
  `reverse.each`を用いた場合と同じ効率です。
<sup>[[link](#reverse-each)]</sup>

  ```Ruby
  # 悪い例
  array.reverse.each { ... }

  # 良い例
  array.reverse_each { ... }
  ```

## 命名規則

> プログラミングで真に困難な領域は、キャッシュの無効化と命名にしかない。 <br>
> -- Phil Karlton

* <a name="english-identifiers"></a>
  識別子は英語で名づけましょう。
<sup>[[link](#english-identifiers)]</sup>

  ```Ruby
  # 悪い例 - 識別子がnon-asciiな文字列です
  заплата = 1_000

  # 悪い例 - (キリル文字の代わりに)ラテン文字で書かれてはいますが、識別子がブルガリア語です
  zaplata = 1_000

  # 良い例
  salary = 1_000
  ```

* <a name="snake-case-symbols-methods-vars"></a>
  シンボル、メソッド、変数には`snake_case`を用いましょう。
<sup>[[link](#snake-case-symbols-methods-vars)]</sup>

  ```Ruby
  # 悪い例
  :'some symbol'
  :SomeSymbol
  :someSymbol

  someVar = 5

  def someMethod
    ...
  end

  def SomeMethod
   ...
  end

  # 良い例
  :some_symbol

  def some_method
    ...
  end
  ```

* <a name="camelcase-classes"></a>
  クラスやモジュールには`CamelCase`を用いましょう。(HTTP、RFC、XMLのような頭字語は大文字を保ちましょう)。
<sup>[[link](#camelcase-classes)]</sup>

  ```Ruby
  # 悪い例
  class Someclass
    ...
  end

  class Some_Class
    ...
  end

  class SomeXml
    ...
  end

  # 良い例
  class SomeClass
    ...
  end

  class SomeXML
    ...
  end
  ```

* <a name="snake-case-files"></a>
  ファイル名には`snake_case`を用いましょう。例えば`hello_world.rb`のように。
<sup>[[link](#snake-case-files)]</sup>

* <a name="snake-case-dirs"></a>
  ディレクトリ名には`snake_case`を用いましょう。例えば`lib/hello_world/hello_world.rb`のように。
<sup>[[link](#snake-case-dirs)]</sup>


* <a name="one-class-per-file"></a>
  ソースファイル１つにつきただ１つのクラス/モジュールだけが書かれている状態を目指しましょう。
  そのファイルの名前はそのクラス/モジュールと同じ名前で、ただしキャメルケースをスネークケースに変換して用いましょう。
<sup>[[link](#one-class-per-file)]</sup>

* <a name="screaming-snake-case"></a>
  他の定数は`SCREAMING_SNAKE_CASE`を用いましょう。
<sup>[[link](#screaming-snake-case)]</sup>

  ```Ruby
  # 悪い例
  SomeConst = 5

  # 良い例
  SOME_CONST = 5
  ```

* <a name="bool-methods-qmark"></a>
  述語メソッド(boolean値が返るメソッド)は疑問符で終わりましょう。
  (すなわち`Array#empty?`のように)。
  boolean値を返さないメソッドは、疑問符で終わるべきではないです。
<sup>[[link](#bool-methods-qmark)]</sup>

* <a name="dangerous-method-bang"></a>
  *危険* な可能性のあるメソッド
  (引数や`self`を変更するようなメソッドや、
  `exit!`(`exit`と違ってファイナライザが走らない)のようなもの)
  は、その安全なバージョンがある場合には、 *危険* であることを明示する意味で感嘆符で終わりましょう。
<sup>[[link](#dangerous-method-bang)]</sup>

  ```Ruby
  # 悪い例 - 対応する「安全」なメソッドが存在しません
  class Person
    def update!
    end
  end

  # 良い例
  class Person
    def update
    end
  end

  # 良い例
  class Person
    def update!
    end

    def update
    end
  end
  ```

* <a name="safe-because-unsafe"></a>
  危険な(感嘆符付き)メソッドがあるときは、対応する安全な(感嘆符なし)メソッドを定義できないか検討しましょう。
<sup>[[link](#safe-because-unsafe)]</sup>

  ```Ruby
  class Array
    def flatten_once!
      res = []

      each do |e|
        [*e].each { |f| res << f }
      end

      replace(res)
    end

    def flatten_once
      dup.flatten_once!
    end
  end
  ```

* <a name="reduce-blocks"></a>
  短いブロックと共に`reduce`を使うとき、引数は`|a, e|`と名づけましょう。
  (accumulator, element).
<sup>[[link](#reduce-blocks)]</sup>

* <a name="other-arg"></a>
  二項演算子を定義するとき、引数名は`other`を用いましょう
  (`<<`と`[]`は意味が違ってくるので、このルールの例外です)。
<sup>[[link](#other-arg)]</sup>

  ```Ruby
  def +(other)
    # body omitted
  end
  ```

## コメント

> 良く書けたコードは、それ自身が最良のドキュメントでもある。
> コメントを書こうとしている時は、常に自問してほしい、
> "このコメントが不要になるようにコードを改善できるだろうか？"
> コードを改善した上で、ドキュメントでさらに明快にするのだ。
> -- Steve McConnell

* <a name="no-comments"></a>
  自己説明的なコードを書いて、このセクションの残りのパートは無視しましょう。本当に！
<sup>[[link](#no-comments)]</sup>

* <a name="english-comments"></a>
  コメントは英語で書きましょう。
<sup>[[link](#english-comments)]</sup>

* <a name="hash-space"></a>
  最初の`#`とコメントの間にスペースを１つ入れましょう。
<sup>[[link](#hash-space)]</sup>

* <a name="english-syntax"></a>
  １語より長いコメントは頭語を大文字化してピリオドを打ちましょう。
  文と文の間にはスペースを[一つだけ](https://en.wikipedia.org/wiki/Sentence_spacing)入れましょう。
<sup>[[link](#english-syntax)]</sup>

* <a name="no-superfluous-comments"></a>
  過剰なコメントは避けましょう。
<sup>[[link](#no-superfluous-comments)]</sup>

  ```Ruby
  # 悪い例
  counter += 1 # カウンターをインクリメント
  ```

* <a name="comment-upkeep"></a>
  コメントは最新に保ちましょう。
  古くなったコメントは、コメントがないより悪いです。
<sup>[[link](#comment-upkeep)]</sup>

> 良いコードは良いジョークのようだ - なんの説明もいらない。<br>
> -- Russ Olsen

* <a name="refactor-dont-comment"></a>
  悪いコードを説明するコメントは避けましょう。
  自己説明的なコードへのリファクタリングを行いましょう
  (やるかやらないか - "やってみる"はなしだ。 --Yoda)。
<sup>[[link](#refactor-dont-comment)]</sup>

### 注釈

* <a name="annotate-above"></a>
  注釈は、通常関連するコードのすぐ上に書きましょう。
<sup>[[link](#annotate-above)]</sup>

* <a name="annotate-keywords"></a>
  注釈のキーワードの後ろは`: `を続けましょう。
  その後ろに問題点を書きましょう。
<sup>[[link](#annotate-keywords)]</sup>

* <a name="indent-annotations"></a>
  もし問題点の記述に複数行かかる場合は、
  後続の行は`#`の後ろにスペース３つでインデントしましょう。
  (通常の１つに加え、インデント目的に２つ)
<sup>[[link](#indent-annotations)]</sup>

  ```Ruby
  def bar
    # FIXME: This has crashed occasionally since v3.2.1. It may
    #   be related to the BarBazUtil upgrade.
    baz(:quux)
  end
  ```

* <a name="rare-eol-annotations"></a>
  もし問題が明らかで、説明すると冗長になる時は、
  問題のある行の末尾に、本文なしの注釈だけ付けましょう。
  この用法は例外であり、ルールではありません。
<sup>[[link](#rare-eol-annotations)]</sup>

    ```Ruby
    def bar
      sleep 100 # OPTIMIZE
    end
    ```

* <a name="todo"></a>
  あとで追加されるべき、今はない特徴や機能の注釈には`TODO`を使いましょう。
<sup>[[link](#todo)]</sup>

* <a name="fixme"></a>
  直す必要がある壊れたコードの注釈には`FIXME`を使いましょう。
<sup>[[link](#fixme)]</sup>

* <a name="optimize"></a>
  パフォーマンスに問題を及ぼすかもしれない遅い、または非効率なコードの注釈には`OPTIMIZE`を使いましょう。
<sup>[[link](#optimize)]</sup>

* <a name="hack"></a>
  疑問の残るコードの書き方でコードの臭いを感じた箇所の注釈には`HACK`を使いましょう。
<sup>[[link](#hack)]</sup>

* <a name="review"></a>
  意図したとおりに動くか確認する必要がある箇所の注釈には`REVIEW`を使いましょう。
  例: `REVIEW: Are we sure this is how the client does X currently?`
<sup>[[link](#review)]</sup>

* <a name="document-annotations"></a>
  適切に感じるのであれば、他の独自のキーワードを用いても構いませんが、
  それらのキーワードは`README`やそれに類するものに書いておきましょう。
<sup>[[link](#document-annotations)]</sup>

## クラスとモジュール

* <a name="consistent-classes"></a>
  クラス定義の構造には一貫性をもたせましょう。
<sup>[[link](#consistent-classes)]</sup>

  ```Ruby
  class Person
    # extend や include を最初に行います
    extend SomeModule
    include AnotherModule

    # 定数定義はその次です
    SOME_CONSTANT = 20

    # その後ろはアトリビュートマクロです
    attr_reader :name

    # 他のマクロが続きます(もしあれば)
    validates :name

    # public class methods が次に来ます
    def self.some_method
    end

    # initializeはclass methodsと他のinstance methodsの間に来ます
    def initialize
    end

    # 他のpublic instance methods が続きます
    def some_method
    end

    # protected and private methods は後ろの方にまとめます
    protected

    def some_protected_method
    end

    private

    def some_private_method
    end
  end
  ```

* <a name="file-classes"></a>
  クラスの中に複数行あるようなクラスをネストしてはいけません。
  それぞれのクラスごとにファイルに分けて、
  外側のクラスの名前のついたフォルダに含めるようにしましょう。
<sup>[[link](#file-classes)]</sup>

  ```Ruby
  # 悪い例

  # foo.rb
  class Foo
    class Bar
      # 中に30メソッド
    end

    class Car
      # 中に20メソッド
    end

    # 中に30メソッド
  end

  # 良い例

  # foo.rb
  class Foo
    # 中に30メソッド
  end

  # foo/bar.rb
  class Foo
    class Bar
      # 中に30メソッド
    end
  end

  # foo/car.rb
  class Foo
    class Car
      # 中に20メソッド
    end
  end
  ```

* <a name="modules-vs-classes"></a>
  クラスメソッドしかないクラスはモジュールであることが好まれます。
  クラスはインスタンスを生成することにのみ意味があります。
<sup>[[link](#modules-vs-classes)]</sup>

  ```Ruby
  # 悪い例
  class SomeClass
    def self.some_method
      # body omitted
    end

    def self.some_other_method
    end
  end

  # 良い例
  module SomeModule
    module_function

    def some_method
      # body omitted
    end

    def some_other_method
    end
  end
  ```

* <a name="module-function"></a>
  モジュールのインスタンスメソッドをクラスメソッドにしたいときは、
  `extend self`よりも`module_function`が好まれます。
<sup>[[link](#module-function)]</sup>

  ```Ruby
  # 悪い例
  module Utilities
    extend self

    def parse_something(string)
      # do stuff here
    end

    def other_utility_method(number, string)
      # do some more stuff
    end
  end

  # 良い例
  module Utilities
    module_function

    def parse_something(string)
      # do stuff here
    end

    def other_utility_method(number, string)
      # do some more stuff
    end
  end
  ```

* <a name="liskov"></a>
  クラス階層の設計を行うときは、
  [リスコフの置換原則](http://ja.wikipedia.org/wiki/%E3%83%AA%E3%82%B9%E3%82%B3%E3%83%95%E3%81%AE%E7%BD%AE%E6%8F%9B%E5%8E%9F%E5%89%87).
  に従いましょう。
<sup>[[link](#liskov)]</sup>

* <a name="solid-design"></a>
  あなたのクラスを可能な限り
  [SOLID](http://en.wikipedia.org/wiki/SOLID_(object-oriented_design))
  に保ちましょう。
<sup>[[link](#solid-design)]</sup>

* <a name="define-to-s"></a>
  ドメインオブジェクトのクラスにおいては常に適切な`to_s`メソッドを提供しましょう。
<sup>[[link](#define-to-s)]</sup>

  ```Ruby
  class Person
    attr_reader :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end

    def to_s
      "#{@first_name} #{@last_name}"
    end
  end
  ```

* <a name="attr_family"></a>
  単純なアクセサやミューテータの定義には、`attr`群を用いましょう。
<sup>[[link](#attr_family)]</sup>

  ```Ruby
  # 悪い例
  class Person
    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end

    def first_name
      @first_name
    end

    def last_name
      @last_name
    end
  end

  # 良い例
  class Person
    attr_reader :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end
  end
  ```

* <a name="attr"></a>
  `attr`の使用は避けましょう。代わりに`attr_reader`や`attr_accessor`を使いましょう。
<sup>[[link](#attr)]</sup>

  ```Ruby
  # 悪い例 - １つのアクセサしか作れません(1.9で廃止されました)
  attr :something, true
  attr :one, :two, :three # attr_readerと同じです

  # 良い例
  attr_accessor :something
  attr_reader :one, :two, :three
  ```

* <a name="struct-new"></a>
  `Struct.new`の使用を考えましょう、
  それは、単純なアクセサ、コンストラクタや比較演算子を定義してくれます。
<sup>[[link](#struct-new)]</sup>

  ```Ruby
  # 良い例
  class Person
    attr_accessor :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end
  end

  # より良い例
  Person = Struct.new(:first_name, :last_name) do
  end
  ````

* <a name="no-extend-struct-new"></a>
  `Struct.new`で初期化されたインスタンスを拡張してはいけません。
  それは余分なクラスレベルをもたらし、
  複数回`require`された時に、奇妙なエラーの原因にもなります。
<sup>[[link](#no-extend-struct-new)]</sup>

  ```Ruby
  # 悪い例
  class Person < Struct.new(:first_name, :last_name)
  end

  # 良い例
  Person = Struct.new(:first_name, :last_name)
  ````

* <a name="factory-methods"></a>
  あるクラスのインスタンス生成する追加の方法を提供したいときは、
  ファクトリメソッドの追加を検討しましょう。
<sup>[[link](#factory-methods)]</sup>

  ```Ruby
  class Person
    def self.create(options_hash)
      # body omitted
    end
  end
  ```

* <a name="duck-typing"></a>
  継承より[ダック・タイピング](http://ja.wikipedia.org/wiki/%E3%83%80%E3%83%83%E3%82%AF%E3%83%BB%E3%82%BF%E3%82%A4%E3%83%94%E3%83%B3%E3%82%B0)が好まれます。
<sup>[[link](#duck-typing)]</sup>

  ```Ruby
  # 悪い例
  class Animal
    # abstract method
    def speak
    end
  end

  # 継承
  class Duck < Animal
    def speak
      puts 'Quack! Quack'
    end
  end

  # 継承
  class Dog < Animal
    def speak
      puts 'Bau! Bau!'
    end
  end

  # 良い例
  class Duck
    def speak
      puts 'Quack! Quack'
    end
  end

  class Dog
    def speak
      puts 'Bau! Bau!'
    end
  end
  ```

* <a name="no-class-vars"></a>
  継承での振る舞いが"扱いづらい"ので、クラス変数(`@@`)の使用は避けましょう。
<sup>[[link](#no-class-vars)]</sup>

  ```Ruby
  class Parent
    @@class_var = 'parent'

    def self.print_class_var
      puts @@class_var
    end
  end

  class Child < Parent
    @@class_var = 'child'
  end

  Parent.print_class_var # => will print "child"
  ```

  このように、ひとつのクラス階層に属するすべてのクラスは、
  １つのクラス変数を共有してしまいます。
  クラス変数よりもクラスのインスタンス変数のほうを使うべきです。

* <a name="visibility"></a>
  意図した使い方に沿って、可視性(`private`、`protected`)を設定しましょう。
  全てを`public`(デフォルトの設定)のままにしないようにしましょう。
  結局私達は今 *Ruby* を書いているのだから。 *Python* ではなく。
<sup>[[link](#visibility)]</sup>

* <a name="indent-public-private-protected"></a>
  `public`、`protected`、`private`は、適用するメソッド定義と同じインデントにしましょう。
  そして、以降のすべてのメソッド定義に適用されることを強調するために、
  それらの修飾子の前１行と後１行に空行を入れましょう。
<sup>[[link](#indent-public-private-protected)]</sup>

  ```Ruby
  class SomeClass
    def public_method
      # ...
    end

    private

    def private_method
      # ...
    end

    def another_private_method
      # ...
    end
  end
  ```

* <a name="def-self-singletons"></a>
  シングルトンメソッドを定義するときは`def self.method`を用いましょう。
  クラス名を繰り返さないので、簡単にリファクタリングできるようになります。
<sup>[[link](#def-self-singletons)]</sup>

  ```Ruby
  class TestClass
    # 悪い例
    def TestClass.some_method
      # body omitted
    end

    # 良い例
    def self.some_other_method
      # body omitted
    end

    # たくさんのシングルトンメソッドを定義しなければならない時
    # この書き方も便利で、許容できます。
    class << self
      def first_method
        # body omitted
      end

      def second_method_etc
        # body omitted
      end
    end
  end
  ```

* <a name="alias-method-lexically"></a>
  メソッドの別名をつける時は`alias`を使いましょう。
  クラスのレキシカルスコープの中では`self`と同じように名前解決されます。
  またユーザーにとっても、実行時やサブクラス側で明示的にエイリアスを変更しなければ、
  変更されないことが読み取りやすいです。
<sup>[[link](#alias-method-lexically)]</sup>

  ```Ruby
  class Westerner
    def first_name
      @names.first
    end

    alias given_name first_name
  end
  ```

  `alias`は`def`のと同じく予約語なので、シンボルや文字列よりもベアワードが好まれます。
  言い換えると、`alias :foo :bar`ではなく、`alias foo bar`と書きましょう。

  また、Rubyがエイリアスや継承をどのように扱うか注意しましょう。
  `alias`はそれが定義された地点で解決されたメソッドを参照します。
  動的には解決されません。

  ```Ruby
  class Fugitive < Westerner
    def first_name
      'Nobody'
    end
  end
  ```

  この例では、`Fugitive#given_name`は、`Fugitive#first_name`ではなく、オリジナルの`Westerner#first_name`を呼び出します。
  `Fugitive#given_name`もオーバーライドしたい時は、継承したクラスでも
  再定義しなければなりません。

  ```Ruby
  class Fugitive < Westerner
    def first_name
      'Nobody'
    end

    alias given_name first_name
  end
  ```

* <a name="alias-method"></a>
  モジュールやクラス、実行時のシングルトンクラス等では、
  `alias`の挙動が予期できないので、
  エイリアス定義には常に`alias_method`を用いましょう。
<sup>[[link](#alias-method)]</sup>

  ```Ruby
  module Mononymous
    def self.included(other)
      other.class_eval { alias_method :full_name, :given_name }
    end
  end

  class Sting < Westerner
    include Mononymous
  end
  ```

## 例外

* <a name="fail-method"></a>
  例外は`fail`を使って発生させましょう。
  `raise`は例外をキャッチして、再度発生させるときにのみ使いましょう
  (何故なら、ここでは失敗(fail)ではなく、明示的に意図的に例外を上げ(raise)ているからです)。
<sup>[[link](#fail-method)]</sup>

  ```Ruby
  begin
    fail 'Oops'
  rescue => error
    raise if error.message != 'Oops'
  end
  ```

* <a name="no-explicit-runtimeerror"></a>
  ２引数の`fail/raise`では、`RuntimeError`を明示しないようにしましょう。
<sup>[[link](#no-explicit-runtimeerror)]</sup>

  ```Ruby
  # 悪い例
  fail RuntimeError, 'message'

  # 良い例 - デフォルトでRuntimeErrorが発生します
  fail 'message'
  ```

* <a name="exception-class-messages"></a>
  例外インスタンスの代わりに、
  例外クラスとメッセージが分かれている`fail/raise`が好まれます。
<sup>[[link](#exception-class-messages)]</sup>

  ```Ruby
  # 悪い例
  fail SomeException.new('message')
  # `fail SomeException.new('message'), backtrace`とする書き方が存在しないことに注意しましょう。

  # 良い例
  fail SomeException, 'message'
  # `fail SomeException, 'message', backtrace`の用法と一貫性があります
  ```

* <a name="no-return-ensure"></a>
  `ensure`ブロックから`return`してはいけません。
  もし`ensure`の中から明示的に値を返した場合は、
  `return`はどの例外発生よりも優先されて、
  例外など発生していなかったかのように値を返してしまいます。
  事実上、例外は静かに捨てられます。
<sup>[[link](#no-return-ensure)]</sup>

  ```Ruby
  def foo
    fail
  ensure
    return 'very bad idea'
  end
  ```

* <a name="begin-implicit"></a>
  可能な場所では、 *暗黙のbeginブロック* を用いましょう。
<sup>[[link](#begin-implicit)]</sup>

  ```Ruby
  # 悪い例
  def foo
    begin
      # main logic goes here
    rescue
      # failure handling goes here
    end
  end

  # 良い例
  def foo
    # main logic goes here
  rescue
    # failure handling goes here
  end
  ```

* <a name="contingency-methods"></a>
  *不確実性のあるメソッド*(Avdi Grimmによって作られた言葉です)
  を用いて`begin`の蔓延を和らげましょう。
<sup>[[link](#contingency-methods)]</sup>

  ```Ruby
  # 悪い例
  begin
    something_that_might_fail
  rescue IOError
    # handle IOError
  end

  begin
    something_else_that_might_fail
  rescue IOError
    # handle IOError
  end

  # 良い例
  def with_io_error_handling
    yield
  rescue IOError
    # handle IOError
  end

  with_io_error_handling { something_that_might_fail }

  with_io_error_handling { something_else_that_might_fail }
  ```

* <a name="dont-hide-exceptions"></a>
  例外をもみ消してはいけません。
<sup>[[link](#dont-hide-exceptions)]</sup>

  ```Ruby
  # 悪い例
  begin
    # an exception occurs here
  rescue SomeError
    # the rescue clause does absolutely nothing
  end

  # 悪い例
  do_something rescue nil
  ```

* <a name="no-rescue-modifiers"></a>
  `rescue`を修飾子として利用するのは避けましょう。
<sup>[[link](#no-rescue-modifiers)]</sup>

  ```Ruby
  # 悪い例 - StandardErrorとそれを継承した全てのクラスをキャッチしてしまいます
  read_file rescue handle_error($!)

  # 良い例 - Errno::ENOENTとそれを継承したクラスのみをキャッチします
  def foo
    read_file
  rescue Errno::ENOENT => ex
    handle_error(ex)
  end
  ```


* <a name="no-exceptional-flows"></a>
  制御フローに例外を使っては行けません。
<sup>[[link](#no-exceptional-flows)]</sup>

  ```Ruby
  # 悪い例
  begin
    n / d
  rescue ZeroDivisionError
    puts 'Cannot divide by 0!'
  end

  # 良い例
  if d.zero?
    puts 'Cannot divide by 0!'
  else
    n / d
  end
  ```

* <a name="no-blind-rescues"></a>
  `Exception`を`rescue`するのは避けましょう。
  これは`exit`のシグナルも捕捉するため、プロセスを殺すのに`kill -9`が必要になります。
<sup>[[link](#no-blind-rescues)]</sup>

  ```Ruby
  # 悪い例
  begin
    # calls to exit and kill signals will be caught (except kill -9)
    exit
  rescue Exception
    puts "you didn't really want to exit, right?"
    # exception handling
  end

  # 良い例
  begin
    # a blind rescue rescues from StandardError, not Exception as many
    # programmers assume.
  rescue => e
    # exception handling
  end

  # こちらも良い例
  begin
    # an exception occurs here

  rescue StandardError => e
    # exception handling
  end

  ```

* <a name="exception-ordering"></a>
  より詳細な例外を`rescue`チェーンの上に配置しましょう。
  そうでなければ、決して`rescue`されません。
<sup>[[link](#exception-ordering)]</sup>

  ```Ruby
  # 悪い例
  begin
    # 処理
  rescue Exception => e
    # エラー処理
  rescue StandardError => e
    # 決して到達しないエラー処理
  end

  # 良い例
  begin
    # 処理
  rescue StandardError => e
    # エラー処理
  rescue Exception => e
    # エラー処理
  end
  ```

* <a name="release-resources"></a>
  プログラム内で確保した外部リソースは、`ensure`で開放しましょう
<sup>[[link](#release-resources)]</sup>

  ```Ruby
  f = File.open('testfile')
  begin
    # .. process
  rescue
    # .. handle error
  ensure
    f.close if f
  end
  ```

* <a name="auto-release-resources"></a>
  自動的にリソースを開放してくれる機能を含むメソッドを利用可能な時は、そちらを使いましょう。
<sup>[[link](#auto-release-resources)]</sup>

  ```Ruby
  # 悪い例 - 明示的にファイルディスクリプタを閉じる必要が有ります
  f = File.open('testfile')
    # ...
  f.close

  # 良い例 - ファイルディスクリプタは自動的に閉じられます
  File.open('testfile') do |f|
    # ...
  end
  ```

* <a name="standard-exceptions"></a>
  新しい例外クラスを導入するより、基本ライブラリの例外クラスを用いることが好まれます。
<sup>[[link](#standard-exceptions)]</sup>

## コレクション

* <a name="literal-array-hash"></a>
  配列やハッシュを生成する時はリテラル記法を使いましょう。
  (コンストラクタに引数を渡す場合を除けば、ということですが)
<sup>[[link](#literal-array-hash)]</sup>

  ```Ruby
  # 悪い例
  arr = Array.new
  hash = Hash.new

  # 良い例
  arr = []
  hash = {}
  ```

* <a name="percent-w"></a>
  (空文字列や、文字列内にスペースが入っていない)文字列の配列構文は、
  `%w`リテラルの方が好まれます。
  このルールは要素が２つ以上の配列に適用されます。
<sup>[[link](#percent-w)]</sup>

  ```Ruby
  # 悪い例
  STATES = ['draft', 'open', 'closed']

  # 良い例
  STATES = %w(draft open closed)
  ```

* <a name="percent-i"></a>
  シンボルの配列が必要なときは`%i`が好まれます
  (Ruby 1.9との互換性の維持が必要で無ければ)。
  このルールは要素が２つ以上の配列に適用されます。
<sup>[[link](#percent-i)]</sup>

  ```Ruby
  # 悪い例
  STATES = [:draft, :open, :closed]

  # 良い例
  STATES = %i(draft open closed)
  ```

* <a name="no-trailing-array-commas"></a>
  `Array`や`Hash`リテラルの最後の要素の後ろの`,`は避けましょう。
  複数行にわかれていない時は特に避けましょう。
<sup>[[link](#no-trailing-array-commas)]</sup>

  ```Ruby
  # 悪い例 - 簡単に要素を移動・追加・削除できますが、それでも好まれません。
  VALUES = [
             1001,
             2020,
             3333,
           ]

  # 悪い例
  VALUES = [1001, 2020, 3333, ]

  # 良い例
  VALUES = [1001, 2020, 3333]
  ```

* <a name="no-gappy-arrays"></a>
  配列に大きな隙間を作るのは避けましょう。
<sup>[[link](#no-gappy-arrays)]</sup>

  ```Ruby
  arr = []
  arr[100] = 1 # now you have an array with lots of nils
  ```

* <a name="first-and-last"></a>
  配列の最初や最後にアクセスしたいときは、
  `[0]`や`[-1]`より`first`や`last`が好まれます。
<sup>[[link](#first-and-last)]</sup>

* <a name="set-vs-array"></a>
  要素が一意のものを扱うときは、`Array`の代わりに`Set`を用いましょう。
  `Set`は要素に重複と順序がないようなコレクションの実装です。
  これは`Array`の直感的な二項演算子と、`Hash`の速さが合わさっています。
<sup>[[link](#set-vs-array)]</sup>

* <a name="symbols-as-keys"></a>
  ハッシュのキーには文字列よりシンボルが好まれます。
<sup>[[link](#symbols-as-keys)]</sup>

  ```Ruby
  # 悪い例
  hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

  # 良い例
  hash = { one: 1, two: 2, three: 3 }
  ```

* <a name="no-mutable-keys"></a>
  変更のできるオブジェクトをハッシュのキーに使うのは避けましょう。
<sup>[[link](#no-mutable-keys)]</sup>

* <a name="hash-literals"></a>
  ハッシュのキーがシンボルの時は、Ruby 1.9のハッシュリテラル記法を用いましょう。
<sup>[[link](#hash-literals)]</sup>

  ```Ruby
  # 悪い例
  hash = { :one => 1, :two => 2, :three => 3 }

  # 良い例
  hash = { one: 1, two: 2, three: 3 }
  ```

* <a name="no-mixed-hash-syntaces"></a>
  Ruby 1.9のハッシュ記法とロケット記法を同じハッシュリテラル内で混在させてはいけません。
  シンボルでないキーがある場合は、ロケット記法を使いましょう。
<sup>[[link](#no-mixed-hash-syntaces)]</sup>

  ```Ruby
  # 悪い例
  { a: 1, 'b' => 2 }

  # 良い例
  { :a => 1, 'b' => 2 }
  ```

* <a name="hash-key"></a>
  `Hash#has_key?`より`Hash#key?`を、
  `Hash#has_value?`より`Hash#value?`を用いましょう。
    [ここ](http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-core/43765)
  でMatzが述べているように、長い記法は廃止が検討されています。
<sup>[[link](#hash-key)]</sup>

  ```Ruby
  # 悪い例
  hash.has_key?(:test)
  hash.has_value?(value)

  # 良い例
  hash.key?(:test)
  hash.value?(value)
  ```

* <a name="hash-fetch"></a>
  存在すべきキーを扱う時は、`Hash#fetch`を用いましょう。
<sup>[[link](#hash-fetch)]</sup>

  ```Ruby
  heroes = { batman: 'Bruce Wayne', superman: 'Clark Kent' }
  # 悪い例 - もし誤りがあってもすぐに気づくことができないかもしれません
  heroes[:batman] # => "Bruce Wayne"
  heroes[:supermann] # => nil

  # 良い例 - fetchはKeyErrorを投げるので、問題が明らかになります
  heroes.fetch(:supermann)
  ```

* <a name="hash-fetch-defaults"></a>
  `Hash#fetch`のデフォルト値を使い、自力でロジックを書かないようにしましょう。
<sup>[[link](#hash-fetch-defaults)]</sup>

  ```Ruby
  batman = { name: 'Bruce Wayne', is_evil: false }

  # 悪い例 - たんに||演算子を使ってしまうと偽値が入っていた時に望まない結果になります
  batman[:is_evil] || true # => true

  # 良い例 - fetchなら偽値でも正しく動きます
  batman.fetch(:is_evil, true) # => false
  ```

* <a name="use-hash-blocks"></a>
  `Hash#fetch`のデフォルト値は評価するべき式に副作用があったり実行コストが高いときはうまくいかないので、代わりにブロックを使いましょう。
<sup>[[link](#use-hash-blocks)]</sup>

  ```Ruby
  batman = { name: 'Bruce Wayne' }

  # 悪い例 - デフォルト値が使われると、先に評価してしまいます
  # だから、もし複数回呼ばれると、プログラムが遅くなります
  batman.fetch(:powers, get_batman_powers) # get_batman_powers は高コストな呼び出し

  # 良い例 - ブロックは後から評価されます。だから、KeyErrorが評価の引き金になります
  batman.fetch(:powers) { get_batman_powers }
  ```

* <a name="hash-values-at"></a>
  ハッシュから連続して複数の値が必要になる時は、`Hash#values_at`を用いましょう。
<sup>[[link](#hash-values-at)]</sup>

  ```Ruby
  # 悪い例
  email = data['email']
  username = data['nickname']

  # 良い例
  email, username = data.values_at('email', 'nickname')
  ```

* <a name="ordered-hashes"></a>
  Ruby 1.9以降、ハッシュは順序付けられるということを信頼しましょう。
<sup>[[link](#ordered-hashes)]</sup>

* <a name="no-modifying-collections"></a>
  コレクションを走査している時に変更を加えてはいけません。
<sup>[[link](#no-modifying-collections)]</sup>

* <a name="accessing-elements-directly"></a>
  コレクションにアクセスするとき、`[n]`の代替のリーダーメソッドが提供されている場合に
  直接`[n]`経由でアクセスすることは避けましょう。
  `nil`に対して`[]`を呼ぶことを避けることが出来ます。
<sup>[[link](#accessing-elements-directly)]</sup>

  ```Ruby
  # 悪い例
  Regexp.last_match[1]

  # 良い例
  Regexp.last_match(1)
  ```

* <a name="provide-alternate-accessor-to-collections"></a>
  コレクションに対するアクセサを提供するとき、
  コレクション内の要素にアクセスする前に、
  `nil`でアクセスするのを防ぐための代替のアクセス方法を提供しましょう。
<sup>[[link](#provide-alternate-accessor-to-collections)]</sup>

  ```Ruby
  # 悪い例
  def awesome_things
    @awesome_things
  end

  # 良い例
  def awesome_things(index = nil)
    if index && @awesome_things
      @awesome_things[index]
    else
      @awesome_things
    end
  end
  ```

## 文字列

* <a name="string-interpolation"></a>
  文字列連結の代わりに文字列挿入や文字列整形を好みます。
<sup>[[link](#string-interpolation)]</sup>

  ```Ruby
  # 悪い例
  email_with_name = user.name + ' <' + user.email + '>'

  # 良い例
  email_with_name = "#{user.name} <#{user.email}>"

  # 良い例
  email_with_name = format('%s <%s>', user.name, user.email)
  ```

* <a name="string-interpolation"></a>
  文字列挿入時には、括弧の内部にスペースを入れるべきではありません。
<sup>[[link](#string-interpolation)]</sup>

  ```Ruby
  # 悪い例
  "From: #{ user.first_name }, #{ user.last_name }"

  # 良い例
  "From: #{user.first_name}, #{user.last_name}"
  ```

* <a name="consistent-string-literals"></a>
  文字列リテラルの引用符は一貫したスタイルで使いましょう。
  Rubyコミュニティでは、
  デフォルトでシングルクォートを用いるもの (Option A)、
  ダブルクォートを用いるもの (Option B)
  の二つのよく使われるスタイルがあって、
  どちらも良いと考えられています。
<sup>[[link](#consistent-string-literals)]</sup>

  * **(Option A)** 文字列挿入の必要がないときや、`\t`や`\n`｀’｀等の特別な文字がない場合は、
    シングルクォーテーションが好まれます。

    ```Ruby
    # 悪い例
    name = "Bozhidar"

    # 良い例
    name = 'Bozhidar'
    ```

  * **(Option B)** 文字列中に`"`を含んでいたり、エスケープ文字を抑えたいときでない限り、
    ダブルクォーテーションが好まれます。

    ```Ruby
    # 悪い例
    name = 'Bozhidar'

    # 良い例
    name = "Bozhidar"
    ```

  このガイド内の文字列リテラル表記は、
  １つ目のスタイルを採用しています。

* <a name="no-character-literals"></a>
  文字リテラル構文`?x`を用いてはいけません。
  Ruby 1.9以降、この表記法を必要とする場面はないはずです -
  `?x`は`'x'`(１文字の文字列)と解釈されるからです。
<sup>[[link](#no-character-literals)]</sup>

  ```Ruby
  # 悪い例
  char = ?c

  # 良い例
  char = 'c'
  ```

* <a name="curlies-interpolate"></a>
  文字列の中の挿入されるインスタンス変数やグローバル変数の周りの
  `{}`は省略してはいけません。
<sup>[[link](#curlies-interpolate)]</sup>

  ```Ruby
  class Person
    attr_reader :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end

    # 悪い例 - 有効ですが不格好です
    def to_s
      "#@first_name #@last_name"
    end

    # 良い例
    def to_s
      "#{@first_name} #{@last_name}"
    end
  end

  $global = 0
  # 悪い例
  puts "$global = #$global"

  # 良い例
  puts "$global = #{$global}"
  ```

* <a name="no-to-s"></a>
  文字列に挿入するときに`Object#to_s`を使ってはいけません。
  自動的に呼び出されます。
<sup>[[link](#no-to-s)]</sup>

  ```Ruby
  # 悪い例
  message = "This is the #{result.to_s}."

  # 良い例
  message = "This is the #{result}."
  ```

* <a name="concat-strings"></a>
  大きなデータの塊を作る必要があるときは、`String#+`の使用は避けましょう。
  代わりに、`String#<<`を使いましょう。
  文字列連結は、文字列インスタンスを直接書き換えるため、
  たくさんの新しいオブジェクトを作ってしまう`String#+`よりも常に速いです。
<sup>[[link](#concat-strings)]</sup>

  ```Ruby
  # 良く、そして速い例
  html = ''
  html << '<h1>Page title</h1>'

  paragraphs.each do |paragraph|
    html << "<p>#{paragraph}</p>"
  end
  ```

* <a name="dont-abuse-gsub"></a>
利用するケースにより特化した速い代替手段がある場合、`String#gsub`は使わないようにしましょう。
<sup>[[link](#dont-abuse-gsub)]</sup>

  ```Ruby
  url = 'http://example.com'
  str = 'lisp-case-rules'

  # 悪い例
  url.gsub("http://", "https://")
  str.gsub("-", "_")

  # 良い例
  url.sub("http://", "https://")
  str.tr("-", "_")
  ```

* <a name="heredocs"></a>
  複数行のヒアドキュメントを用いるときは、
  先頭のスペースも保持してしまうということを頭に入れておかなければなりません。
  過剰なスペースを取り除くためのマージンを採用するのを実用的です。
<sup>[[link](#heredocs)]</sup>

  ```Ruby
  code = <<-END.gsub(/^\s+\|/, '')
    |def test
    |  some_method
    |  other_method
    |end
  END
  # => "def test\n  some_method\n  other_method\nend\n"
  ```

## 正規表現

> なにか問題に突き当たった時、「わかった、正規表現を使えばいいんだ」と思う人がいますね。
> その時、元の問題のほかにもう一つ問題が加わっているんです。<br>
> -- Jamie Zawinski

* <a name="no-regexp-for-plaintext"></a>
  単に文字列中から文字列を探すだけの時は、
  正規表現を使ってはいけません: `string['text']`を使いましょう。
<sup>[[link](#no-regexp-for-plaintext)]</sup>

* <a name="regexp-string-index"></a>
  文字列の添字に直接正規表現を渡すことで、文字列の構築をシンプルにできます。
<sup>[[link](#regexp-string-index)]</sup>

  ```Ruby
  match = string[/regexp/]             # マッチした内容が得られる
  first_group = string[/text(grp)/, 1] # キャプチャグループの内容が得られる
  string[/text (grp)/, 1] = 'replace'  # string => 'text replace'
  ```

* <a name="non-capturing-regexp"></a>
  キャプチャした結果を使う必要のないときは、キャプチャしないグループを用いましょう。
<sup>[[link](#non-capturing-regexp)]</sup>

  ```Ruby
  /(first|second)/   # 悪い例
  /(?:first|second)/ # 良い例
  ```

* <a name="no-perl-regexp-last-matchers"></a>
  最後に正規表現にマッチした値を示すPerlレガシーの暗号的な変数を用いてはいけません
  (`$1`、`$2`など)。
  代わりに`Regexp.last_match(n)`を用いましょう。
<sup>[[link](#no-perl-regexp-last-matchers)]</sup>

  ```Ruby
  /(regexp)/ =~ string
  ...

  # 悪い例
  process $1

  # 良い例
  process Regexp.last_match(1)
  ```


* <a name="no-numbered-regexes"></a>
  どの値が入っているか追うのが困難になるので、
  グループ番号を使うのは避けましょう。
  代わりにグループに名前をつけましょう。
<sup>[[link](#no-numbered-regexes)]</sup>

  ```Ruby
  # 悪い例
  /(regexp)/ =~ string
  ...
  process Regexp.last_match(1)

  # 良い例
  /(?<meaningful_var>regexp)/ =~ string
  ...
  process meaningful_var
  ```

* <a name="limit-escapes"></a>
  文字クラスの中では、特別な意味を持つ文字が少ないので注意が必要です:
  `^`、`-`、`\`、`]`のみが特別な意味を持つので、
  `.`や括弧を`[]`の中でエスケープしてはいけません。
<sup>[[link](#limit-escapes)]</sup>

* <a name="caret-and-dollar-regexp"></a>
  `^`や`$`は、文字列の先頭や末尾ではなく、
  行頭や行末にマッチするので注意が必要です。
  もし文字列全体の先頭末尾にマッチさせたいときは、
  `\A`、`\z`を使いましょう
  (`\n?\z`と等価である`\Z`と混同しないようにしましょう)。
<sup>[[link](#caret-and-dollar-regexp)]</sup>

  ```Ruby
  string = "some injection\nusername"
  string[/^username$/]   # matches
  string[/\Ausername\z/] # don't match
  ```

* <a name="comment-regexes"></a>
  複雑な正規表現には`x`識別子を用いましょう。
  これを用いることで、より読みやすくなり、
  便利なコメントを使えるようになります。
  スペースが無視されることに注意しましょう。
<sup>[[link](#comment-regexes)]</sup>

  ```Ruby
  regexp = /
    start         # some text
    \s            # white space char
    (group)       # first group
    (?:alt1|alt2) # some alternation
    end
  /x
  ```

* <a name="gsub-blocks"></a>
  `sub`/`gsub`での複雑な置換は、ブロックやハッシュを用いることで実現できます。
<sup>[[link](#gsub-blocks)]</sup>

## パーセントリテラル

* <a name="percent-q-shorthand"></a>
  挿入と`"`双方が入る１行の文字列には、
  `%()`(`%Q()`の短縮形)を使いましょう。
  複数行の時はヒアドキュメントを好みます。
<sup>[[link](#percent-q-shorthand)]</sup>

  ```Ruby
  # 悪い例 (挿入の必要がありません)
  %(<div class="text">Some text</div>)
  # '<div class="text">Some text</div>' であるべき

  # 悪い例 (ダブルクォートがありません)
  %(This is #{quality} style)
  # "This is #{quality} style" であるべき

  # 悪い例 (複数行です)
  %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
  # ヒアドキュメントであるべき

  # 良い例 (挿入が必要、ダブルクォートがある、そして１行です)
  %(<tr><td class="name">#{name}</td>)
  ```

* <a name="percent-q"></a>
  文字列に`'`と`"`双方が含まれない限り、
  `%q`の使用は避けましょう。
  通常の文字列リテラルのほうがより読みやすいので、
  エスケープが大量に必要出ない限りは、そちらを使いましょう。
<sup>[[link](#percent-q)]</sup>

  ```Ruby
  # 悪い例
  name = %q(Bruce Wayne)
  time = %q(8 o'clock)
  question = %q("What did you say?")

  # 良い例
  name = 'Bruce Wayne'
  time = "8 o'clock"
  question = '"What did you say?"'
  ```

* <a name="percent-r"></a>
  '/'が１つ *以上の* 正規表現に限り、`%r`を使いましょう。
<sup>[[link](#percent-r)]</sup>

  ```Ruby
  # 悪い例
  %r{\s+}

  # 良い例
  %r{^/(.*)$}
  %r{^/blog/2011/(.*)$}
  ```

* <a name="percent-x"></a>
  呼び出すコマンドにバッククォートが含まれる(かなり起こりえないが)ことがない限り、
  `%x`の使用は避けましょう。
<sup>[[link](#percent-x)]</sup>

  ```Ruby
  # 悪い例
  date = %x(date)

  # 良い例
  date = `date`
  echo = %x(echo `date`)
  ```

* <a name="percent-s"></a>
  `%s`の使用は避けましょう。
  Rubyコミュニティは、スペース含むシンボルをを作る時は
  `:"文字列"`がよいと決めたようです。
<sup>[[link](#percent-s)]</sup>

* <a name="percent-literal-braces"></a>
  パーセントリテラルの区切り文字は、`%r`を除いて`()`が好まれます。
  正規表現の中では、`()`は色々なシーンで使われるので、
  正規表現の内容によっては、より使われる機会の少ない`{`のほうが
  良い選択となることがあるかもしれません。
<sup>[[link](#percent-literal-braces)]</sup>

  ```Ruby
  # 悪い例
  %w[one two three]
  %q{"Test's king!", John said.}

  # 良い例
  %w(one two three)
  %q("Test's king!", John said.)
  ```

## メタプログラミング

* <a name="no-needless-metaprogramming"></a>
  不要なメタプログラミングは避けましょう。
<sup>[[link](#no-needless-metaprogramming)]</sup>

* <a name="no-monkey-patching"></a>
  ライブラリを作成する時にコアクラスを汚染するのはやめましょう。
  (モンキーパッチを当ててはいけません)。
<sup>[[link](#no-monkey-patching)]</sup>

* <a name="block-class-eval"></a>
  ブロック渡しの`class_eval`のほうが、文字列挿入型よりも好ましいです。
  - 文字列挿入型を使う時は、バックトレースが働くように、常に`__FILE__`と`__LINE__`を渡しましょう:
<sup>[[link](#block-class-eval)]</sup>

  ```ruby
  class_eval 'def use_relative_model_naming?; true; end', __FILE__, __LINE__
  ```

  - `define_method`の方が、`class_eval{ def ... }`よりも好まれます。

* <a name="eval-comment-docs"></a>
  文字列挿入型の`class_eval`(または他の`eval`)を用いる時は、
  挿入されたときのコードをコメントに追加しましょう(Railsでは活用されています)。
<sup>[[link](#eval-comment-docs)]</sup>

  ```ruby
  # from activesupport/lib/active_support/core_ext/string/output_safety.rb
  UNSAFE_STRING_METHODS.each do |unsafe_method|
    if 'String'.respond_to?(unsafe_method)
      class_eval <<-EOT, __FILE__, __LINE__ + 1
        def #{unsafe_method}(*params, &block)       # def capitalize(*params, &block)
          to_str.#{unsafe_method}(*params, &block)  #   to_str.capitalize(*params, &block)
        end                                       # end

        def #{unsafe_method}!(*params)              # def capitalize!(*params)
          @dirty = true                           #   @dirty = true
          super                                   #   super
        end                                       # end
      EOT
    end
  end
  ```

* <a name="no-method-missing"></a>
  `method_missing`を用いたメタプログラミングは避けましょう。
  何故なら、バックトレースが面倒になり、
  `#methods`のリストの中に出てこず、
  ミススペルしたメソッド呼び出しも無言で動いてしまいます、
  例えば`nukes.launch_state = false`のようにです。
  代わりに、移譲、プロキシ、または`define_method`を使いましょう。
  もし`method_missing`を使わなければならない時は:
<sup>[[link](#no-method-missing)]</sup>

  - [`respond_to_missing?`](http://blog.marc-andre.ca/2010/11/methodmissing-politely.html)も実装されているか確かめましょう
  - 既知の接頭辞、`find_by_*`のようなものを捕捉しましょう -- 可能な限りアサートさせましょう
  - 最後に`super`を呼び出しましょう
  - アサートする、特別でないメソッドに移譲しましょう:

  ```ruby
  # 悪い例
  def method_missing?(meth, *params, &block)
    if /^find_by_(?<prop>.*)/ =~ meth
      # ... lots of code to do a find_by
    else
      super
    end
  end

  # 良い例
  def method_missing?(meth, *args, &block)
    if /^find_by_(?<prop>.*)/ =~ meth
      find_by(prop, *args, &block)
    else
      super
    end
  end

  # それでも最も良い選択は、発見できる全てのアトリビュートにdefine_methodすることです
  ```

* <a name="prefer-public-send"></a>
  `private`/`protected`制約を避けないように、`send`よりも`public_send`を好みます。
<sup>[[link](#prefer-public-send)]</sup>

## 雑則

* <a name="always-warn"></a>
  `ruby -w`で安全なコードを書きましょう。
<sup>[[link](#always-warn)]</sup>

* <a name="no-optional-hash-params"></a>
  オプショナルな変数としてのハッシュの使用を避けましょう。やりすぎてはいませんか？(オブジェクトの初期化はこのルールの例外です)
<sup>[[link](#no-optional-hash-params)]</sup>

* <a name="short-methods"></a>
  コードのある行が10行を超えるメソッドは避けましょう。
  理想を言えば、多くのメソッドは5行以内がよいです。
  空行は行数には含めません。
<sup>[[link](#short-methods)]</sup>

* <a name="too-many-params"></a>
  ３つや４つ以上引数を設定するのは避けましょう。
<sup>[[link](#too-many-params)]</sup>

* <a name="private-global-methods"></a>
  もし本当に"global"なメソッドが必要な場合は、
  Kernelに定義し、privateに設定しましょう。
<sup>[[link](#private-global-methods)]</sup>

* <a name="instance-vars"></a>
  グローバル変数の代わりに、モジュールのインスタンス変数を使用しましょう。
<sup>[[link](#instance-vars)]</sup>

  ```Ruby
  # 悪い例
  $foo_bar = 1

  # 良い例
  module Foo
    class << self
      attr_accessor :bar
    end
  end

  Foo.bar = 1
  ```

* <a name="optionparser"></a>
  複雑なコマンドラインオプションをパースするために`OptionParser`を使いましょう。
  また、些細なオプションには`ruby -s`を使いましょう。
<sup>[[link](#optionparser)]</sup>

* <a name="time-now"></a>
  現在のシステム時間を読み出すには、`Time.new`よりも`Time.now`を使いましょう。
<sup>[[link](#time-now)]</sup>

* <a name="functional-code"></a>
  それで問題ない時は、破壊的処理を避け関数型の手法でコードを書きましょう。
<sup>[[link](#functional-code)]</sup>

* <a name="no-param-mutations"></a>
  それがメソッドの目的でない限り、引数に破壊的変更をするのはやめましょう。
<sup>[[link](#no-param-mutations)]</sup>

* <a name="three-is-the-number-thou-shalt-count"></a>
  ３段階を超えるネストは避けましょう。
<sup>[[link](#three-is-the-number-thou-shalt-count)]</sup>

* <a name="be-consistent"></a>
  一貫性を保ちましょう。理想を言えば、このガイドラインに沿いましょう。
<sup>[[link](#be-consistent)]</sup>

* <a name="common-sense"></a>
  常識を用いましょう。
<sup>[[link](#common-sense)]</sup>

## ツール

ここでは、このガイドに反するコードを自動的にチェックするのを支援するツールをいくつか紹介します。

### RuboCop

[RuboCop][]は、このガイドに基づいた
Rubyコードスタイルチェッカーです。
Rubocopはすでにこのガイドの重要な部分をカバーしており、
MRI 1.9、MRI 2.0 双方をサポートし、Emacs向けのよいプラグインがあります。

### RubyMine

[RubyMine](http://www.jetbrains.com/ruby/) のコードインスペクションは、このガイドに
[部分的に基づいています](http://confluence.jetbrains.com/display/RUBYDEV/RubyMine+Inspections)。

# Contributing

このガイドはまだ未完成です - いくつかのルールはサンプルがなく、 いくつかのルールは説明が不十分です。
そのようなルールの改善はRubyコミュニティを助ける素晴らしい(そしてシンプルな)手段です!

やがてこれらの課題は対応されます - 今後これらを記憶にとどめておきます。

このガイドに書いてあることには変更不能なものはありません。
Rubyのコードスタイルに興味のある全ての人と共に取り組むことが私の望みなので、
究極的には、全てのRubyコミュニティにとって有益なリソースを作ることができればと思っています。

改善のために、遠慮せずチケットを立てたりプルリクエストを送ったりしてください。
あなたの手助けに予め感謝します！

また、このプロジェクト(とRubocop)への金銭的な貢献は、
[gittip](https://www.gittip.com/bbatsov)経由で行うことができます。

[![Gittip経由での支援](https://rawgithub.com/twolfson/gittip-badge/0.2.0/dist/gittip.png)](https://www.gittip.com/bbatsov)

## 貢献するには

簡単です！ [contribution guidelines](https://github.com/bbatsov/ruby-style-guide/blob/master/CONTRIBUTING.md)を読んでください！

# ライセンス

![Creative Commons License](http://i.creativecommons.org/l/by/3.0/88x31.png)
この著作物は、[Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/deed.en_US)
に従います。

# 広めましょう

コミュニティ駆動のスタイルガイドは、これを知らないコミュニティにはほとんど役に立ちません。
このガイドについてつぶやいたり、友達や同僚にシェアしてください。
全てのコメント、提案、オプションがこのガイドを少しだけでも良くしていきます。
そして、考えうるベストのガイドが欲しいですよね？

ありがとう<br>
[Bozhidar](https://twitter.com/bbatsov)

[PEP-8]: http://www.python.org/dev/peps/pep-0008/
[rails-style-guide]: https://github.com/bbatsov/rails-style-guide
[pickaxe]: http://pragprog.com/book/ruby4/programming-ruby-1-9-2-0
[trpl]: http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177
[transmuter]: https://github.com/TechnoGate/transmuter
[RuboCop]: https://github.com/bbatsov/rubocop
