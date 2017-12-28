# Address operators

타입 `T`의 피 연산자 `x`에 대해, 주소 연산자인 `&x`는 `x`에 대한 `*T` 타입의 포인터를 생성한다. 피연산자는 주소 지정이 가능해야한다. 즉 변수, 포인터 간접 참조 또는 슬라이스 인덱싱 연산; 또는 주소 지정 가능한 struct 피 연산자의 필드 선택자; 또는 주소 지정 가능한 배열의 배열 인덱싱 연산이 그 예다. `x`가 (어쩌면 괄호 안에 있는) [합성 리터럴](/Expressions/composite_literals.html)일 경우는 주소가 지정가능하지 않아도 되는 예외의 경우이다. If the evaluation of x would cause a [run-time panic](/Run-time%20panics/), then the evaluation of &x does too.

For an operand x of pointer type *T, the pointer indirection *x denotes the [variable](/Variables/) of type T pointed to by x. If x is nil, an attempt to evaluate *x will cause a [run-time panic](/Run-time%20panics/).

    &x
    &a[f(2)]
    &Point{2, 3}
    *p
    *pf(x)
    
    var x *int = nil
    *x   // causes a run-time panic
    &*x  // causes a run-time panic