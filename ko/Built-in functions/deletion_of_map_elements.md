# [map 요소 삭제](#deletion-of-map-elements)

내장 함수 `delete`는 키 `k`를 통해 [map](/Types/map_types.html) `m`으로부터 요소를 제거한다. `k`의 타입은 반드시 `m`의 키 타입에 [할당 가능](/Properties%20of%20types%20and%20values/assignability.html)해야 한다.

```go
delete(m, k)  // map m에서 m[k] 요소를 제거
```

map `m`이 `nil`이거나 요소 `m[k]`가 존재하지 않는다면, `delete`는 아무런 동작을 하지 않는 연산이다.
