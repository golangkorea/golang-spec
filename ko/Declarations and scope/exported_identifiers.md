# [엑스포트 된(Exported) 식별자](#exported-identifiers]

식별자는 다른 패키지에서 접근할 수 있게 *엑스포트 될* 수 있다. 아래 두 가지 조건을 모두 만족한다면 식별자는 엑스포트 될 수 있다.

  1. 식별자 이름의 첫 번째 캐릭터가 유니코드 중 알파벳 대문자(유니코드 클래스에서 "Lu" 에 해당함)이고;
  2. 식별자가 [패키지 블록](/Blocks/) 안에 선언되어 있거나, [필드 이름](/Types/struct_types.html) 또는 [메서드 이름](/Types/interface_types.html#MethodName)인 경우

이외의 식별자들은 엑스포트 될 수 없다.
