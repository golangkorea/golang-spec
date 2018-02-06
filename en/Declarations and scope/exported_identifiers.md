# [Exported identifiers](#exported-identifiers)

An identifier may be *exported* to permit access to it from another package. An identifier is exported if both:

  1. the first character of the identifier's name is a Unicode upper case letter (Unicode class "Lu"); and
  2. the identifier is declared in the [package block](/Blocks/) or it is a [field name](/Types/struct_types.html) or [method name](/Types/interface_types.html#MethodName).

All other identifiers are not exported.
