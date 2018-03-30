# golang-spec
[Go 언어 스펙](https://golang.org/ref/spec) 문서에 대한 번역 프로젝트입니다. golang-spec 프로젝트에서는 번역 수행, 번역 현황 관리, 문서 업데이트 지원 등을 위해 번역 플랫폼(transifex)을 도입하여 운영하고 있으며, 다국어 번역을 지원하고 있습니다. 

# golang-spec 프로젝트 운영 현황

- 번역 대상: go spec 버전 1.9
- 번역 현황: 한국어 번역 100% 완료. 기타 언어 미지원

# proof-readers 참가 방법
1. [GitBook](https://www.gitbook.com/book/gosudaweb/go-language-specification-in-korean/details) 문서를 읽습니다.
2. 오탈자, 번역 관련 의문 사항 또는 개념 설명 요청 등이 있을 경우 [GitHub issue](https://github.com/golangkorea/golang-spec/issues/) 게시판에서 issue 를 오픈합니다.

issue 에서 논의된 내용은 토론과 리뷰를 거쳐 번역문에 반영됩니다. 

[Gitter 방](https://gitter.im/golang-korean-community/go-spec-in-korean?utm_source=share-link&utm_medium=link&utm_campaign=share-link)도 마련되어 있으니 많은 참여바랍니다.

# 번역 가이드라인

go spec 문서 한국어 번역에 적용한 번역 가이드라인입니다. proof-reading 시 참고하시길 바랍니다. 


1. [타입](https://gosudaweb.gitbooks.io/go-language-specification-in-korean/content/Types/) 자체가 코드에서 사용되는 경우 `string 타입`과 같은 형태로 번역하고, 그 외에는 한글 번역을 적용하는 것을 원칙으로 합니다. 이 기준에 따라 [타입](https://gosudaweb.gitbooks.io/go-language-specification-in-korean/content/Types/)은 아래와 같이 번역합니다. 

> 불리언 타입, 숫자 타입, string 타입, 배열 타입, 슬라이스 타입, struct 타입, 포인터 타입, 함수 타입, interface 타입, map 타입, 채널 타입

```
// 번역 예시 
A string type represents the set of string values

string 타입은 문자열 값들의 집합을 표현한다.
```

2. EBNF에 따라 작성된 Go 문법은 번역하지 않는 것을 원칙으로 합니다.(주석은 번역 가능) 예를 들면,  [Characters 섹션](https://golang.org/ref/spec#Characters)에 나오는 문법 표현은 아래와 같습니다.

```
newline        = /* the Unicode code point U+000A */ .
unicode_char   = /* an arbitrary Unicode code point except newline */ .
unicode_letter = /* a Unicode code point classified as "Letter" */ .
unicode_digit  = /* a Unicode code point classified as "Number, decimal digit" */ .
```

Go 문법 표현은 원문 그대로 유지해 주시길 바라며, `/* the Unicode code point U+000A */`과 같은 주석은 한글로 번역하셔도 괜찮습니다.

3. 맺음말은 "~하다"로 통일하겠습니다.