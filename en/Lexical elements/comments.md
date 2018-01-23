# [Comments](#comments)

Comments serve as program documentation. There are two forms:

1. *Line comments* start with the character sequence // and stop at the end of the line.
2. *General comments* start with the character sequence /\* and stop with the first subsequent character sequence \*/.

A comment cannot start inside a [rune](/Lexical%20elements/rune_literals.html) or [string literal](/Lexical%20elements/string_literals.html), or inside a comment. A general comment containing no newlines acts like a space. Any other comment acts like a newline.
