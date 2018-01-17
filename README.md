# 번역 플랫폼 도입 공지
효율적인 번역 프로젝트 관리를 위해 번역 플랫폼 Crowdin, Transifex 와 GitHub 연동 테스트를 진행한 결과, Transifex를 도입하기로 최종 결정했습니다. 2018년 1월 15일부터는 [Transifex](https://www.transifex.com/golang-korea/go-specification/)를 이용해 번역을 진행해주시길 바랍니다.

# golang-spec
[Go 언어 스펙](https://golang.org/ref/spec)에 대한 한글 번역 프로젝트입니다.

Go 언어 스펙 번역에 참여하실 분들은 아래 링크를 통해 본인이 번역하고자 하는 부분에 이름을 등록하시길 바랍니다.

https://docs.google.com/spreadsheets/d/1R-E_4SM1vGsUiGBLLVilUlahHxC7U1R592E3GLryYKA/edit?usp=sharing

Go 언어 스펙 번역 프로젝트는 효율적인 번역 프로젝트 관리를 위해 Transifex 번역 플랫폼을 사용합니다. Go 언어 스펙 번역에 참여하실 분들과 기존 번역 참가자들께서는 [Transifex](https://www.transifex.com/golang-korea/go-specification/)에서 `Help Translate Go Specification` 버튼을 이용해 번역자로 등록한 다음, 번역을 진행해주시길 바랍니다.

![transifex_registration](https://user-images.githubusercontent.com/8563047/34928124-cc4905c6-f9fe-11e7-9615-7828250e036f.png)


번역물은 [GitBook](https://www.gitbook.com/book/gosudaweb/go-language-specification-in-korean/details)에 호스트됩니다.

기본적인 번역 가이드라인에 대한 의견은 [issue](https://github.com/golangkorea/golang-spec/issues/2)를 이용해주세요. 

번역에 대한 질의 및 토의는 [GitHub issue](https://github.com/golangkorea/golang-spec/issues/) 게시판을 이용해주시기 바랍니다.

[Gitter 방](https://gitter.im/golang-korean-community/go-spec-in-korean?utm_source=share-link&utm_medium=link&utm_campaign=share-link)도 마련되어 있으니 많은 참여바랍니다.


# 번역 진행 과정

번역(Transifex) - Review - Merge - GitBook 포스팅 - Proof of Reading - Issue 생성 - Contents Update(Transifex)

- [Transifex](https://www.transifex.com/golang-korea/go-specification/)에서 `Help Translate Go Specification` 버튼을 이용해 프로젝트 번역자로 등록한 다음, 번역하고 싶은 파일을 찾아 번역을 시작하세요.
- [Transifex](https://www.transifex.com/golang-korea/go-specification/)에서 특정 파일에 대한 번역 작업이 완료되면 관리자/리뷰어들에 의해 번역물에 대한 리뷰가 진행됩니다.
- 원활한 리뷰 진행을 위해 번역 참가자들은 특정 챕터에 대한 번역 완료시 [Gitter 방](https://gitter.im/golang-korean-community/go-spec-in-korean?utm_source=share-link&utm_medium=link&utm_campaign=share-link)에 번역완료 사실을 알려주시길 바랍니다.
- 리뷰 과정에서 논의된 수정사항들을 반영하여 PR을 생성하면 최종적으로 transifex branch에 merge됩니다.
- GitHub에서 transifex branch에 merge되면 자동으로 [GitBook](https://www.gitbook.com/book/gosudaweb/go-language-specification-in-korean/details)에 포스팅됩니다. 
- [GitBook](https://www.gitbook.com/book/gosudaweb/go-language-specification-in-korean/details)에 포스팅된 이후에 발생하는 번역문 관련 모든 이슈는 [GitHub issue](https://github.com/golangkorea/golang-spec/issues/)로 보고해주시기 바랍니다.
- 번역 참가자(proof of reading 참가자 포함)는 GitBook에서 제공하는 disqus 댓글, discussion 기능 대신 [GitHub issue](https://github.com/golangkorea/golang-spec/issues/)를 이용해주세요.

# 번역 가이드라인

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
4. [용어집](https://github.com/golangkorea/golang-spec/blob/master/GLOSSARY.md)에서는 자주 사용되는 용어, 번역하기 힘들거나 애매한 용어들에 대한 추천 번역 및 설명을 제공하고 있습니다. GitBook에서는 [용어집](https://github.com/golangkorea/golang-spec/blob/master/GLOSSARY.md)에 등록된 용어가 본문에 있을 경우, 아래처럼 밑줄, 하이라이트, 팝업창 등의 기능을 제공합니다.(예제에서는 *code point*가 해당됩니다.)

![glossary](https://user-images.githubusercontent.com/8563047/33648108-b1b31814-da9b-11e7-9189-e42ba01c4137.png)

[용어집](https://github.com/golangkorea/golang-spec/blob/master/GLOSSARY.md) 용어 추가 건의, 번역 용어에 대한 의견은 [용어집 이슈 게시판](https://github.com/golangkorea/golang-spec/issues/105)을 이용해주세요.
 
5. 번역작업도 중요하지만 함께 작업하시는 분들의 내용을 Proof reading하는데 동참해 주십시오.