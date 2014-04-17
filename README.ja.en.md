# Introduction

> Role model's important. <br/>
> - Alex Murphy constable / RoboCop

As a Ruby developer, and has been plagued by that there is always I -
Python developers a great programming style guide
([PEP-8] (http://www.python.org/dev/peps/pep-0008/))
Although you have,
Best practices and coding style of the official to us
I do not possess any.
And, I'm sure what it is the problem.
In addition, great hacker community Ruby is like having the,
I'm sure also should have the power to create a document that everyone envy.

This guide was born from in-house-made Ruby coding guide our
([I] author (https://github.com/bbatsov)).
When you have decided I would write this guide, a member of the Ruby community at large
Will be interesting, guide the company made or not than not require much
I was thinking with.
However, I was recognized in the community drive, the community,
Convention for Ruby, diction, style provisions,
And I think in obtaining or beneficial to the Ruby community surely.

Beginning this guide, I will from members of the Ruby community with excellent all over the world,
I have received a lot of feedback.
All proposals, I appreciate your support!
Valuable resource for all of Ruby developers also, to each other,
It can be made together.

By the way, if you are like the Rails if,
Please check also supplement here.
[Ruby on Rails 3 & 4 Style Guide] (https://github.com/bbatsov/rails-style-guide).

# The Ruby Style Guide

This Ruby style guide is, for writing code serviceable Ruby other programmers
It is recommended that you adopt the best practices.
Style guide that reflects how it is actually used came to be used,
As is rejected by people who feel that remains ideal theory, is employed it is a risk
Style guide &nbdash; that it is no longer used at all
It is to be understood that no matter how great.

This guide is divided into several sections on the basis of rules that are related.
It will make every effort to add also the rationale behind the rule
(Other than those determined to be self-evident).

It does not mean that come up out of nowhere all the rules these I -
Most of these, as a professional software engineer my
And a wealth of experience, comments and suggestions from members of the Ruby community,
In addition, ["Programming Ruby 1.9"] and (http://pragprog.com/book/ruby4/programming-ruby-1-9-2-0),
["The Ruby Programming Language"] such as (http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177),
It is based on the Ruby programming resources acclaimed at various altitudes.

There is no sample some rules, - is still unfinished this guide
Explanation There is insufficient some rules.
I leave remembered these future - these issues will be addressed in due course.

You can create by using this guide is a copy of the HTML or PDF
[Transmuter] (https://github.com/TechnoGate/transmuter).

[RuboCop] (https://github.com/bbatsov/rubocop) is,
It is a code analyzer based on this style guide.

The translation of the following languages ​​are available:

* [Chinese (Simplified)] (https://github.com/JuanitoFatas/ruby-style-guide/blob/master/README-zhCN.md)
* [Chinese (Traditional)] (https://github.com/JuanitoFatas/ruby-style-guide/blob/master/README-zhTW.md)
* [French] (https://github.com/porecreat/ruby-style-guide/blob/master/README-frFR.md)
* [Spanish] (https://github.com/alemohamad/ruby-style-guide/blob/master/README-esLA.md)
* [Vietnamese] (https://github.com/scrum2b/ruby-style-guide/blob/master/README-viVN.md)

# # Table of Contents

* Layout (# Layout)
* [Syntax] (# syntax)
* [File Naming Rule] (# naming convention)
* [Comments] (# comments)
    * [Note] (# comments)
* [Class] (# class)
* [Exception] (# exceptions)
* [Collections] (# collections)
* [String] (# string)
* Regular expression (# regular expression)
* Percent literal] (# literal percent)
* [Meta-programming] (# meta-programming)
* [Miscellaneous Provisions] (# Miscellaneous Provisions)
* Tools (# tool)

# # Layout

> Style all people, not themselves the most
> I'm sure that it is not a reasonable uncomfortable.
> With the exception of "their own", although he probably right,,,
> - Jerry Coffin (on indentation)

* Let's using `UTF-8` The encoding of the source file.
* The indent two spaces ** ** (also known as soft tab). You should not be using the (hard) tab.

    `` `Ruby
    # Bad example - four spaces
    def some_method
        do_something
    end

    # A good example
    def some_method
      do_something
    end
    `` `

* We will continue with our new line of Unix-style.
(* BSD / Solaris / Linux / OS X user is set by default.
  Windows users need special attention. )
    * And if you are using Git, then the new line of Windows to prevent funneled to the project, it is preferable to add the following might be good:

    `` `Bash
    $ Git config - global core.autocrlf true
    `` `

* `To separate the expression or statement; You should not be using the`.
  Of course, try to Tsunishi one type per line.

    `` `Ruby
    # Bad example
    A semicolon extra #; puts 'foobar'.

    There is one line expressions of one puts 'bar' # 2; puts 'foo'.

    # A good example
    puts 'foobar'

    puts 'foo'
    puts 'bar'

    It applies in particular puts puts 'foo', 'bar' #.
    `` `

* The format of a line is to be preferred class with no body.

    `` `Ruby
    # Bad example
    class FooError <StandardError
    end

    # Example not bad
    class FooError <StandardError; end

    # A good example
    FooError = Class.new (StandardError)
    `` `

* Method of a line Avoid.
  There are some places that have been used some,
  There are peculiarities of some to be defined specification of their syntax is undesirable.
  I should be the one to equation (1) at most one line method - at any rate.

    `` `Ruby
    # Bad example
    def too_much; something; something_else; end

    # Example not bad - first; it is required.
    def no_braces_method; body end

    # Example not bad - the second; is optional.
    def no_braces_method; body; end

    # Example it is not bad - it is correct grammar. However,; I am a little hard to read there is no description.
    def some_method () body end

    # A good example
    def some_method
      body
    end
    `` `

    Empty method is an exception to this rule text.

    `` `Ruby
    # Good
    def no_op; end
    `` `

* Before and after the operator, after a comma, colon, semicolon, before and after the {`,`} `Let's put a space before the`.
  (In most cases) space is not as important to the interpreter of Ruby,
  Proper use of space is the key for writing easily readable code.

    `` `Ruby
    sum = 1 + 2
    a, b = 1, 2
    ? 1> 2 true: false; puts 'Hi'
    . [1, 2, 3] each {| e | puts e}
    `` `

    For operators only exception is the exponentiation operator:

    `` `Ruby
    # Bad example
    e = M * c ** 2

    # A good example
    e = M * c ** 2
    `` `

    `The` {`and`}, it is useful for the sake of clarity of syntax.
    So, as if to fill the floor to a string,
    It is used to hash and syntax block.
    The hash syntax, style of the two is acceptable.

    `` `Ruby
    # A good example - I put in front of the {and} after the space
    {One: 1, two: 2}

    # A good example - it is not put in front of the {and} after the space
    {One: 1, two: 2}
    `` `

    The syntax of the first (and is popular in the Ruby community general arguably) it is easy to read a little slight.
    Second syntax is advantageous in that they can be differentiated visually and hash block.
    By adopting the one either, let's use the same syntax always.

    Syntax to be embedded in the string can also be acceptable in two styles:

    `` `Ruby
    # Good example - with no spaces
    "String # {expr}"

    # Good example - better here is easy to read in almost certainly
    "String # {expr}"
    `` `

    There is a very popular than other formulas, equations The first is writing which proceeds to use here in general.
    On the other hand, the second, (no doubt) I am a little easy to read.
    As with hash - By adopting the one, let's adopt the same person at all times.

* `There is no space ([and after the`, `]` ``, `,) in front of the`.

    `` `Ruby
    some (arg). other
    [1, 2, 3]. Size
    `` `

* `!` There is no space after the.

    `` `Ruby
    # Bad example
    ! Something

    # A good example
    ! Something
    `` `

* `Let's aligned to the same depth as the` case `is when`.
  Although I know many people from not agree,
  This "The Ruby Programming Language", "Programming Ruby" style
  It is something that has been established in both.

    `` `Ruby
    # Bad example
    case
      when song.name == 'Misty'
        puts 'Not again!'
      when song.duration> 120
        puts 'Too long!'
      when Time.now.hour> 21
        puts "It's too late"
      else
        song.play
    end

    # A good example
    case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration> 120
      puts 'Too long!'
    when Time.now.hour> 21
      puts "It's too late"
    else
      song.play
    end
    `` `

* When you assigned to a variable conditional expression,
  Let's maintain the alignment of its normal expression.

    `` `Ruby
    # Bad example - is very complex
    kind = case year
    when 1850 .. 1889 then 'Blues'
    when 1890 .. 1909 then 'Ragtime'
    when 1910 .. 1929 then 'New Orleans Jazz'
    when 1930 .. 1939 then 'Swing'
    when 1940 .. 1950 then 'Bebop'
    else 'Jazz'
    end

    result = if some_cond
      calc_something
    else
      calc_something_else
    end

    # A good example - it is clear what has been done
    kind = case year
           when 1850 .. 1889 then 'Blues'
           when 1890 .. 1909 then 'Ragtime'
           when 1910 .. 1929 then 'New Orleans Jazz'
           when 1930 .. 1939 then 'Swing'
           when 1940 .. 1950 then 'Bebop'
           else 'Jazz'
           end

    result = if some_cond
               calc_something
             else
               calc_something_else
             end

    # (Width of efficiency is good only a little) a good example
    kind =
      case year
      when 1850 .. 1889 then 'Blues'
      when 1890 .. 1909 then 'Ragtime'
      when 1910 .. 1929 then 'New Orleans Jazz'
      when 1930 .. 1939 then 'Swing'
      when 1940 .. 1950 then 'Bebop'
      else 'Jazz'
      end

    result =
      if some_cond
        calc_something
      else
        calc_something_else
      end
    `` `

* Put a blank line between the definition formula,
  Let's divided into logical paragraphs in the method.

    `` `Ruby
    def some_method
      data = initialize (options)

      data.manipulate!

      data.result
    end

    def some_method
      result
    end
    `` `

* Comma after the last argument of the method invocation Avoid.
  When the arguments are not divided into multiple lines, Avoid in particular.

    `` `Ruby
    # Bad example - you can move, add, delete the argument easily, but it is still not recommended.
    some_method (
                 size,
                 count,
                 color,
               )

    # Bad example
    some_method (size, count, color,)

    # A good example
    some_method (size, count, color)
    `` `

* When you assign an initial value to the argument of the method,
  `=` Let's put a space around the operator.

    `` `Ruby
    # Bad example
    def some_method (arg1 =: default, arg2 = nil, arg3 = [])
      # Do something ...
    end

    # A good example
    def some_method (arg1 =: default, arg2 = nil, arg3 = [])
      # Do something ...
    end
    `` `

    Ruby books, but some have proposed the style of the first,
    Person of the second will have better practical
    (And it is easy to read a little arguably).

* Avoid the line continuation using unnecessary `\`.
  In fact, let's avoid the continuation of the line in the string concatenation other than.

    `` `Ruby
    # Bad example
    result = 1 - \
             Two

    # (But still ugly as hell) a good example
    result = 1 \
             - 2

    long_string = 'First part of the long string' \
                  'And second part of the long string'
    `` `

* When you connect to other lines the chain method, let's put on the next line `.`.

    `` `Ruby
    # Bad example - you must examine the first line to understand the second line
    one.two.three.
      four

    # A good example - I can understand immediately what is going on in the second line
    one.two.three
      . Four
    `` `

* When a method call spans multiple lines, the argument let's aligned.
  When for the constraint length of a line, it is not suitable to align the argument,
  I can tolerate the style to align in one minute indent after the first argument.

    `` `Ruby
    # (One line is very long) initial value
    def send_mail (source)
      Mailer.deliver (to: 'bob@example.com', from: 'us@example.com', subject: 'Important message', body: source.text)
    end

    # (I prepare it in one indentation 2) Bad Example
    def send_mail (source)
      Mailer.deliver (
          to: 'bob@example.com',
          from: 'us@example.com',
          subject: 'Important message',
          body: source.text)
    end

    # A good example
    def send_mail (source)
      Mailer.deliver (to: 'bob@example.com',
                     from: 'us@example.com',
                     subject: 'Important message',
                     body: source.text)
    end

    # (Which is indentation of normal) a good example
    def send_mail (source)
      Mailer.deliver (
        to: 'bob@example.com',
        from: 'us@example.com',
        subject: 'Important message',
        body: source.text
      )
    end
    `` `

* Array that spans more than one line, let's align the elements.

    `` `Ruby
    # Bad example - is another indent 1
    menu_item = ["Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
      "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"]

    # A good example
    menu_item = [
      "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
      "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"
    ]

    # A good example
    menu_item =
      ["Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
       "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"]
    `` `

* For readability, let's put the underscore in large numbers.

    `` `Ruby
    # Bad example - How many 0?
    num = 1000000

    # A good example - I can be analyzed more easily in a person's head
    num = 1_000_000
    `` `

* For documents of API, let's follow the terms of the RDoc.
  It should not be a blank line between the comment lines of `def`.
* Let's up to 80 characters in one line.
* Avoid the space at the end of the line.
* Block comments should not be used.
  And to not work space to go into before,
  Unlike regular comments, indistinguishable easily.

    `` `Ruby
    # Bad example
    == Begin
    comment line
    another comment line
    == End

    # A good example
    # Comment line
    # Another comment line
    `` `

# # Syntax

* `::` Is, and Ya (also includes classes and modules) constant
  Let's use only when you see (or () `` Nokogiri :: HTML () `` Array, for example) constructor.
  Avoid the use of `::` In a normal method call.

    `` `Ruby
    # Bad example
    SomeClass :: some_method
    some_object :: some_method

    # A good example
    SomeClass.some_method
    some_object.some_method
    SomeModule :: SomeClass :: SOME_CONST
    SomeModule :: SomeClass ()
    `` `

* If any of the arguments, let's use along with the `()` is `def`.
  Let's except for `()` If there is no argument.

     `` `Ruby
     # Bad example
     def some_method ()
       # Body omitted
     end

     # A good example
     def some_method
       # Body omitted
     end

     # Bad example
     def some_method_with_arguments arg1, arg2
       # Body omitted
     end

     # A good example
     def some_method_with_arguments (arg1, arg2)
       # Body omitted
     end
     `` `

* If you do not know exactly why you should not be used, and do not use the `for` never.
  Iterator should be used instead.
  `(So, you who I use in detour) is it is implemented in terms of the` each `for`,
  `(Unlike` each `) for` does not introduce a new scope,
  Variables defined within the block will become visible from the outside of the block.

    `` `Ruby
    arr = [1, 2, 3]

    # Bad example
    for elem in arr do
      puts elem
    end

    # It is important to note that that can be referenced from outside the Lube elem
    elem # => 3

    # A good example
    arr.each {| elem | puts elem}

    # Will be unable to see the outside of each block elem
    elem # => NameError: undefined local variable or method `elem '
    `` `

* The `Do not use it in the` if / unless `span multiple lines then`.

    `` `Ruby
    # Bad example
    if some_condition then
      # Body omitted
    end

    # A good example
    if some_condition
      # Body omitted
    end
    `` `

* In the `if / unless` multi-line, let's put on the same line as the `if / unless` always conditional expression.

    `` `Ruby
    # Bad example
    if
      some_condition
      do_something
      do_something_else
    end

    # A good example
    if some_condition
      do_something
      do_something_else
    end
    `` `

* `Ternary operator than if / then / else / end` syntax: I prefer the (`?)
  It is the simplicity of those there is a clearer.

    `` `Ruby
    # Bad example
    result = if some_condition then something else something_else end

    # A good example
    ? result = some_condition something: something_else
    `` `

* Ternary operator Let's make up one for one formula.
  In other words, the ternary operator should not be nested.
  Person of `if / else` is good in this case.

    `` `Ruby
    # Bad example
    ? some_condition (? nested_condition nested_something: nested_something_else): something_else

    # A good example
    if some_condition
      ? nested_condition nested_something: nested_something_else
    else
      something_else
    end
    `` `

* `If x: ...` It must not be used - is deprecated Ruby 1.9 now.
  Let's use the ternary operator instead.

    `` `Ruby
    # Bad example
    result = if some_condition: something else something_else end

    # A good example
    ? result = some_condition something: something_else
    `` `

* `If x; You should not be using the ...`. Let's use the ternary operator instead.

* Let's use the `when x then ...` of one line in the `case` statement.
  Is a representation of an alternative `when x: ...` is now obsolete in Ruby 1.9.

* `When x; You should not be using the ...`. Please look at the rules of the previous.

* `Let's use the`! Instead of `not`.

    `` `Ruby
    # Bad example - for evaluation order, () is required
    x = (not something)

    # A good example
    x =! something
    `` `

* `!` Let's avoid.

    `` `Ruby
    # Bad example
    x = 'test'
    # Obscure nil check
    if!! x
      # Body omitted
    end

    x = false
    # Double negative does not help as boolean.
    !! X # => false

    # A good example
    x = 'test'
    unless x.nil?
      # Body omitted
    end
    `` `

* The use of `` or `is prohibited and and`. There is no worth to them.
   Always, `and` `&& instead | Let's use the` |.

    `` `Ruby
    # Bad example
    # Boolean expression
    if some_condition and some_other_condition
      do_something
    end

    # Syntax control
    document.saved? or document.save!

    # Good
    # Boolean expression
    if some_condition && some_other_condition
      do_something
    end

    # Syntax control
    document.saved |? | document.save!
    `` `

* Ternary operator `run to multiple lines: Avoid`; Let's use the `if / unless` instead?

* I will be preferred when one line, `if / unless` is to guard the clause body.
  There is a control syntax that uses a `| |` && / An alternative other good.

    `` `Ruby
    # Bad example
    if some_condition
      do_something
    end

    # A good example
    do_something if some_condition

    # Good example of another
    some_condition && do_something
    `` `

* `Unless` is preferred more `if` When the negative form. (| Let's use the syntax `|` or).

    `` `Ruby
    # Bad example
    do_something if! some_condition

    # Bad example
    do_something if not some_condition

    # A good example
    do_something unless some_condition

    # Good example of another
    some_condition | | do_something
    `` `

* `It should not be used in the` else `with the unless`.
  You'll want to change in the previously positive conditions.

    `` `Ruby
    # Bad example
    unless success?
      puts 'failure'
    else
      puts 'success'
    end

    # A good example
    if success?
      puts 'success'
    else
      puts 'failure'
    end
    `` `

* `Let's avoid the use of` () `in the if / unless / while / until` syntax.

    `` `Ruby
    # Bad example
    if (x> 10)
      # Body omitted
    end

    # A good example
    if x> 10
      # Body omitted
    end
    `` `

* Do not in `while / until`, and using the `while / until condition do` more than one line.

    `` `Ruby
    # Bad example
    while x> 5 do
      # Body omitted
    end

    until x> 5 do
      # Body omitted
    end

    # A good example
    while x> 5
      # Body omitted
    end

    until x> 5
      # Body omitted
    end
    `` `

* If a single line, `while / until` Try to guard clause body.

    `` `Ruby
    # Bad example
    while some_condition
      do_something
    end

    # A good example
    do_something while some_condition
    `` `

* When the negative form, towards the `until` is preferred than the `while`.

    `` `Ruby
    # Bad example
    do_something while! some_condition

    # A good example
    do_something until some_condition
    `` `

* In the case of post-decision loop, and `begin / end / until` from `begin / end / while`, the `break` with `Kernel # loop` is preferred.

   `` `Ruby
   # Bad example
   begin
     puts val
     val + = 1
   end while val <0

   # A good example
   loop do
     puts val
     val + = 1
     break unless val <0
   end
   `` `

* (Rake, Rails, and RSpec for example) internal DSL,
  Method with the status becomes "keyword" in Ruby within (or `attr_reader` such as `puts`) Ya
  Methods that access the attribute,
  Let omitted around the argument `()`.
  In all other methods, let's add a `()` at the time of the method call.

    `` `Ruby
    class Person
      attr_reader: name,: age

      # Omitted
    end

    temperance = Person.new ('Temperance', 30)
    temperance.name

    puts temperance.age

    x = Math.sin (y)
    array.delete (e)

    bowling.score.should == 0
    `` `

* Let omitted outside the options hash of implicit `{}`.

    `` `Ruby
    # Bad example
    user.set ({name: 'John', age: 45, permissions: {read: true}})

    # A good example
    user.set (name: 'John', age: 45, permissions: {read: true})
    `` `

* The argument of the method to be used as part of an internal DSL, let's skip `{}` () `,` outer

    `` `Ruby
    class Person <ActiveRecord :: Base
      # Bad example
      validates (: name, {presence: true, length: {within: 1 .. 10}})

      # A good example
      validates: name, presence: true, length: {within: 1 .. 10}
    end
    `` `

* Let's omission of the method call with no arguments `()`.

    `` `Ruby
    # Bad example
    Kernel.exit! ()
    2.even? ()
    fork ()
    'Test'. Upcase ()

    # A good example
    Kernel.exit!
    2.even?
    fork
    'Test'. Upcase
    `` `

* If the `{...}` is preferred more `do ... end` a block of one line.
  Avoid the `{...}` block in multiline
  (Method chain of more than one line is always ugly).
  Let's use the `do ... end` always or "control structures" in "method definition"
  (Such as DSL or a specific Rakefiles for example)
  Avoid in the method chain `do ... end`.

    `` `Ruby
    names = ['Bozhidar', 'Steve', 'Sarah']

    # Bad example
    names.each do | name |
      puts name
    end

    # A good example
    names.each {| name | puts name}

    # Bad example
    names.select do | name |
      name.start_with? ('S')
    end.map {| name | name.upcase}

    # A good example
    names.select. {| name |? name.start_with ('S')} map {| name | name.upcase}
    `` `

    `But Some people may argue that OK method chaining of multiple lines using the {...}`,
    I want you to ask yourself - Will it be really easy to read this code?
    In addition, the body of this block, or will be able to rapidly deploy?

* In order to avoid a literal block of only passing arguments to block other simply,
  Let's consider that you explicitly block argument.
  However, be careful to performance in that block is converted to `Proc`.

    `` `Ruby
    require 'tempfile'

    # Bad example
    def with_tmp_dir
      Dir.mktmpdir do | tmp_dir |
        Dir.chdir (tmp_dir) {| dir | yield dir} # block just passes arguments
      end
    end

    # A good example
    def with_tmp_dir (& block)
      Dir.mktmpdir do | tmp_dir |
        Dir.chdir (tmp_dir, & block)
      end
    end

    with_tmp_dir do | dir |
      puts "dir is accessible as parameter and pwd is set: # {dir}"
    end
    `` `

* Avoid unnecessary `return` syntax on control.

    `` `Ruby
    # Bad example
    def some_method (some_arr)
      return some_arr.size
    end

    # A good example
    def some_method (some_arr)
      some_arr.size
    end
    `` `

* (Required only in writing to the attribute of itself) unnecessary `self` Avoid.

    `` `Ruby
    # Bad example
    def ready?
      if self.last_reviewed_at> self.last_updated_at
        self.worker.update (self.content, self.options)
        self.status =: in_progress
      end
      self.status ==: verified
    end

    # A good example
    def ready?
      if last_reviewed_at> last_updated_at
        worker.update (content, options)
        self.status =: in_progress
      end
      status ==: verified
    end
    `` `

* Naturally, you hide the method in local variable,
  Avoid as long as they are not equivalent.

    `` `Ruby
    class Foo
      attr_accessor: options

      # Ok
      def initialize (options)
        self.options = options
        # Both options and self.options are equivalent here
      end

      # Bad example
      def do_something (options = {})
        unless options [: when] ==: later
          output (self.options [: message])
        end
      end

      # A good example
      def do_something (params = {})
        unless params [: when] ==: later
          output (options [: message])
        end
      end
    end
    `` `

* Do not unquoted `()` the assignment part, it is used in the conditional expression return value of `=`.
  This is very famous as a safe assignment * in * conditional expression is in Rubyist.

    `` `Ruby
    # (+ Warning is issued) bad example
    if v = array.grep (/ foo /)
      do_something (v)
      ...
    end

    # Good example (MRI complains even this, but this is not a problem in RuboCop)
    if (v = array.grep (/ foo /))
      do_something (v)
      ...
    end

    # A good example
    v = array.grep (/ foo /)
    if v
      do_something (v)
      ...
    end
    `` `

* The initialization of variables, `| Let's use freely =` |.

    `` `Ruby
    # Name is not equal to false or nil, I will be initialized with Bozhidar
    name | | = 'Bozhidar'
    `` `

* The `boolean variable | you should not be using the =` |
  (Let's consider what happens when the current value was `false`).

    `` `Ruby
    # Bad example - true will contain any false, even if enabled
    enabled | | = true

    # A good example
    enabled = true if enabled.nil?
    `` `

* Pre-processing of the variable you do not know value is entering Let's use `=` &&.
  `&& =` Because you change the value only when the variable exists and if I use the,
  You can remove is used to verify the presence unnecessary `if`.

    `` `Ruby
    # Bad example
    if something
      something = something.downcase
    end

    # Ok
    something = something.downcase if something

    # A good example
    something = something && something.downcase

    # Example better
    something && = something.downcase
    `` `

* Avoid blatant use of the equality operator `===`.
  As the name suggests, it has been used in the determination of conditions for `case`,
  And it can be confusing if you use it in the outside.

    `` `Ruby
    # Bad example
    Array === something
    (1 .. 100) === 7
    / Something / === some_string

    # A good example
    something.is_a? (Array)
    (1 .. 100). Include? (7)
    some_string = ~ / something /
    `` `

* Perl-style: it; Let's avoid the use (`$ $` or `such as`) of a special variable.
  They are very cryptic,
  Motivation is Soga as they are used by a script other than the one line.
  `Let's using an alias is kind to a person that is provided by the English` library.

    `` `Ruby
    # Bad example
    $:. Unshift File.dirname (__FILE__)

    # A good example
    require 'English'
    $ LOAD_PATH.unshift File.dirname (__FILE__)
    `` `

* You should not put any space between the beginning of the method name and argument of `(`.

    `` `Ruby
    # Bad example
    f (3 + 2) + 1

    # A good example
    f (3 + 2) + 1
    `` `

* The first argument of the method if starting with `(`,
  Let's use `()` method to call at all times.
  For example, I write as follows:
`F ((3 + 2) + 1)`.

* When you run the Ruby interpreter, let's add a `-w` always optional.
  It can warn when you forget any of the rules so far!

* Let's have a new literal to lambda that has the body of a single line.
  `Let's use when they span multiple lines lambda`.

    `` `Ruby
    # Bad example
    l = lambda {| a, b | a + b}
    l.call (1, 2)

    # Correct, But I'm jerky
    l = -> (a, b) do
      tmp = a * 7
      tmp * b / 50
    end

    # A good example
    l = -> (a, b) {a + b}
    l.call (1, 2)

    l = lambda do | a, b |
      tmp = a * 7
      tmp * b / 50
    end
    `` `

* `I prefer` proc `more Proc.new`.

    `` `Ruby
    # Bad example
    p = Proc.new {| n | puts n}

    # A good example
    p = proc {| n | puts n}
    `` `

* I prefer the `proc.call ()` more `proc. ()` And [] `` proc to call the proc and lambda.

    `` `Ruby
    # Bad example - it appears to be similar to the access of an enumerated type
    l = -> (v) {puts v}
    l [1]

    # Here also a bad example - is unusual syntax
    l = -> (v) {puts v}
    l. (1)

    # A good example
    l = -> (v) {puts v}
    l.call (1)
    `` `

* Let's use `_` The block argument is not used.

    `` `Ruby
    # Bad
    result = hash.map {| k, v | v + 1}

    # Good
    result = hash.map {| _, v | v + 1}
    `` `

* `Let's using the` $ stdout / $ stderr / $ stdin `instead of STDOUT / STDERR / STDIN`.
  `STDOUT / STDERR / STDIN` is a constant,
  Constant in Ruby can be reassignment actually (you can also redirect to other streams),
  Warning from the interpreter will appear when you reallocated.

* `Let's using the` warn `instead of $ stderr.puts`.
  Aside the clarity and brevity,
  `You can suppress the warning if necessary, warn`
  (You can accomplish this by setting to 0 by using the `-W0` the warning level).

* I prefer and `sprintf` from `String #%` method inexplicable `format`.

    `` `Ruby
    # Bad example
    '% D% d'% [20, 10]
    # => '20 10 '

    # A good example
    sprintf ('% d% d', 20, 10)
    # => '20 10 '

    # A good example
    sprintf ('% {first}% {second}', first: 20, second: 10)
    # => '20 10 '

    format ('% d% d', 20, 10)
    # => '20 10 '

    # A good example
    format ('% {first}% {second}', first: 20, second: 10)
    # => '20 10 '
    `` `

* I prefer `Array # join` than the mysterious `Array # *` method.

    `` `Ruby
    # Bad example
    % W (one two three) * ','
    # => 'One, two, three'

    # A good example
    % W (one two three). Join (',')
    # => 'One, two, three'
    `` `

* I do not know whether the argument is an array, but when you want to process and treat it as an array,
  Than demonstrate the check of the array, let's use instead and `[* var]` `Array () to`.

    `` `Ruby
    # Bad example
    paths = [paths] unless paths.is_a? Array
    paths.each {| path | do_something (path)}

    # A good example
    [* Paths] each. {| Path | do_something (path)}

    # (I'm easy to read and a little) a good example
    . Array (paths) each {| path | do_something (path)}
    `` `

* Instead of complex comparison logic,
  Let's use and as long as the `Range` possible `Comparable # between?`.

    `` `Ruby
    # Bad example
    do_something if x> = 1000 && x <= 2000

    # A good example
    do_something if (1000 .. 2000). include? (x)

    # A good example
    do_something if x.between? (1000, 2000)
    `` `

* `==` Let's using the determination method than the comparison that makes clear the.
  Comparison of the number is OK.

    `` `Ruby
    # Bad example
    if x% 2 == 0
    end

    if x% 2 == 1
    end

    if x == nil
    end

    # A good example
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
    `` `

* `Let's avoid the use of BEGIN` blocks.

* The `Do not use the END` block. Let's use the `Kernel # at_exit` instead.

    `` `Ruby
    # Bad example

    END {puts 'Goodbye!'}

    # A good example

    at_exit {puts 'Goodbye!'}
    `` `

* Avoid the use of flip-flop.

* Avoid nesting of conditional expression control syntax.
  I like the guard clause to assert incorrect data.
  Guard clause, to go out from the function as far as possible,
  This is a conditional expression is declared near the beginning of the function.

    `` `Ruby
    # Bad example
      def compute_thing (thing)
        if thing [: foo]
          update_with_bar (thing)
          if thing [: foo] [: bar]
            partial_compute (thing)
          else
            re_compute (thing)
          end
        end
      end

    # A good example
      def compute_thing (thing)
        return unless thing [: foo]
        update_with_bar (thing [: foo])
        return re_compute (thing) unless thing [: foo] [: bar]
        partial_compute (thing)
      end
    `` `

# # Naming convention

> That the programming only difficult one is the designation and cache invalidation. <br/>
> - Phil Karlton

* Let's named in English identifier.

    `` `Ruby
    # Bad example - identifier is a character string a non-ascii
    заплата = 1_000

    # Bad Example - (instead of Cyrillic characters) has been written in Latin characters, but identifier is Bulgarian
    zaplata = 1_000

    # A good example
    salary = 1_000
    `` `

* Let's using the `snake_case` symbol, methods, variables.

    `` `Ruby
    # Bad example
    : 'Some symbol'
    : SomeSymbol
    : SomeSymbol

    someVar = 5

    def someMethod
      ...
    end

    def SomeMethod
     ...
    end

    # A good example
    : Some_symbol

    def some_method
      ...
    end
    `` `

* Let's using the `CamelCase` The module or class. (Acronym HTTP, RFC, such as XML Keep your case).

    `` `Ruby
    # Bad example
    class Someclass
      ...
    end

    class Some_Class
      ...
    end

    class SomeXml
      ...
    end

    # A good example
    class SomeClass
      ...
    end

    class SomeXML
      ...
    end
    `` `

* Let's using the `SCREAMING_SNAKE_CASE` The other constants.

    `` `Ruby
    # Bad example
    SomeConst = 5

    # A good example
    SOME_CONST = 5
    `` `

* Let's put an end to `?` (Boolean value is returned) the condition determination method
  (Ie, skip as `Array # empty?`).
  Method must return a boolean value, it should not be with a `? 'At the end.
** Method that might dangerous *
  And what changes are made to the attributes of `self` (ie,
  `Those exit!` (Finalizer is not run unlike `exit`) such as)
  Is used to indicate that it is a * dangerous *,
  Let's put a `! 'At the end.

    `` `Ruby
    # Bad example - it is a method 'safe'
    class Person
      def update!
      end
    end

    # A good example
    class Person
      def update
      end
    end

    # A good example
    class Person
      def update!
      end

      def update
      end
    end
    `` `

* As much as possible, let's define a safe method from the point of view of a dangerous method.

    `` `Ruby
    class Array
      def flatten_once!
        res = []

        each do | e |
          [* E] each. {| F | res << f}
        end

        replace (res)
      end

      def flatten_once
        dup.flatten_once!
      end
    end
    `` `

* When using `reduce` along with the short block, the argument `| Let's named` | a, e.
  (Accumulator, element).
* When you define a binary operator, let's argument using the `other`
  (Meaning, so will be different and `<<` and `[]`, which is an exception to this rule).

    `` `Ruby
    def + (other)
      # Body omitted
    end
    `` `

* More `collect` more `detect` more `find_all` `map`, `find`, `select`
  `` Reduce `, I prefer the` size `more` length `more inject`.
  It is not a requirement severe this;
  Find that using the alias if as long as the rise is readability,
  Use it is also OK.
  Method of perfect rhyme of them are inherited from Smalltalk,
  It is not very common in other languages.
  `Why is the recommended` select `than find_all` is,
  `When used with reject`, its name because it is very self-explanatory.

* `Instead of the combination of` flatten `, let's using the` flat_map `map`.
  This does not apply to an array of two or more in depth.
  That is, when ['a', ['b', 'c']] of `` users.first.songs == is,
  `Let's using the` map + flatten `more flat_map`.
  `Whereas to flatten all of the array, only one-dimensional and flat in an array is` flat_map `flatten`.

    `` `Ruby
    # Bad example
    all_songs = users.map. (&: songs) flatten.uniq

    # A good example
    all_songs = users.flat_map. (&: songs) uniq
    `` `

* `Let's using the` reverse_each `instead of reverse.each`.
  `Reverse_each` does not create a new array, it is an advantage.

    `` `Ruby
    # Bad example
    array.reverse.each {...}

    # A good example
    array.reverse_each {...}
    `` `

# # Comments

> Good code has a great document.
> When you are trying to add comments to the code exactly,
> Want you to ask yourself, "how if improved code, or this comment would be unnecessary?"
> Let's clearer in the document to improve the code.
> - Steve McConnell

* I write a code descriptive code itself such that the documents, let's ignore the part of the rest of this section. Really!
* Would you like to write in English comment.
* Let's put one space between the first comment and `#`.
* Utilizing a comment longer than one word, let's use punctuation.
  [One space] Let's use the (http://en.wikipedia.org/wiki/Sentence_spacing) after the period.
* Avoid any extra comments.

    `` `Ruby
    # Bad example
    counter + = 1 # Increments counter by one.
    `` `

* Comments Let's keep up-to-date.
  Comments outdated, is worse than no comment.

> Seems like a good joke is good code - description of what I do not need. <br/>
> - Russ Olsen

* Avoid the comment that describes the bad code.
  Let's do refactoring to the code self-explanatory
  and (do not do or do - it. Yoda -'s story "try").

# # # Comments

* Annotations Would you like to write just above the code normally associated.
* After the keyword annotation `: let's continue the`.
  Let's write the problem behind it.
* If you take more than one line to describe the problem is if,
  Let's indentation are two spaces after the `#` following lines.

    `` `Ruby
    def bar
      # FIXME:. This has crashed occasionally since v3.2.1 It may
      # Be related to the BarBazUtil upgrade.
      baz (: quux)
    end
    `` `

* If the problem is clear, then description is redundant,
  At the end of the line that has a problem, annotations not body only should wear.
  This usage is an exception, not the rule.

    `` `Ruby
    def bar
      sleep 100 # OPTIMIZE
    end
    `` `

* Let's use the `TODO` If you want to write down to be added later, features and functions not now.
* Let's use the `FIXME` If you want to write down the broken code you need to fix.
* Let's use the `OPTIMIZE` If you want to write down, such as on the performance problems, inefficient code or slow.
* Let's use the `HACK` If you want to write down the smell of code to be removed in refactoring suspicious.
* Let's use the `REVIEW` To write down where it is necessary to confirm that it works as intended.
  Example: `REVIEW: Are we sure this is how the client does X currently`?
* If you feel properly, I do not have to be using your own keywords other,
  You should write to something like that and `README` keywords of them.

# # Class

* We will continue with our consistent structure by placing the class definition.

    `` `Ruby
    class Person
      # I is the first thing we will do the include and extend
      extend SomeModule
      include AnotherModule

      # Constant definition is the following
      SOME_CONSTANT = 20

      # After that is the attributes macro
      attr_reader: name

      # (If any) other macros will continue
      validates: name

      # Public class methods is coming next
      def self.some_method
      end

      # Public instance methods followed
      def some_method
      end

      # Protected and private methods are summarized toward the back
      protected

      def some_protected_method
      end

      private

      def some_private_method
      end
    end
    `` `

* That the class has only class method is a module is preferred.
  It makes sense only to generating the instance class.

    `` `Ruby
    # Bad example
    class SomeClass
      def self.some_method
        # Body omitted
      end

      def self.some_other_method
      end
    end

    # A good example
    module SomeClass
      module_function

      def some_method
        # Body omitted
      end

      def some_other_method
      end
    end
    `` `

* If you want to the class method and an instance method of the module,
  `` Module_function `is preferred to extend self`.

    `` `Ruby
    # Bad example
    module Utilities
      extend self

      def parse_something (string)
        # Do stuff here
      end

      def other_utility_method (number, string)
        # Do some more stuff
      end
    end

    # A good example
    module Utilities
      module_function

      def parse_something (string)
        # Do stuff here
      end

      def other_utility_method (number, string)
        # Do some more stuff
      end
    end
    `` `

* When carrying out the design of the class hierarchy,
  Replace principle of Liskov] (http://ja.wikipedia.org/wiki/% E3% 83% AA% E3% 82% B9% E3% 82% B3% E3% 83% 95% E3% 81% AE% E7% BD% AE% E6% 8F% 9B% E5% 8E% 9F% E5% 89% 87).
  Let's follow the.
* Possible only your class
  [SOLID] (http://en.wikipedia.org/wiki/SOLID_ (object-oriented_design \))
  Let's keep to.
* In order to describe the province of the class, let's provide a `to_s` method always.

    `` `Ruby
    class Person
      attr_reader: first_name,: last_name

      def initialize (first_name, last_name)
        @ First_name = first_name
        @ Last_name = last_name
      end

      def to_s
        "# {@ First_name} # {@ last_name}"
      end
    end
    `` `

* The definition of mutator and accessor simple, let's use the `attr` group.

    `` `Ruby
    # Bad example
    class Person
      def initialize (first_name, last_name)
        @ First_name = first_name
        @ Last_name = last_name
      end

      def first_name
        @ First_name
      end

      def last_name
        @ Last_name
      end
    end

    # A good example
    class Person
      attr_reader: first_name,: last_name

      def initialize (first_name, last_name)
        @ First_name = first_name
        @ Last_name = last_name
      end
    end
    `` `

* `Let's avoid the use of attr`. Let's use or `attr_reader` a `attr_accessor` instead.

    `` `Ruby
    # Bad example - (it has been deprecated in 1.9) does not make only one accessor
    attr: something, true
    This is the same as three # attr_reader: attr: one,: two,

    # A good example
    attr_accessor: something
    attr_reader: one,: two,: three
    `` `

* `Let's consider the use of Struct.new`,
  It makes it simple definitions accessor, comparison operators and constructors.

    `` `Ruby
    # A good example
    class Person
      attr_accessor: first_name,: last_name

      def initialize (first_name, last_name)
        @ First_name = first_name
        @ Last_name = last_name
      end
    end

    # Example better
    Person = Struct.new (: first_name,: last_name) do
    end
    `` ``

* `This is not to extend the Struct.new` - it is a new class already.
  It results in an extra class level,
  When it was more than once `require`, possibly causing it to strange error.

* If you want to offer additional ways of instantiating a class,
  Let's consider adding a factory method.

    `` `Ruby
    class Person
      def self.create (options_hash)
        # Body omitted
      end
    end
    `` `

* [Duck typing] (http://ja.wikipedia.org/wiki/% E3% 83% 80% E3% 83% 83% E3% 82% AF% E3% 83% BB% E3% 82% than inheritance 82% B0) BF% E3% 82% A4% E3% 83% 94% E3% 83% B3% E3% is preferred.

    `` `Ruby
    # Bad example
    class Animal
      # Abstract method
      def speak
      end
    end

    # Inheritance
    class Duck <Animal
      def speak
        puts 'Quack! Quack'
      end
    end

    # Inheritance
    class Dog <Animal
      def speak
        puts 'Bau! Bau!'
      end
    end

    # A good example
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
    `` `

* Behavior in inheritance because "awkward", let's avoid using class variables (`@ @`).

    `` `Ruby
    class Parent
      @ @ Class_var = 'parent'

      def self.print_class_var
        puts @ @ class_var
      end
    end

    class Child <Parent
      @ @ Class_var = 'child'
    end

    Parent.print_class_var # => will print "child"
    `` `

    As can be seen all the classes in the class hierarchy,
    I will try to share one class variable actually.
    Class instance variable is preferred to class variable.

* Along the usage it was an accident, let's set visibility (`private`, `protected`) a.
  It is suggested that you do not leave (the default setting) `public` all.
  We because I are writing now * Ruby * after all. * And instead of Python *.
* `Public`, `protected`, the `private`, let's indentation in the same method definition to apply.
  In order to emphasize that it is applied to a method identifier after defining visibility,
  Let's put a blank line at the top and bottom of the identifier.

    `` `Ruby
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
    `` `

* Let's using `def self.method` When you define a singleton method.
  Since not repeat the class name, you will be able to refactor easily.

    `` `Ruby
    class TestClass
      # Bad example
      def TestClass.some_method
        # Body omitted
      end

      # A good example
      def self.some_other_method
        # Body omitted
      end

      # When you must define a singleton method of a lot
      # This format is also convenient, I can tolerate.
      class << self
        def first_method
          # Body omitted
        end

        def second_method_etc
          # Body omitted
        end
      end
    end
    `` `

# # Exception

* Let's using the `fail` is an exception occurs.
  `Let's use only when you can catch an exception, generating again raise`
  (because, instead of fall is here, it is because it raises an exception with a purpose explicitly).

    `` `Ruby
    begin
      fail 'Oops'
    rescue => error
      raise if error.message! = 'Oops'
    end
    `` `

* 2 argument in `fail / raise`, it is suggested that you do not explicitly `RuntimeError`.

    `` `Ruby
    # Bad example
    fail RuntimeError, 'message'

    # Good example - RuntimeError occurs by default
    fail 'message'
    `` `

* Instead of the exception instance,
  Message and exception class is divided `fail / raise` is preferred.

    `` `Ruby
    # Bad example
    fail SomeException.new ('message')
    # `It is important to note that writing to fail SomeException.new ('message'), and backtrace` does not exist.

    # A good example
    fail SomeException, 'message'
    # `Is consistent with the usage fail SomeException, 'message', the backtrace`
    `` `

`* Do not block from ensure` If you want to `return`.
  If you want to return a value explicitly from `ensure` if is,
  `It is also possible to write before any exception occurs return`,
  Let's return the values ​​as exceptions, such as if it had not occurred.
  In effect, the exception is silently discarded.

    `` `Ruby
    def foo
      begin
        fail
      ensure
        return 'very bad idea'
      end
    end
    `` `

* Where possible, let's begin with a block * of * implicit.

    `` `Ruby
    # Bad example
    def foo
      begin
        # Main logic goes here
      rescue
        # Failure handling goes here
      end
    end

    # A good example
    def foo
      # Main logic goes here
    rescue
      # Failure handling goes here
    end
    `` `

** (This is a word made by Avdi Grimm) method * that uncertainty
  Let's soften the spread of `begin` using.

    `` `Ruby
    # Bad example
    begin
      something_that_might_fail
    rescue IOError
      # Handle IOError
    end

    begin
      something_else_that_might_fail
    rescue IOError
      # Handle IOError
    end

    # A good example
    def with_io_error_handling
       yield
    rescue IOError
      # Handle IOError
    end

    with_io_error_handling {something_that_might_fail}

    with_io_error_handling {something_else_that_might_fail}
    `` `

* It must not be a cover-up exception.

    `` `Ruby
    # Bad example
    begin
      # An exception occurs here
    rescue SomeError
      # The rescue clause does absolutely nothing
    end

    # Bad example
    do_something rescue nil
    `` `

* `Let's avoid the guard clause of the rescue`.

    `` `Ruby
    # Bad example - to the island to catch all the classes that inherit it with StandardError
    read_file rescue handle_error ($!)

    # A good example - I will catch only class that inherits from it and Errno :: ENOENT
    def foo
      read_file
    rescue Errno :: ENOENT => ex
      handle_error (ex)
    end
    `` `


* You are not allowed to use the exception to the control flow.

    `` `Ruby
    # Bad example
    begin
      n / d
    rescue ZeroDivisionError
      puts 'Cannot divide by 0!'
    end

    # A good example
    if d.zero?
      puts 'Cannot divide by 0!'
    else
      n / d
    end
    `` `

* `To` rescue `is the Exception` Avoid.
  Since the signal of `exit` also capture, this will require -9 `` kill.

    `` `Ruby
    # Bad example
    begin
      # Calls to exit and kill signals will be caught (except kill -9)
      exit
    rescue Exception
      puts "you didn't really want to exit, right?"
      # Exception handling
    end

    # A good example
    begin
      # A blind rescue rescues from StandardError, not Exception as many
      # Programmers assume.
    rescue => e
      # Exception handling
    end

    # This is also a good example
    begin
      # An exception occurs here

    rescue StandardError => e
      # Exception handling
    end

    `` `

* Let's placed on top of the `rescue` chain a more detailed exception.
  And if not, it will not be `rescue` never.

    `` `Ruby
    # Bad example
    begin
      # Some code
    rescue Exception => e
      # Some handling
    rescue StandardError => e
      # Some handling
    end

    # A good example
    begin
      # Some code
    rescue StandardError => e
      # Some handling
    rescue Exception => e
      # Some handling
    end
    `` `

* The program included the external resources, let's open at `ensure`

    `` `Ruby
    f = File.open ('testfile')
    begin
      # .. Process
    rescue
      # .. Handle error
    ensure
      f.close unless f.nil?
    end
    `` `

* That it than to introduce a new exception class, using the exception of the basic class library is preferred.

# # Collections

* If a literal array or hash is preferred.
  (Although is that, except for the case to pass arguments to the constructor)

    `` `Ruby
    # Bad example
    arr = Array.new
    hash = Hash.new

    # A good example
    arr = []
    hash = {}
    `` `

* (Or an empty string, there are no spaces in the string) array syntax of the string,
  `% W` person of the literal is preferred.
  This rule is applied to an array of two or more elements.

    `` `Ruby
    # Bad example
    STATES = ['draft', 'open', 'closed']

    # A good example
    STATES =% w (draft open closed)
    `` `

* `% I` is preferred when the sequence of symbols is required
  (Maintaining compatibility with Ruby 1.9 and you do not need).
  This rule is applied to an array of two or more elements.

    `` `Ruby
    # Bad example
    STATES = [: draft,: open,: closed]

    # A good example
    STATES =% i (draft open closed)
    `` `

* The `Avoid`, behind the last element and Array `of` Hash `literal`.
  Avoid especially when it is not divided into multiple lines.

    `` `Ruby
    # Bad example - you can move, add, delete elements easily, but still it is not preferred.
    VALUES = [
               1001,
               2020,
               3333,
             ]

    # Bad example
    VALUES = [1001, 2020, 3333,]

    # A good example
    VALUES = [1001, 2020, 3333]
    `` `

* You make a big gap in the array Avoid.

    `` `Ruby
    arr = []
    arr [100] = 1 # now you have an array with lots of nils
    `` `

* If you want to access the beginning or end of the array,
  `And` first `` last `is preferred more` [-1] or `[0]`.

* When dealing with the element of unique things, let's using the `Set` instead of `Array`.
  `Set` This is implemented element there is no overlap in such a way does not have the order.
  Internal and intuitive operation of `Array`, the speed of the discovery of element `Hash` has put together this.
* Symbol is preferred over string hash keys.

    `` `Ruby
    # Bad example
    hash = {'one' => 1, 'two' => 2, 'three' => 3}

    # A good example
    hash = {one: 1, two: 2, three: 3}
    `` `

* The use of the hash key to an object that can be changed to Avoid.

* In the case of the symbol, key let using the syntax of hash literal.

    `` `Ruby
    # Bad example
    hash = {: one => 1,: two => 2,: three => 3}

    # A good example
    hash = {one: 1, two: 2, three: 3}
    `` `

* More `Hash # has_key?` A `Hash # key?`,
  `Let's using the` Hash # value? `More Hash # has_value?`.
    [Here] (http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-core/43765)
  In Matz is as stated, abolition have been investigated for long notation.

    `` `Ruby
    # Bad example
    ? hash.has_key (: test)
    hash.has_value? (value)

    # A good example
    ? hash.key (: test)
    hash.value? (value)
    `` `

* When dealing with key should be present, let's use the `Hash # fetch`.

    `` `Ruby
    heroes = {batman: 'Bruce Wayne', superman: 'Clark Kent'}
    # Bad example - you might not be able to notice immediately, even if there is an error if
    heroes [: batman] # => "Bruce Wayne"
    heroes [: supermann] # => nil

    # Good example - fetch so throw a KeyError, problem will reveal
    heroes.fetch (: supermann)
    `` `

* In order to not to use your own logic,
  `Let's introduce a default value in the Hash # fetch` through.

   `` `Ruby
   batman = {name: 'Bruce Wayne', is_evil: false}

   # Bad example - if the value is determined to be false came in, it may not work to get off to be wanted
   batman [: is_evil] | | true # => true

   # A good example - I will work correctly value is determined to be false, even if on
   batman.fetch (: is_evil, true) # => false
   `` `

* For `Hash # fetch`, by using the block instead of the default value is preferred.

   `` `Ruby
   batman = {name: 'Bruce Wayne'}

   # Bad example - the default value is used, I will be evaluated first
   # So, if it is called multiple times, then the program is slow
   batman.fetch (: powers, get_batman_powers) # get_batman_powers is an expensive call

   # Good example - block will be evaluated later. So, KeyError will trigger the evaluation
   batman.fetch (: powers) {get_batman_powers}
   `` `

* Let's trust that the hash that are ordered in Ruby 1.9 now.
* Do not you'll make changes when you are scanning the collection.

# # String

* I prefer the string inserted in place of the string concatenation.

    `` `Ruby
    # Bad example
    email_with_name = user.name + '<' + user.email + '>'

    # A good example
    email_with_name = "# {user.name} <# {user.email}>"
    `` `

* Let's consider putting a space in the string is inserted.
  Code separate from the string becomes more clear.

    `` `Ruby
    "# {User.last_name}, # {user.first_name}"
    `` `

* Or when there is no need for string insertion, if there is no special character and `\ t` of `\ n `` '`, etc.,
  Single quotes is preferred.

    `` `Ruby
    # Bad example
    name = "Bozhidar"

    # A good example
    name = 'Bozhidar'
    `` `

* You should not be using the character literal syntax `? X`.
  It is redundant basically from Ruby 1.9 -
  `? X` will be converted to (a one-character string) `'x'`

    `` `Ruby
    # Bad example
    char =? c

    # A good example
    char = 'c'
    `` `

* Around the global variable or instance variable that is inserted in the string
  `You should not be omitted {}`.

    `` `Ruby
    class Person
      attr_reader: first_name,: last_name

      def initialize (first_name, last_name)
        @ First_name = first_name
        @ Last_name = last_name
      end

      # Bad example - is valid, but is awkward
      def to_s
        "# @ First_name # @ last_name"
      end

      # A good example
      def to_s
        "# {@ First_name} # {@ last_name}"
      end
    end

    $ Global = 0
    # Bad example
    puts "$ global = # $ global"

    # A good example
    puts "$ global = # {$ global}"
    `` `

* If you need to make large chunks of data, let's avoid the use of `String # +`.
  Instead, we'll use a `String # <<`.
  Consolidated `String # <<`, to rewrite the string directly instance,
  `It is always faster than the String # +`,
  `To the island by creating a new object of a lot of String # +`.

    `` `Ruby
    Example # fast and well
    html =''
    html << '<h1> Page title </ h1>'

    paragraphs.each do | paragraph |
      html << "<p> # {paragraph} </ p>"
    end
    `` `

* When using a here document of more than one line,
  Must keep in mind that it arises also holds leading spaces.
  It is practical to employ a margin to remove excess space.

    `` `Ruby
    code = <<-END.gsub (/ ^ \ s + \ | /,'')
      | Def test
      | Some_method
      | Other_method
      | End
    END
    # => "Def test \ n some_method \ n other_method \ nend \ n"
    `` `

# # Regular expression

> When you run into a problem, I think "Yeah, I'll use the regular expression" and.
> There are two problems there. <br/>
> - Jamie Zawinski

* When you only look for from a string in plain text simply,
  Let's use the `string ['text']`: Do not use regular expressions.
* For the sake of simplicity, let's pass the regular expression directly into the string indices.

    `` `Ruby
    match = string [/ regexp /] # get content of matched regexp
    first_group = string [/ text (grp) /, 1] # get content of captured group
    string [/ text (grp) /, 1] = 'replace' # string => 'text replace'
    `` `

* When it is not necessary to use the result of the captured, let's using the group that is not captured.

    `` `Ruby
    / | Bad example (first second) / #
    /: | A good example (first second?) / #
    `` `

* You should not be using the variable cryptic Perl legacy of indicating the value that matched the regular expression at the end
  (`$ 1`, and `$ 2`).
  Let `Regexp.last_match using the [n]` instead.

    `` `Ruby
    / (Regexp) / = ~ string
    ...

    # Bad example
    process $ 1

    # A good example
    process Regexp.last_match [1]
    `` `


* Because become difficult to follow what values ​​are entered,
  You use the group you ordered Avoid.
  Let's use a group named instead.

    `` `Ruby
    # Bad example
    / (Regexp) / = ~ string
    ...
    process Regexp.last_match [1]

    # A good example
    / (? <meaningful_var> Regexp) / = ~ string
    ...
    process meaningful_var
    `` `

* Within the character class, characters that have a special meaning is small you need to be careful:
  `^`, `-`, `\`, `Only]` is because it has a special meaning,
  `.` You should not be escaped in the `[]` a.

* `^` `$` And is not the beginning or end of a string,
  It is important to note because it matches the beginning and end of a line.
  When you want to match to the top end of the string if the whole,
  `\ Let's use A`, the `\ z`
  (It is suggested that you do not confuse it is equivalent to `\ n? \ Z` and `\ Z`).

    `` `Ruby
    string = "some injection \ nusername"
    string [/ ^ username $ /] # matches
    string [/ \ Ausername \ z /] # don't match
    `` `

* Let's use the `x` identifier for complex regular expression.
  It is easy to read more by using this,
  I will be able to use the handy comment.
  It is important to note that space is ignored.

    `` `Ruby
    regexp =% r {
      start # some text
      \ S # white space char
      (Group) # first group
      (:? Alt1 | alt2) # some alternation
      end
    } X
    `` `

* `Complex substitution at sub` / `gsub`, but it is possible to use a hash or block.

# #% Literal

* A string of one-line insertion and `" `both is entered,
  `% Let's use the ()` (short of `% Q ()`).
  I prefer here documents when more than one line.

    `` `Ruby
    # (There is no need of insertion) bad example
    % (<div Class="text"> Some text </ div>)
    # Should be '<div class="text"> Some text </ div>'

    # (No double quotes) bad example
    % (This is # {quality} style)
    # Should be "This is # {quality} style"

    # Bad example (is a multi-line)
    % (<div> \ N <span class="big"> # {exclamation} </ span> \ n </ div>)
    # Should be a heredoc.

    # (One line insertion is necessary, and double quotes, a) a good example
    % (<tr> <td Class="name"> # {name} </ td>)
    `` `

* As long as both the `'` and `" `in the string is not included,
  `% Avoid the use of q`.
  And when it is not necessary to escape a string of many,
  More of regular string literals more readable,
  Should be recommended.

    `` `Ruby
    # Bad example
    name =% q (Bruce Wayne)
    time =% q (8 o'clock)
    question =% q ("What did you say?")

    # A good example
    name = 'Bruce Wayne'
    time = "8 o'clock"
    question = '"What did you say?"'
    `` `

* '/' Is only more than * one * regular expression, we'll use a `% r`.

    `` `Ruby
    # Bad example
    % R (\ s +)

    # This is also a bad example
    % R (^ / (. *) $)
    # Should be / ^ \ / (. *) $ /

    # A good example
    % R (^ / blog/2011 / (. *) $)
    `` `

* Backquote is included in the command to call (it is not quite happen but) as long as there is no thing,
  `% Avoid the use of x`.

    `` `Ruby
    # Bad example
    date =% x (date)

    # A good example
    date = `date`
    echo =% x (echo `date`)
    `` `

* `% Avoid the use of s`.
  Ruby community, when creating a symbol that includes a space to
  `: It seems to have decided" string "` is good.

* Delimiter percent of literals are preferred by `()` with the exception of `% r`.
  Within the regular expression, it will be used, in various scenes and `()`,
  Depending on the contents of the regular expression, and prefer `{` little chance to be used more
  You might be a good choice.

    `` `Ruby
    # Bad example
    % W [one two three]
    % Q {"Test's king!", John said.}

    # A good example
    % W (one two three)
    % Q ("Test's king!", John said.)
    `` `

# # Meta-programming

* Avoid unnecessary meta-programming. Avoid needless metaprogramming.

* The tainting the core classes that are written in the library Let us not
  (I do not do it by applying a monkey patch).

* More of block passing `class_eval` is the preferred over string insertion type.
  - When you use the string insertion type, and race back to work, let's pass the `__LINE__` and `__FILE__` always:

    `` `Ruby
    class_eval 'def use_relative_model_naming;? true; end', __ FILE__, __ LINE__
    `` `

  - `Define_method` who is, is preferred over {def ...} `` class_eval.

* When using a string insertion type (or other `eval`) `class_eval` a is,
  (It is used in Rails) and let's add to the comments of the code when it is inserted.

    `` `Ruby
    # From activesupport / lib / active_support / core_ext / string / output_safety.rb
    UNSAFE_STRING_METHODS.each do | unsafe_method |
      if 'String'. respond_to? (unsafe_method)
        class_eval <<-EOT, __ FILE__, __ LINE__ + 1
          def # {unsafe_method} (* args, & block) # def capitalize (* args, & block)
            to_str. # {unsafe_method} (* args, & block) # to_str.capitalize (* args, & block)
          end # end

          def # {unsafe_method}! (* args) # def capitalize! (* args)
            @ Dirty = true # @ dirty = true
            super # super
          end # end
        EOT
      end
    end
    `` `

* `Let's avoid the meta-programming with method_missing`.
  This is because, the backtrace is in trouble,
  `# Will not come out in the list of methods`,
  Method calls that you misspelled will also move in silence,
  For example, as in this `nukes.launch_state = false`.
  Instead, let's use transfer, or proxy, the `define_method`.
  If you must use the `method_missing` if you:

  - [? `Respond_to_missing`] Let's check (http://blog.marc-andre.ca/2010/11/methodmissing-politely.html) also are being implemented
  - Let the asserted as much as possible - you'll capture prefix known, things like `find_by_ *`
  - Let's call the `super` at the end
  - Let's transfer to assert, in the method it is not special:

    `` `Ruby
    # Bad example
    def method_missing? (meth, * args, & block)
      if / ^ find_by_ (? <prop>. *) / = ~ meth
        # ... Lots of code to do a find_by
      else
        super
      end
    end

    # A good example
    def method_missing? (meth, * args, & block)
      if / ^ find_by_ (? <prop>. *) / = ~ meth
        find_by (prop, * args, & block)
      else
        super
      end
    end

    # Still the best choice is to define_method to attribute all of that can be found
    `` `

# # Miscellaneous

* `Let's write secure code in ruby-w`.
* Avoid the use of hash as an optional variable. Is not there too much to do? (Initialization of an object is an exception to this rule)
* Methods that line of code is more than 10 lines Avoid.
  Ideally speaking, within five lines is a good number of methods.
  It is not included in the number of lines blank line.
* And to set the argument more than three or four to Avoid.
* If you need a method "global" really is if,
  Define the Kernel, let's set to private.
* Instead of a global variable, let's use an instance variable of the module.

    `` `Ruby
    # Bad example
    $ Foo_bar = 1

    # A good example
    module Foo
      class << self
        attr_accessor: bar
      end
    end

    Foo.bar = 1
    `` `

* `When alias_method` moves, let's avoid the `alias`.
* Let's use the `OptionParser` to parse the complex command line options.
  In addition, we'll use a `ruby-s` The trivial option.
* To read the current system time, we'll use a `Time.now` than `Time.new`.
* If so there is no problem, let's write the code in the method of functional avoid the destructive process.
* Unless the purpose of the method, it is to the destructive changes to the argument Let us not.
* Avoid nesting more than three stages.
* Keep your consistency. Ideally speaking, let along these guidelines.
* Let's use common sense.

# # Tool

Here are a few tools to help you to automatically check the code contrary to this guide.

# # # RuboCop

[RuboCop] (https://github.com/bbatsov/rubocop) was based on this guide
Is Ruby code style checker.
Rubocop covers an important part of this guide already,
It supports MRI 1.9, 2.0 both MRI, there is a plug-in for good Emacs.

# # # RubyMine

[RubyMine] code inspection of (http://www.jetbrains.com/ruby/) is, in this guide
[Based in part] (http://confluence.jetbrains.com/display/RUBYDEV/RubyMine+Inspections).

# Contributing

There is nothing that can not change is that it is written in this guide.
To tackle together with all people who are interested in code style of Ruby is so my hope,
I think ultimately, and if it is possible to create a useful resource for all of the Ruby community.

For improvement, please or send a pull request to put up a ticket not hesitate.
I thank you in advance to help you!

# # In order to contribute

Is easy! [Contribution guidelines] Please read the (https://github.com/bbatsov/ruby-style-guide/blob/master/CONTRIBUTING.md)!

# License

! [Creative Commons License] (http://i.creativecommons.org/l/by/3.0/88x31.png)
This copyrighted material, [Creative Commons Attribution 3.0 Unported License] (http://creativecommons.org/licenses/by/3.0/deed.en_US)
I will follow.

# Let's spread

Style Guide of community-driven, of little use to the community that does not know this.
You can muttered about this guide, please share to your friends and colleagues.
All comments, suggestions, options will continue to well just a little this guide.
The guide of the best conceivable is not it want?

Thank <br/>
[Bozhidar] (https://twitter.com/bbatsov)
