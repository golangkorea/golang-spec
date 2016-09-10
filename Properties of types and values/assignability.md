# Assignability

Assignability

A value x is assignable to a [variable](/Variables/) of type T ("x is assignable to T") in any of these cases:

  * x's type is identical to T.
  * x's type V and T have identical [underlying types](/Types/) and at least one of V or T is not a [named type](/Types/).
  * T is an interface type and x [implements](/Types/interface_types.html) T.
  * x is a bidirectional channel value, T is a channel type, x's type V and T have identical element types, and at least one of V or T is not a named type.
  * x is the predeclared identifier nil and T is a pointer, function, slice, map, channel, or interface type.
  * x is an untyped [constant](/Constants/) representable by a value of type T.