# [Semicolons](#semicolons)

The formal grammar uses semicolons ";" as terminators in a number of productions. Go programs may omit most of these semicolons using the following two rules:

1. When the input is broken into tokens, a semicolon is automatically inserted into the token stream immediately after a line's final token if that token is
  + an [identifier](/Lexical%20elements/identifiers.html)
  + an [integer](/Lexical%20elements/integer_literals.html), [floating-point](/Lexical%20elements/floating-point_literals.html), [imaginary](/Lexical%20elements/imaginary_literals.html), [rune](/Lexical%20elements/rune_literals.html), or [string](/Lexical%20elements/string_literals.html) literal
  + one of the [keywords](/Lexical%20elements/keywords.html) break, continue, fallthrough, or return
  + one of the [operators and punctuation](/Lexical%20elements/operators_and_punctuation.html) ++, --, ), ], or }
2. To allow complex statements to occupy a single line, a semicolon may be omitted before a closing ")" or "}".

To reflect idiomatic use, code examples in this document elide semicolons using these rules.
