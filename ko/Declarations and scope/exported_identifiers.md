# [내보내진(Exported) 식별자](#exported-identifiers]

식별자는 다른 패키지에서 접근 할 수 있게 내보내질(*exported*)  수 있다.
아래 두 경우에 식별자는 내보내 질 수 있다.

  1. 식별자의 이름에 첫번째 글자가 Unicode 대문자(Unicode class "Lu"); 그리고
  2. 식별자가 패키지 블록[package block](/Blocks/) 에서 선언 되거나, 필드 명[field name](/Types/struct_types.html) or 메소드 명[method name](/Types/interface_types.html#MethodName).

다른 식별자들은 내보내질 수 없다.
