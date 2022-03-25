# 스프링 MVC 2편 - 백엔드 웹 개발 활용 기술 

## 타임리프 - 기본기능 

### 프로젝트생성 


### 타임리프 소개 
```
공식 사이트: https://www.thymeleaf.org/
공식 메뉴얼 - 기본 기능: https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html
공식 메뉴얼 - 스프링 통합: https://www.thymeleaf.org/doc/tutorials/3.0/thymeleafspring.html

  이전 강의인 스프링 MVC 1편에서 타임리프를 간단히 사용해보고, 그 특징들도 알아보았다. 
  이번 시간에는 타임리프의 개념은 간단히 소개하고, 실제 동작하는 기본 기능 위주로 알아보겠다. 
  
  타임리프 특징 
    - 서버 사이드 HTML 렌더링(SSR)
	- 네추럴 템플릿
	- 스프링 통합 지원 
	
	- 서버 사이드 HTML 렌더링(SSR)
	  - 타임리프는 백엔드 서버에서 HTML을 동적으로 렌더링 하는 용도로 사용된다. 
	
	- 네추럴 템플릿 
	  - 타임리프는 순수 HTML을 최대한 유지하는 특징이 있다. 
	    타임리프로 작성한 파일은 HTML을 유지하기 때문에 웹 브라우저에서 파일을 직접 열어도 
		내용을 확인할 수 있고, 서버를 통해 뷰 템플릿을 거치면 동적으로 변경된 결과를 확인할 수 있다. 
		JSP를 포함한 다른 뷰 템플릿들은 해당 파일을 열면, 예를 들어서 JSP 파일 자체를 그대로 
		웹 브라우저에서 열어보면 JSP 소스코드와 HTML이 뒤죽박죽 섞여서 웹 프라우저에서 정상적인 
		HTML 결과를 확인할 수 없다. 오직 서버를 통해서 JSP가 렌더링 되고 HTML 응답 결과를 
		받아야 확인할 수 있다. 반면에 타임리프로 작성된 파일은 해당 파일을 그대로 웹 브라우저에서 
		열어도 정상적인 HTML 결과를 확인할 수 있다. 물론 이 경우 동적으로 결과가 렌더링 되지는 
		않는다. 하지만 HTML 마크업 결과가 어떻게 되는지 파일만 열어도 바로 확인할 수 있다.
		이렇게 순수 HTML을 그대로 유지하면서 뷰 템플릿도 사용할 수 있는 타임리프의 특징을 
		네추럴 템플릿(natural templates)이라 한다. 
	
	- 스프링 통합 지원 
	  - 타임리프는 스프링과 자연스럽게 통합되고, 스프링의 다양한 기능을 편리하게 사용할 수 있게 
	    지원한다. 이 부분은 스프링 통합과 폼 장에서 자세히 알아보겠다. 
	
  타임리프 기본 기능 
    - 타임리프를 사용하려면 다음 선언을 하면 된다. 
	  - <html xmlns:th="http://www.thymeleaf.org">
	
	- 기본 표현식 
	  - 타임리프는 다음과 같은 기본 표현식들을 제공한다. 지금부터 하나씩 알아보자. 
	    - 간단한 표현 
		  - 변수 표현식: ${...}
		  - 선택 변수 표현식: *{...}
		  - 메시지 표현식: #{...}
		  - 링크 URL 표현식: @{...}
		  - 조각 표현식: ~{...}
		- 리터럴 
		  - 텍스트; 'one text', 'Another one!',...
		  - 숫자: 0, 34, 3.0, 12,3,...
		  - 불린: true, false
		  - 널: null
		  - 리터럴 토큰: one, sometext, main,...
		- 문자 연산
		  - 문자 합치기: + 
		  - 리터럴 대체: |The name is ${name}|
		- 산술 연산:
		  - Binary operators: +, -, *, /, %
		  - Minus sign (unary operator): -
		- 불린 연산: 
		  - Binary operators: and, or 
		  - Boolean negation (unary operator): !, not
		- 비교와 동등: 
		  - 비교: >, <, >=, <= (gt, lt, ge, le)
		  - 동등 연산: ==, !=(eq, ne)
		- 조건 연산:
		  - If-then: (if) ? (then)
		  - If-then-else: (if) ? (then) : (else)
		  - Default: (value) ?: (defaultvalue)
		- 특별한 토큰:
		  - No-Operation: _
	
	참고: https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#standard-expression-syntax
```

### 텍스트 - text, utext 
```
  타임리프의 가장 기본 기능인 텍스트를 출력하는 기능을 먼저 알아보자. 
  타임리프는 기본적으로 HTML 태그의 속성에 기능을 정의해서 동작한다. HTML의 콘텐츠(content)에 
  데이터를 출력할 때는 다음과 같이 th:text를 사용하면 된다. 
  <span th:text="${data}">
  
  HTML 태그의 속성이 아니라 HTML 콘텐츠 영역안에서 직접 데이터를 출력하고 싶으면 
  다음과 같이  [[...]]를 사용하면 된다. 
    - 컨텐츠 안에서 직접 출력하기 = [[${data}]]

  Escape 
    - HTML 문서는 <,>같은 특수 문자를 기반으로 정의된다. 따라서 뷰 템플릿으로 
	  HTML 화면을 생성할 때는 출력하는 데이터에 이러한 특수 문자가 있는 것을 
	  주의해서 사용해야 한다. 앞에서 만든 예제의 데이터를 다음과 같이 변경해서 
	  실행해보자. 
	  
	  - 변경 전 
	    - "Hello Spring"
	  - 변경 후 
	    - "Hello <b>Spring!</b>"
		- <b> 태그를 사용해서 Spring!이라는 단어가 진하게 나오도록 해보자. 
	
	- 웹 브라우저에서 실행결과를 보자.
	  - 웹브라우저: Hello <b>Spring!</b>
	  - 소스보기:  Hello &lt;b&gt;Spring!&lt;/b&gt;
	
	- 개발자가 의도한 것은 <b>가 있으면 해당 부분을 강조하는 것이 목적이었다. 
	  그런데 <b> 태그가 그대로 나온다. 소스보기를 하면 < 부분이 &lt;로 
	  변경된 것을 확인할 수 있다. 
	
	- HTML 엔티티 
	  - 웹 브라우저는 <를 HTML 태그의 시작으로 인식한다. 따라서 <를 태그의 
	    시작이 아니라 문자로 표현할 수 있는 방법이 필요한데, 이것을 HTML 
		엔티티라 한다. 그리고 이렇게 HTML에서 사용하는 특수 문자를 
		HTML 엔티티로 변경하는 것을 이스케이프(escape)라 한다. 그리고 
		타임리프가 제공하는 th:text, [[..]]는 기본적으로 
		이스케이프(escape)를 제공한다.
		- < -> &lt;
		- > -> &rt;
		- 기타 수 많은 HTML 엔티티가 있다. 
	  참고 
	    - HTML 엔티티와 관련해서 더 자세한 내용은 HTML 엔티티로 검색해보자.

  Unescape 
    - 이스케이프 기능을 사용하지 않으려면 어떻게 해야할까?
	- 타임리프는 다음 두 기능을 제공한다ㅏ.
	  - th:text -> th:utext
	  - [[..]] -> [(...)]
	
	- text-unescape.html
	  - th:inline="none"
	    - 타임리프는 [[...]]를 해석하기 때문에, 화면에 [[...]]글자를
		  보여줄 수 없다. 이 태그 안에서는 타임리프가 해석하지 말라는 
		  옵션이다. 
	
	주의 
	  - 실제 서비스를 개발하다 보면 excape를 사용하지 않아서 HTML이 정상 
	    렌더링 되지 않는 수 많은 문제가 발생한다. escape를 기본으로 하고, 
		꼭 필요한 때만 unescape를 사용하자. 
```

### 변수 - SpringEL
```
  타임리프에서 변수를 사용할 때는 변수 표현식을 사용한다. 
    - 변수 표현식: ${...}
  그리고 이 변수 표현식에는 스프링 EL이라는 스프링이 제공하는 표현식을 사용할 수 있다. 
  
  SpringEL 다양한 표현식 사용
    - Object 
	  - user.username: user의 username을 프로퍼티 접근 -> user.getUsername()
	  - user['username']: 위와 같음 -> user.getUsername()
	  - user.getUsername(): user의 getUsername()을 직접 호출 
	
	- List 
	  - users[0].username: List에서 첫 번째 회원을 찾고 username 프로퍼티 접근 
	    -> list.get(0).getUsername()
	  - users[0]['username']: 위와 같음 
	  - users[0].getUsername(): List에서 첫 번째 회원을 찾고 메서드 직접 호출
	
	- Map 
	  - userMap['userA'].username: Map에서 userA를 찾고, 
	    username 프로퍼티 접근 -> map.get("userA").getUsername()
	  - userMap['userA']['username']: 위와 같음 
	  - userMap['userA'].getUsername(): Map에서 userA를 찾고 메서드 직접 호출

  지역 변수 선언 
    - th:with를 사용하면 지역 변수를 선언해서 사용할 수 있다. 지역 변수는 선언한 태그 안에서만 
	  사용할 수 있다. 
```

### 기본 객체들 
```
  타임리프는 기본 객체들을 제공한다. 
    - ${#request}
	- ${#response}
	- ${#session}
	- ${#servletContext}
	- ${#locale}

  그런데 #request는 HttpServletRequest 객체가 그대로 제공되기 때문에 데이터를 조회하려면 
  request.getParameter("data")처럼 불편하게 접근해야 한다. 
  이런 점을 해결하기 위해 편의 객체도 제공한다. 
    - HTTP 요청 파라미터 접근: param
	  - 예) ${param.paramData}
	- HTTP 세션 접근: session
	  - 예) ${session.sessionData}
	- 스프링 빈 접근: @
	  - 예) ${@helloBean.hello('Spring!')}
```

### 유틸리티 객체와 날짜 
```
  타임리프는 문자, 숫자, 날짜, URI등을 편리하게 다루는 다양한 유틸리티 객체들을 제공한다. 
  
  타임리프 유틸리티 객체 
    - #message: 메시지, 국제화 처리 
	- #uris: URI 이스케이프 지원 
	- #dates: java.util.Date 서식 지원 
	- #calendars: java.util.Calendar 서식 지원 
	- #temporals: 자바8 날짜 서식 지원 
	- #numbers: 숫자 서식 지원 
	- #strings: 문자 관련 편의 기능 
	- #objects: 객체 관련 기능 제공 
	- #bools: boolean 관련 기능 제공 
	- #arrays: 배열 관련 기능 제공 
	- #lists, #sets, #maps: 컬렉션 관련 기능 제공 
	- #ids: 아이디 처리 관련 기능 제공, 뒤에서 설명 

타임리프 유틸리티 객체
https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#expression-utility-objects
유틸리티 객체 예시
https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#appendix-b-expression-utility-objects
  
  참고 
    - 이런 유틸리티 객체들은 대략 이런 것이 있다 알아두고, 필요할 때 찾아서 사용하면 된다. 
	
  자바8 날짜 
    - 타임리프에서 자바8 날짜인 LocalDate, LocalDateTiem, Instant를 사용하려면 
	  추가 라이브러리가 필요하다. 스프링 부트 타임리프를 사용하면 해당 라이브러리가 자동으로 
	  추가되고 통합된다. 
	
	- 타임리프 자바8 날짜 지원 라이브러리
	  - thymeleaf-extras-java8time
	
	- 자바8 날짜용 유틸리티 객체 
	  - #temporals
	
	- 사용 예시 
	  - <span th:text="${#temporals.format(localDateTime, 'yyyy-MM-dd HH:mm:ss')}"></span>
```

### URL 링크 
```
  타임리프에서 URL을 생성할 때는 @{...} 문법을 사용하면 된다. 
  
  단순한 URL
    - @{/hello} -> /hello
  
  쿼리 파라미터 
    - @{/hello(param1=${param1}, param2=${param2})}
	  - /hello?param1=data1&param2=data2
	  - ()에 있는 부분은 쿼리 파라미터로 처리된다. 

  경로 변수 
    - @{/hello/{param1}/{param2}(param1=${param1}, param2=${param2})}
	  - /hello/data1/data2
	  - URL 경로상에 변수가 있으면 () 부분은 경로 변수로 처리된다. 

  경로 변수 + 쿼리 파라미터 
    - @{/hello/{param1}(param1=${param1}, param2=${param2})}
	  - /hello/data1?param2=data2
	  - 경로 변수와 쿼리 파라미터를 함께 사용할 수 있다. 

  상대경로, 절대경로, 프로토콜 기준을 표현할 수도 있다. 
    - /hello: 절대 경로 
	- hello: 상대 경로 
	참고: https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#link-urls
```

### 리터럴 
```
  Literals
    - 리터럴은 소스 코드상에 고정된 값을 말하는 용어이다. 
	  예를 들어서 다음 코드에서 "Hello"는 문자 리터럴, 10, 20은 숫자 리터럴이다. 
	    String a = "Hello"
		int a = 10 * 20
	
	참고 
	  - 이 내용이 쉬워 보이지만 처음 타임리프를 사용하면 많이 실수하니 잘 보아두자. 
	
	- 타임리프는 다음과 같은 리터럴이 있다. 
	  - 문자: 'hello'
	  - 숫자: 10
	  - 불린: true, false
	  - null: null
	
	- 타임리프에서 문자 리터럴은 항상 '(작은 따옴표)로 감싸야 한다. 
	  - <span th:text="'hello'">
	  - 그런데 문자를 항상 '로 감싸는 것은 너무 귀찮은 일이다. 공백 없이 쭉 이어진다면 
	    하나의 의미있는 토큰으로 인지해서 다음과 같이 작은 따옴표를 생략할 수 있다. 
		- 룰: A-Z, a-z, 0-9, [], . , - , _
		  - <span th:text="hello">
	
	오류 
	  - <span th:text="hello world!"></span>
	  - 문자 리터럴은 원칙상 '로 감싸야 한다. 중간에 공백이 있어서 하나의 의미있는 토큰으로도 
	    인식되지 않는다. 
	
	수정 
	  - <span th:text="'hello world!'"></span>
	  - 이렇게 '로 감싸면 정상 동작한다.
	
	리터럴 대체(Literals substitutions)
	  - <span th:text="|hello ${data}|">
	    - 마지막의 리터럴 대체 문법을 사용하면 마치 템플릿을 사용하는 것 처럼 편리하다.
```

### 연산 
```
  타임리프 연산은 자바와 크게 다르지 않다. HTML 안에서 사용하기 때문에 HTML 엔티티를 사용하는 
  부분만 주의하자. 
    - 비교 연산: HTML 엔티티를 사용해야 하는 부분을 주의하자. 
	  - >(gt), <(lt), >=(ge), <=(le), !(not), ==(eq), !=(neq,ne)
	- 조건식: 자바의 조건식과 유사하다.
	- Elvis 연산자: 조건식의 편의 버전 
	- No-Operation: _인 경우 마치 타임리프가 실행되지 않는 것 처럼 동작한다. 
	  이것을 잘 사용하면 HTML의 내용 그대로 활용할 수 있다. 마지막 예를 보면 데이터가 
	  없습니다. 부분이 그대로 출력된다.
```

### 속성 값 설정 
```
  타임리프 태그 속성(Attribute)
    - 타임리프는 주로 HTML 태그에 th:* 속성을 지정하는 방식으로 동작한다. th:*로 
	  속성을 적용하면 기존 속성을 대체한다. 기존 속성이 없으면 새로 만든다.
	
	- 속성 설정
	  - th:* 속성을 지정하면 타임리프는 기존 속성을 th:*로 지정한 속성으로 대체한다. 
	    기존 속성이 없다면 새로 만든다. 
		- <input type="text" name="mock" th:name="userA"/>
		  -> 타임리프 렌더링 후 <input type="text" name="userA"/>
	
	- 속성 추가 
	  - th:attrappend: 속성 값의 뒤에 값을 추가한다.
	  - th:attrprepend: 속성 값의 앞에 값을 추가한다.
	  - th:classappend: class 속성에 자연스럽게 추가한다. 
	  
	- checked 처리 
	  - HTML 에서는 <input type="checkbox" name="active" checked="false" /> 
	    -> 이 경우에도 checked 속성이 있기 때문에 checked 처리가 되어버린다. 
	  - HTML에서 checked 속성은 checked 속성의 값과 상관없이 checked라는 속성만 
	    있어도 체크가 된다. 이런 부분이 true, false 값을 주로 사용하는 개발자 입장에서는 불편한다.
	  - 타임리프의 th:checked는 값이 false인 경우 checked 속성 자체를 제거한다. 
	    <input type="checkbox" name="active" th:checked="false" />
		-> 타임리프 렌더링 후 <input type="checkbox" name="active" />
```

### 반복 
```
  타임리프에서 반복은 th:each를 사용한다. 추가로 반복해서 사용할 수 있는 여러 상태 값을 지원한다.
    - 반복 기능 
	  - <tr th:each="user : ${users}">
	    - 반복시 오른쪽 컬렉션(${users})의 값을 하나씩 꺼내서 왼쪽 변수(user)에 담아서 
		  태그를 반복 실행합니다. 
		- th:each는 List 뿐만 아니라 배열, java.util.Iterable, 
		  java.util.Enumeration을 구현한 모든 객체를 반복에 사용할 수 있습니다. 
		  Map도 사용할 수 있는데 이 경우 변수에 담기는 값은 Map.Entry입니다. 
	
	- 반복 상태 유지 
	  - <tr th:each="user, userStat: ${users}">
	    - 반복의 두번째 파라미터를 설정해서 반복의 상태를 확인 할 수 있습니다. 
		  두번째 파라미터는 생략 가능한데, 생략하면 지정한 변수명(user) + Stat가 됩니다.
		  여기서는 user + Stat = userState 이므로 생략 가능합니다. 
	
	- 반복 상태 유지 기능 
	  - index: 0부터 시작하는 값 
	  - count: 1부터 시작하는 값 
	  - size: 전체 사이즈 
	  - even, odd: 홀수, 짝수 여부(boolean)
	  - first, last: 처음, 마지막 여부(boolean)
	  - current: 현재 객체 
```

### 조건부 평가 
```
  타임리프의 조건식 if, unless(if의 반대)
  
  if, unless 
    - 타임리프는 해당 조건이 맞지 않으면 태그 자체를 렌더링하지 않는다. 
	  만약 다음 조건이 false인 경우 <span>...</span>부분 자체가 렌더링 되지 않고 사라진다. 
	    - <span th:text="'미성년자'" th:if="${user.age lt 20}"></span>
		
  switch 
    - *은 만족하는 조건이 없을 때 사용하는 디폴트이다.
```

### 주석 
```
  1. 표준 HTML 주석 
    - 자바스크립트의 표준 HTML 주석은 타임리프가 랜더링 하지 않고, 그대로 남겨둔다. 
  2. 타임리프 파서 주석 
    - 타임리프 파서 주석은 타임리프의 진짜 주석이다. 렌더링에서 주석 부분을 제거한다. 
  3. 타임리프 프로토타입 주석 
    - 타임리프 프로토타입은 약간 특이한데, HTML 주석에 약간의 구문을 더했다. 
	  HTML 파일을 웹 브라우저에서 그대로 열어보면 HTML 주석이기 때문에 이 부분이 
	  웹 브라우저가 렌더링하지 않는다. 
	  타임리프 렌더링을 거치면 이 부분이 정상 렌더링 된다ㅏ. 
	  쉽게 이야기해서 HTML 파일을 그대로 열어보면 주석 처리가 되지만, 타임리프를 
	  랜더링 한 경우에만 보이는 기능이다.
```

### 블록 
```
  <th:block>은 HTML 태그가 아닌 타임리프의 유일한 자체 태그다.
    - 타임리프 특성상 HTML 태그안에 속성으로 기능을 정의해서 사용하는데, 위 예처럼 
	  이렇게 사용하기 애매한 경우에 사용하면 된다. <th:block>은 렌더링시 제거된다.
```

### 자바스크립트 인라인 
```
  타임리프는 자바스크립트에서 타임리프를 편리하게 사용할 수 있는 자바스크립트 인라인
  기능을 제공한다. 자바스크립트 인라인 기능은 다음과 같이 적용하면 된다. 
  <script th:inline="javascript">
  
  자바스크립트 인라인을 사용하지 않은 경우 어떤 문제들이 있는지 알아보고, 인라인을 
  사용하면 해당 문제들이 어떻게 해결되는지 확인해보자. 
  
  텍스트 렌더링 
    - var username = [[${user.username}]];
	  - 인라인 사용 전 -> var username = userA;
	  - 인라인 사용 후 -> var username = "userA";
	  
	- 인라인 사용 전 렌더링 결과를 보면 userA라는 변수 이름이 그대로 남아있다. 
	  타임리프 입장에서는 정확하게 렌더링 한 것이지만 아마 개발자가 기대한 것은 
	  다음과 같은 "userA"라는 문자일 것이다. 결과적으로 userA가 변수명으로 
	  사용되어서 자바스크립트 오류가 발생한다. 다음으로 나오는 숫자 age의 
	  경우에는 "가 필요 없기 때문에 정상 렌더링 된다. 
	- 인라인 사용 후 렌더링 결과를 보면 문자 타입인 경우 "를 포함해준다. 추가로 
	  자바스크립트에서 문제가 될 수 있는 문자가 포함되어 있으면 이스케이프 처리도 해준다.
	  - 예) " -> \"

  자바스크립트 내추럴 템플릿 
    - 타임리프는 HTML 파일을 직접 열어도 동작하는 내추럴 템플릿 기능을 제공한다. 
	  자바스크립트인 인라인 기능을 사용하면 주석을 활용해서 이 기능을 사용할 수 있다. 
	
	  - var username2 = /*[[${user.username}]]*/ "test username";
	    - 안라인 사용 전 -> var username2 = /*userA*/ "test username";
		- 인라인 사용 후 -> var username2 = "userA";
	  - 인라인 사용 전 결과를 보면 정말 순수하게 그대로 해석해 버렸다. 따라서 내추럴 템플릿 
	    기능이 동작하지 않고, 심지어 렌더링 내용이 주석처리 되어 버린다. 
	  - 인라인 사용 후 결과를 보면 주석 부분이 제거되고, 기대한 "userA"가 정확하게 적용된다.
	
  객체 
    - 타임리프의 자바스크립트 인라인 기능을 사용하면 객체를 JSON으로 자동으로 변환해준다.
	  - var user = [[${user}]];
	    - 인라인 사용 전 -> var user = BasicController.User(username=userA, age=10);
		- 인라인 사용 후 -> var user = {"username": "userA", "age":10};
	
	  - 인라인 사용 전은 객체의 toString()이 호출된 값이다. 
	  - 인라인 사용 후는 객체의 JSON으로 변환해준다.
  
  자바스크립트 인라인 each 
    - 자바스크립트 인라인은 each를 지원한다.
```

### 템플릿 조각 
```
  웹 페이지를 개발할 때는 공통 영역이 많이 있다. 예를 들어서 상단 영역이나 하단 여역, 좌측 카테고리 등등 
  여러 페이지에서 함께 사용하는 영역들이 있다. 이런 부분을 코드를 복사해서 사용한다면 변경시 여러 
  페이지를 다 수정해야 하므로 상당히 비효율 적이다. 타임리프는 이런 문제를 해결하기 위해 템플릿 조각과 
  레이아웃 기능을 지원한다.
  
  주의! 템플릿 조각과 레이아웃 부분은 직접 실행해보아야 이해된다.
  
  템플릿 조각 
    - th:fragment가 있는 태그는 다른곳에 포함되는 코드 조각으로 이해하면 된다.
	- template/fragment/footer :: copy 
	  - template/fragment/footer.html 템플릿에 있는 th:fragment="copy"라는 
	    부분을 템플릿 조각으로 가져와서 사용한다는 의미이다. 
	
	- 부분 포함 insert 
	  - <div th:insert="~{template/fragment/footer :: copy}"></div>
	  - th:insert를 사용하면 현재 태그(div) 내부에 추가한다. 
	
	- 부분 포함 replace 
	  - <div th:replace="~{template/fragment/footer :: copy}"></div>
	  - th:replace를 사용하면 현재 태그(div)를 대체한다. 
	
	- 부분 포함 단순 표현식 
	  - <div th:replace="template/fragment/footer :: copy"></div>
	  - ~{...}를 사용하는 것이 원칙이지만 템플릿 조각을 사용하는 코드가 단순하면 이 부분을 
	    생략할 수 있다. 
	
	- 파라미터 사용 
	  - 다음과 같이 파라미터를 전달해서 동적으로 조각을 렌더링 할 수도 있다. 
	  - <div th:replace="~{template/fragment/footer :: copyParam ('데이터1','데이터2')}"
```

### 템플릿 레이아웃1 
```
  템플릿 레이아웃
    - 이전에는 일부 코드 조각을 가지고와서 사용했다면, 이번에는 개념을 더 확장해서 코드 조각을 
	  레이아웃에 넘겨서 사용하는 방법에 대해서 알아보자. 
	- 예를 들어서 <head>에 공통으로 사용하는 css, javascript 같은 정보들이 있는데, 
	  이러한 공통 정보들을 한 곳에 모아두고, 공통으로 사용하지만, 각 페이지마다 필요한 정보를 
	  더 추가해서 사용하고 싶다면 다음과 같이 사용하면 된다. 
	
	- common_header(~(::title),~(::link)) 이 부분이 핵심이다. 
	  - ::title은 현재 페이지의 title 태그들을 전달한다. 
	  - ::link는 현재 페이지의 link 태그들을 전달한다.
	
	결과를 보자 
	  - 메인 타이틀이 전달한 부분으로 교체되었다. 
	  - 공통 부분은 그대로 유지되고, 추가 부분에 전달한 <link>들이 포함된 것을 확인할 수 있다. 
	
	- 이 방식은 사실 앞서 배운 코드 조각을 조금 더 적극적으로 사용하는 방식이다. 쉽게 이야기해서 
	  레이아웃 개념을 두고, 그 레이아웃에 필요한 코드 조각을 전달해서 완성하는 것으로 이해하면 된다. 
```

### 템플릿 레이아웃2
```
  템플릿 레이아웃 확장 
    - 앞서 이야기한 개념을 <head> 정도에만 적용하는게 아니라 <html> 전체에 적용할 수도 있다. 
	- layoutFile.html을 보면 기본 레이아웃을 가지고 있는데, <html>에 th:fragment 
	  속성이 정의되어 있다. 이 레이아웃 파일을 기본으로 하고 여기에 필요한 내용을 전달해서 
	  부분부분 변경하는 것으로 이해하면 된다. 
	- layoutExtendMain.html은 현재 페이지인데, <html> 자체를 th:replace를 
	  사용해서 변경하는 것을 확인할 수 있다. 결국 layoutFile.html에 필요한 내용을 
	  전달하면서 <html> 자체를 layoutFile.html로 변경한다. 
```

## 타임리프 - 스프링 통합과 폼

### 타임리프 스프링 통합 
```
  타임리프는 크게 2가지 메뉴얼을 제공한다. 
    - 기본 메뉴얼 
	- 스프링 통합 메뉴얼 

  타임리프는 스프링 없이도 동작하지만, 스프링과 통합을 위한 다양한 기능을 편리하게 제공한다. 
  그리고 이런 부분은 스프링으로 백엔드를 개발하는 개발자 입장에서 타임리프를 선택하는 
  하나의 이유가 된다. 
  
  스프링 통합으로 추가되는 기능들
    - 스프링의 SpringEL 문법 통합 
	- ${@myBean.doSomething()} 처럼 스프링 빈 호출 지원
	- 편리한 폼 관리를 위한 추가 속성 
	  - th:object(기능 강화, 폼 커맨드 객체 선택) 
	  - th:field, th:errors, th:errorclass
	- 폼 컴포넌트 기능 
	  - checkbox, radio, button, List 등을 편리하게 사용할 수 있는 기능 지원 
	- 스프링의 메시지, 국제화 기능의 편리한 통합 
	- 스프링의 검증, 오류 처리 통합 
	- 스프링의 변환 서비스 통합(ConversionService)

  설정 방법 
    - 타임리프 템플릿 엔진을 스프링 빈에 등록하고, 타임리브용 뷰 리졸버를 스프링 빈으로 등록하는 방법 
	- https://www.thymeleaf.org/doc/tutorials/3.0/thymeleafspring.html#the-springstandard-dialect
	- https://www.thymeleaf.org/doc/tutorials/3.0/thymeleafspring.html#views-and-view-resolvers
	
	- 스프링 부트는 이런 부분을 모두 자동화 해준다. build.gradle에 다음 한줄을 넣어주면 Gradle은 
	  타임리프와 관련된 라이브러리를 다운로드 받고, 스프링 부트는 앞서 설명한 타임리프와 관련된 설정용 
	  스프링 빈을 자동으로 등록해준다. 
	  - implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
	- 타임리프 관련 설정을 변경하고 싶으면 다음을 참고해서 application.properties에 추가하면 된다. 
	  - 스프링 부트가 제공하는 타임리프 설정, thymeleaf 검색 필요
	  - https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties.templating
```

### 입력 폼 처리 
```
  지금부터 타임리프가 제공하는 입력 폼 기능을 적용해서 기존 프로젝트의 폼 코드를 타임리프가 지원하는 
  기능을 사용해서 효율적으로 개선해보자.
    - th:object: 커맨드 객체를 지정한다. 
	- *{...}: 선택 변수 식이라고 한다. th:object에서 선택한 객체에 접근한다. 
	- th:field
	  - HTML 태그의 id,name,value 속성을 자동으로 처리해준다. 
	
	- 렌더링 전
	  - <input type="text" th:field="*{itemName}" />
	- 렌더링 후 
	  - <input type="text" id="itemName" name="itemName" th:value="*{itemName}" />

  등록 폼 
    - th:object를 적용하려면 먼저 해당 오브젝트 정보를 넘겨주어야 한다. 등록 폼이기 때문에 
	  데이터가 비어있는 빈 오브젝트를 만들어서 뷰에 전달하자. 
	
	- form/addForm.html 변경 코드 부분
	  - th:object="${item}" 
	    - <form>에서 사용할 객체를 지정한다. 선택 변수 식 *{...}을 적용할 수 있다. 
	  - th:field="*{itemName}"
	    - *{itemName}는 선택 변수 식을 사용했는데, ${item.itemName}과 같다. 
		  앞서 th:object로 item을 선택했기 때문에 선택 변수 식을 적용할 수 있다. 
		- th:field는 id, name, value 속성을 모두 자동으로 만들어준다.
		  - id: th:field에서 지정한 변수 이름과 같다. id="itemName"
		  - name: th:field에서 지정한 변수 이름과 같다. name="itemName"
		  - value: th:field에서 지정한 변수의 값을 사용한다. value=""
		참고로 해당 예제에서 id 속성을 제거해도 th:field가 자동으로 만들어준다.

  수정 폼 
    - 수정 폼은 앞서 설명한 내용과 같다. 수정 폼의 경우 id, name, value를 모두 
	  신경써야 했는데, 많은 부분이 th:field 덕분에 자동으로 처리되는 것을 
	  확인할 수 있다. 

  정리 
    - th:object, th:field 덕분에 폼을 개발할 때 약간의 편리함을 얻었다. 
	  쉽고 단순해서 크게 어려움이 없었을 것이다. 
	  사실 이것의 진짜 위력은 뒤에 설명할 검증(Validation)에서 나타난다. 
	  이후 검증 부분에서 폼 처리와 관련된 부분을 더 깊이있게 알아보자. 
```

### 요구사항 추가 
```
  타임리프를 사용해서 폼에서 체크박스, 라디오 버튼, 셀렉트 박스를 편리하게 사용하는 방법을 학습해보자.
  기존 상품 서비스에 다음 요구사항이 추가되었다. 
    - 판매 여부 
	  - 판매 오픈 여부 
	  - 체크 박스로 선택할 수 있다. 
	- 등록 지역 
	  - 서울, 부산, 제주 
	  - 체크 박스로 다중 선택할 수 있다. 
	- 상품 종류 
	  - 도서, 식품, 기타 
	  - 라디오 버튼으로 하나만 선택할 수 있다. 
	- 배송 방식 
	  - 빠른 배송 
	  - 일반 배송 
	  - 느린 배송 
	  - 셀렉트 박스로 하나만 선택할 수 있다. 

  ItemType - 상품 종류
    - 상품 종류는 ENUM을 사용한다. 설명을 위해 description 필드를 추가했다.

  DeliveryCode - 배송 방식 
    - 배송 방식은 DeliveryCode라는 클래스를 사용한다. code는 FAST 같은 시스템에서 
	  전달하는 값이고, displayName은 빠른 배송 같은 고객에게 보여주는 값이다. 

  Item - 상품
    - ENUM, 클래스, String 같은 다양한 상황을 준비했다. 각각의 상황에 어떻게 폼의 
	  데이터를 받을 수 있는지 하나씩 알아보자.
```

### 체크박스 - 단일1 
```
  단순 HTML 체크 박스 
    - 상품이 등록되는 곳에 로그를 남겨서 값이 잘 넘어 오는지 확인해보자. 
  
  FormItemController 추가 
    - FormItemController에 @Slf4j 애노테이션 추가 
	- 체크박스를 체크하면 HTML Form에서 open=on 이라는 값이 넘어간다. 
	  스프링은 on이라는 문자를 true 타입으로 변환해준다.(스프링 타입 컨버터가 
	  이 기능을 수행하는데, 뒤에서 설명한다.)
	
	주의 - 체크 박스를 선택하지 않을 때 
	  - HTML에서 체크 박스를 선택하지 않고 폼을 전송하면 open이라는 
	    필드 자체가 서버로 전송되지 않는다. 

  HTTP 요청 메시지 로깅 
    - HTTP 요청 메시지를 서버에서 보고 싶으면 다음 설정을 추가하면 된다. 
	  - application.properties
	    - logging.level.org.apache.coyote.http11=debug
	- HTTP 메시지 바디를 보면 open의 이름도 전송이 되지 않는 것을 확인할 수 있다. 
	- 서버에서 Boolean 타입을 찍어보면 결과가 null인 것을 확인할 수 있다. 
	  - log.info("item.open={}", item.getOpen());
	
	- HTML checkbox는 선택이 안되면 클라이언트에서 서버로 값 자체를 보내지 않는다. 
	  수정의 경우에는 상황에 따라서 이 방식이 문제가 될 수 있다. 사용자가 의도적으로 
	  체크되어 있던 값을 체크를 해제해도 저장시 아무 값도 넘어가지 않기 때문에, 서버 
	  구현에 따라서 값이 오지 않은 것으로 판단해서 값을 변경하지 않을 수도 있다. 
	- 이런 문제를 해결하기 위해서 스프링 MVC는 약간의 트릭을 사용하는데, 히든 필드를 
	  하나 만들어서, _open처럼 기존 체크박스 이름 앞에 언더스코어(_)를 붙여서 
	  전송하면 체크를 해제했다고 인식할 수 있다. 히든 필드는 항상 전송된다. 따라서 
	  체크를 해제한 경우 여기에서 open은 전송되지 않고, _open만 전송되는데 
	  이 경우 스프링 MVC는 체크를 해제했다고 판단한다. 

  체크 해제를 인식하기 위한 히든 필드 
    - <input type="hidden" name="_open" value="on" />

  체크 박스 체크 
    - open=on&_opne=on 
	  - 체크 박스를 체크하면 스프링 MVC가 open에 값이 있는 것을 확인하고 사용한다. 
	    이때 _open은 무시한다. 
  체크 박스 미체크 
    - _open=on
	  - 체크 박스를 체크하지 않으면 스프링 MVC가 _open만 있는 것을 확인하고, 
	    open의 값이 체크되지 않았다고 인식한다. 이 경우 서버에서 Boolean 
		타입을 찍어보면 결과가 null이 아니라 false인 것을 확인할 수 있다. 
		log.info("item.open={}", item.getOpen());
```

### 체크박스 - 단일2 
```
  타임리프 
    - 개발할 때 마다 이렇게 히든 필드를 추가하는 것은 상당히 번거롭다. 타임리프가 제공하는 
	  폼 기능을 사용하면 이런 부분을 자동으로 처리할 수 있다. 
	
  타임리프 - 체크 박스 코드 추가 
    - 체크 박스의 기존 코드를 제거하고 타임리프가 제공하는 체크 박스 코드로 변경하자. 

  타임리프 체크 박스 HTML 생성 결과 
    - <input type="hidden" name="_open" value="on" /> 
	  - 타임리프를 사용하면 체크 박스의 히든 필드와 관련된 부분도 함께 해결해준다. 
	    HTML 생성 결과를 보면 히든 필드 부분이 자동으로 생성되어 있다. 

  상품 상세에 적용하자. 
    - item.html 
	  주의 
	    - item.html에는 th:object를 사용하지 않았기 때문에 th:field 부분에 
		  ${item.open}으로 적어주어야 한다. 
		- disabled를 사용해서 상품 상세에는 체크 박스가 선택되지 않도록 했다. 
	  
	  - HTML 생성 결과 
	    - 타임리프의 체크 확인 (checked="checked")
		  - 체크 박스에서 판매 여부를 선택해서 저장하면, 조회시에 checked 속성이 
		    추가된 것을 확인할 수 있다. 이런 부분을 개발자가 직접 처리하려면 상당히 
			번거롭다. 타임리프의 th:field를 사용하면, 값이 true인 경우 
			체크를 자동으로 처리해준다. 

  상품 수정에도 적용하자. 
    - editForm.html
	  - 상품 수정도 th:object, th:field를 모두 적용해야 한다. 
	  - 실행해보면 체크 박스를 수정해도 반영되지 않는다. 실제 반영되도록 코드를 수정하자. 
	    - ItemRepository - update() 코드 수정 
```

### 체크 박스 - 멀티 
```
  체크 박스를 멀티로 사용해서, 하나 이상을 체크할 수 있도록 해보자. 
    - 등록 지역 
	  - 서울, 부산, 제주 
	  - 체크 박스로 다중 선택할 수 있다. 
	
	FormItemController - 추가 
	  - @ModelAttribute의 특별한 사용법 
	    - 등록 폼, 상세화면, 수정 폼에서 모두 서울, 부산, 제주라는 체크 박스를 
		  반복해서 보여주어야 한다. 이렇게 하려면 각각의 컨트롤러에서 model.addAttribute(...)을 
		  사용해서 체크 박스를 구성하는 데이터를 반복해서 넣어주어야 한다. 
		  @ModelAttribute는 이렇게 컨트롤러에 있는 별도의 메서드에 적용할 수 있다. 
		  이렇게 하면 해당 컨트롤러를 요청할 때 regions에서 반환한 값이 자동으로 모델(model)에 
		  담기게 된다. 물론 이렇게 사용하지 않고, 각각의 컨트롤러 메서드에서 모델에 직접 
		  데이터를 담아서 처리해도 된다. 
		  
	addForm.html - 추가
	  - th:for="${#ids.prev('regions')}"
	    - 멀티 체크박스는 같은 이름의 여러 체크박스를 만들 수 있다. 그런데 문제는 이렇게 
		  반복해서 HTML 태그를 생성할 때, 생성된 HTML 태그 속성에서 name은 같아도 
		  되지만 id는 모두 달라야 한다. 따라서 타임리프는 체크박스를 each 루프 안에서 
		  반복해서 만들 때 임의로 1,2,3 숫자를 뒤에 붙여준다. 
	
	  - each로 체크박스가 반복 생성된 결과 - id 뒤에 숫자가 추가 
	    - HTML의 id가 타임리프에 의해 동적으로 만들어지기 때문에 <label for="id 값">으로 
		  label의 대상이 되는 id 값을 임의로 지정하는 것은 곤란하다. 타임리프는 
		  ids.prev(...), ids.next(...)을 제공해서 동적으로 생성되는
		  id 값을 사용할 수 있도록 한다.
	  
	  - 타임리프 HTML 생성 결과
	    - <label for="id 값">에 지정된 id가 checkbox에서 동적으로 생성된
		  regions1, regions2,regions3에 맞추어 순서대로 입력된 것을 
		  확인할 수 있다. 
	  - 로그 출력 
	    - _regions는 앞서 설명한 기능이다. 웹 브라우저에서 체크를 하나도 하지 
		  않았을 때, 클라이언트가 서버에 아무런 데이터를 보내지 않는 것을 방지한다. 
		  참고로 _regions 조차 보내지 않으면 결과는 null이 된다. _regions가 
		  체크박스 숫자만큼 생성될 필요는 없지만, 타임리프가 생성되는 옵션 수 만큼 
		  생성해서 그런 것이니 무시하자. 
	
	item.html - 추가
	  - 주의 
	    - item.html에는 th:object를 사용하지 않았기 때문에 th:field 부분에 
		  ${item.regions}으로 적어주어야 한다. 
		  disabled를 사용해서 상품 상세에서는 체크 박스가 선택되지 않도록 했다. 
	
	  - 타임리프의 체크 확인 
	    - 멀티 체크 박스에서 등록 지역을 선택해서 저장하면, 조회시에 checked 속성이 
		  추가된 것을 확인할 수 있다. 
		  타임리프는 th:field에 지정한 값과 th:value의 값을 비교해서 
		  체크를 자동으로 처리해준다. 
	
	editForm.html - 추가 
```

### 라디오 버튼 
```
  라디오 버튼은 여러 선택지 중에 하나를 선택할 때 사용할 수 있다. 이번 시간에는 라디오 버튼을 
  자바 ENUM을 활용해서 개발해보자. 
    - 상품 종류 
	  - 도서, 식품, 기타 
	  - 라디오 버튼으로 하나만 선택할 수 있다. 
	
	FormItemController - 추가 
	  - itemTypes를 등록 폼, 조회, 수정 폼에서 모두 사용하므로 @ModelAttribute의 
	    특별한 사용법을 적용하자. 
	  - ItemType.values()를 사용하면 해당 ENUM의 모든 정보를 배열로 반환한다.
	    예) [BOOK, FOOD, ETC]
	
	상품 등록 폼에 기능을 추가해보자. 
	addForm.html - 추가 
	  - 체크 박스는 수정시 체크를 해제하면 아무 값도 넘어가지 않기 때문에, 별도의 히든 필드로 
	    이런 문제를 해결했다. 라디오 버튼은 이미 선택이 되어 있다면, 수정시에도 항상 하나를 
		선택하도록 되어 있으므로 체크 박스와 달리 별도의 히든 필드를 사용할 필요가 없다. 
	
	상품 상세와 수정에도 라디오 버튼을 넣어주자. 
	item.html
	  - 주의 
	    - item.html에는 th:object를 사용하지 않았기 때문에 th:field 부분에 
		  ${item.itemType}으로 적어주어야 한다. 
		  disabled를 사용해서 상품 상세에서는 라디오 버튼이 선택되지 않도록 했다.
		  
	edit.html 
	  - 타임리프로 생성된 HTML 
	    - 선택한 식품(FOOD)에 checked="checked"가 적용된 것을 확인할 수 있다. 
	
	타임리프에서 ENUM 직접 사용하기 
	  - 이렇게 모델에 ENUM을 담아서 전달하는 대신에 타임리프는 자바 객체에 
	    직접 접근할 수 있다. 
	  - 타임리프에서 ENUM  직접 접근 
	    - <div th:each="type : ${T(hello.itemservice.domain.item.ItemType).values()}"
		- ${T(hello.itemservice.domain.item.ItemType).values()} 스프링EL 문법으로 
		  ENUM을 직접 사용할 수 있다. ENUM에 values()를 호출하면 해당 ENUM의 
		  모든 정보가 배열로 반환된다. 
		- 그런데 이렇게 사용하면 ENUM의 패키지 위치가 변경되거나 할 때 자바 컴파일러가 타임리프까지 
		  컴파일 오류를 잡을 수 없으므로 추천하지는 않는다.
```

### 셀렉트 박스 
```
  셀렉트 박스는 여러 선택지 중에 하나를 선택할 때 사용할 수 있다. 이번시간에는 셀렉트 박스를 
  자바 객체를 활용해서 개발해보자. 
    - 배송 방식 
	  - 빠른 배송 
	  - 일반 배송 
	  - 느린 배송 
	  - 셀렉트 박스로 하나만 선택할 수 있다. 

  FormItemController - 추가 
    - DeliveryCode라는 자바 객체를 사용하는 방법으로 진행하겠다. 
	  DeliveryCode를 등록 폼, 조회, 수정 폼에서 모두 사용하므로 @ModelAttribute의 
	  특별한 사용법을 적용하자. 
	- 참고 
	  - @ModelAttribute가 있는 deliveryCodes() 메서드는 컨트롤러가 호출 될 때 
	    마다 사용되므로 deliveryCodes 객체도 계속 생성된다. 이런 부분은 미리 생성해두고 
		재사용하는 것이 더 효율적이다.

  addForm.html - 추가 
  
  item.html - 추가 
    - 주의
	    - item.html에는 th:object를 사용하지 않았기 때문에 th:field부분에
		  ${item.deliveryCode}으로 적어주어야 한다. 
		  disabled를 사용해서 상품 상세에서는 셀렉트 박스가 선택되지 않도록 했다. 

  editForm.html 
    - selected="selected
	  - 빠른 배송을 선택한 예시인데, 선택된 셀렉트 박스가 유지되는 것을 확인할 수 있다. 
```

## 메시지, 국제화 

### 메시지, 국제화 소개 
```
  메시지 
    - 악덕? 기획자가 화면에 보이는 문구가 마음에 들지 않는다고, 상품명이라는 단어를 모두 
	  상품이름으로 고쳐달라고 하면 어떻게 해야할까?
	- 여러 화면에 보이는 상품명, 가격, 수량 등, label에 있는 단어를 변경하려면 
	  다음 화면들을 다 찾아가면서 모두 변경해야 한다. 지금처럼 화면 수가 적으면 
	  문제가 되지 않지만 화면이 수십개 이상이라면 수십개의 파일을 모두 고쳐야 한다. 
	  - addForm.html, editForm.html, item.html, items.html
	- 왜냐하면 해당 HTML 파일에 메시지가 하드코딩 되어 있기 때문이다. 
	- 이런 다양한 메시지를 한 곳에서 관리하도록 하는 기능을 메시지 기능이라 한다. 
	  예를 들어서 messages.properties라는 메시지 관리용 파일을 만들고 
	    item=상품
		item.id=상품 ID
		item.itemName=상품명
		item.price=가격
		item.quantity=수량
	  각 HTML들은 다음과 같이 해당 데이터를 key 값으로 불러서 사용하는 것이다. 
	
	- addForm.html 
	  - <label for="itemName" th:text="#{item.itemName}"></label>
	- editForm.html 
	  - <label for="itemName" th:text="#{item.itemName}"></label>

  국제화 
    - 메시지에서 한 발 더 나가보자. 
	  메시지에서 설명한 메시지 파일(messages.properties)을 각 나라별로 별도로 관리하면
	  서비스를 국제화 할 수 있다. 
	  예를 들어서 다음과 같이 2개의 파일을 만들어서 분류한다. 
	  - messages_en.properties 
	    item=Item
		item.id=Item ID
		item.itemName=Item Name
		item.price=price
		item.quantity=quantity
	  - messages_ko.properties
	    item=상품
		item.id=상품 ID
		item.itemName=상품명
		item.price=가격
		item.quantity=수량
	- 영어를 사용하는 사람이면 messages_en.properties를 사용하고, 한국어를 사용하는
	  사람이면 messages_ko.properties를 사용하게 개발하면 된다. 
	  이렇게 하면 사이트를 국제화 할 수 있다. 
	- 한국에서 접근한 것인지 영어에서 접근한 것인지 인식하는 방법은 HTTP accept-language
	  헤더 값을 사용하거나 사용자가 직접 언어를 선택하도록 하고, 쿠키 등을 사용해서 처리하면 된다. 
	- 메시지와 국제화 기능을 직접 구현할 수도 있겠지만, 스프링은 기본적인 메시지와 국제화 기능을 
	  모두 제공한다. 그리고 타임리프도 스프링이 제공하는 메시지와 국제화 기능을 편리하게 
	  통합해서 제공한다. 지금부터 스프링이 제공하는 메시지와 국제화 기능을 알아보자.
```

### 스프링 메시지 소스 설정 
```
  스프링은 기본적인 메시지 관리 기능을 제공한다. 
  
  메시지 관리 기능을 사용하려면 스프링이 제공하는 MessageSource를 스프링 빈으로 등록하면 되는데, 
  MessageSource는 인터페이스이다. 따라서 구현체인 ResourceBundleMessageSource를 
  스프링 빈으로 등록하면 된다. 
  
  직접 등록 
    @Bean
	public MessageSource messageSource() {
	 ResourceBundleMessageSource messageSource = new
	ResourceBundleMessageSource();
	 messageSource.setBasenames("messages", "errors");
	 messageSource.setDefaultEncoding("utf-8");
	 return messageSource;
	}
	
    - basenames: 설정 파일의 이름을 지정한다. 
	  - messages로 지정하면 messages.properties 파일을 읽어서 사용한다. 
	  - 추가로 국제화 기능을 적용하려면 messages_en.properties, 
	    messages_ko.properties와 같이 파일명 마지막에 언어 정보를 주면된다. 
		만약 찾을 수 있는 국제화 파일이 없으면 messages.properties
		(언어정보가 없는 파일명)를 기본으로 사용한다.
	  - 파일의 위치는 /resources/messages.properties에 두면 된다. 
	  - 여러 파일을 한번에 지정할 수 있다. 여기서는 messages, errors
	    둘을 지정했다. 
	- defaultEncoding
	  - 인코딩 정보를 지정한다. utf-8을 사용하면 된다.

  스프링 부트 
    - 스프링 부트를 사용하면 스프링 부트가 MessageSource를 자동으로 스프링 빈으로 등록한다. 

  스프링 부트 메시지 소스 설정 
    - 스프링 부트를 사용하면 다음과 같이 메시지 소스를 설정할 수 있다. 
	  - application.properties
	    spring.messages.basename=messages,config.i18n.messages 

  스프링 부트 메시지 소스 기본 값 
    - spring.messages.basename=messages
	
  MessageSource를 스프링 빈으로 등록하지 않고, 스프링 부트와 관련된 별도의 설정을 
  하지 않으면 messages라는 이름으로 기본 등록된다. 따라서 messages_en.properties,
  messages_ko.properties, messages.properties 파일만 등록하면 자동으로 인식된다.
  
  메시지 파일 만들기 
    - 메시지 파일을 만들어보자. 국제화 테스트를 위해서 messages_en 파일도 추가하자. 
	  - messages.properties: 기본 값으로 사용(한글) 
	  - messages_en.properties: 영어 국제화 사용
	  
	  주의! 파일명은 message가 아니라 messages다! 마지막 s에 주의하자.  
```

### 스프링 메시지 소스 사용 
```
  MessageSource 인터페이스 
    - MessageSource 인터페이스를 보면 코드를 포함한 일부 파라미터로 메시지를 
	  읽어오는 기능을 제공한다. 
	- 스프링이 제공하는 메시지 소스를 어떻게 사용하는지 테스트 코드를 통해서 학습해보자.

  test/java/hello/itemservice/message.MessageSourceTest.java
    - ms.getMessage("hello", null, null)
	  - code: hello
	  - args: null
	  - locale: null
	- 가장 단순한 테스트는 메시지 코드로 hello를 입력하고 나머지 값은 null을 입력했다. 
	  locale 정보가 없으면 basename에서 설정한 기본 이름 메시지 파일을 조회한다. 
	  basename으로 messages를 지정 했으므로 messages.properties
	  파일에서 데이터를 조회한다. 

  MessageSourceTest 추가 - 메시지가 없는 경우, 기본 메시지
    - 메시지가 없는 경우에는 NoSuchMessageException이 발생한다. 
	- 메시지가 없어도 기본 메시지(defaultMessage)를 사용하면 기본 메시지가 반환된다. 

  MessageSourceTest 추가 - 매개변수 사용
    - 다음 메시지의 {0} 부분은 매개변수를 전달해서 치환할 수 있다. 
	- hello.name=안녕 {0} -> Spring 단어를 매개변수로 전달 -> 안녕 Spring
	
	- 국제화 파일 선택 
	  - locale 정보를 기반으로 국제화 파일을 선택한다. 
	  - Locale이 en_US의 경우 messages_en_US -> messages_en -> messages 순서로 찾는다. 
	  - Locale에 맞추어 구체적인 것이 있으면 구체적인 것을 찾고, 
	    없으면 디폴트를 찾는다고 이해하면 된다. 

  MessageSourceTest 추가 - 국제화 파일 선택1
    - ms.getMessage("hello", null, null): locale 정보가 없으므로 messages를 사용
	- ms.getMessage("hello", null, Locale.KOREA): locale 정보가 있지만, 
	  messages_ko가 없으므로 messages를 사용 

  MessageSourceTest 추가 - 국제화 파일 선택2
    - ms.getMessage("hello", null, Locale.ENGLISH): locale 정보가 
	  Locale.ENGLISH이므로 messages_en을 찾아서 사용
```

### 웹 애플리케이션에 메시지 적용하기 
```
  실제 웹 애플리케이션에 메시지를 적용해보자. 
  
  먼저 메시지를 추가 등록하자. 
  messages.properties 
    label.item=상품
	label.item.id=상품 ID
	label.item.itemName=상품명
	label.item.price=가격
	label.item.quantity=수량
	
	page.items=상품 목록
	page.item=상품 상세
	page.addItem=상품 등록
	page.updateItem=상품 수정
	
	button.save=저장
	button.cancel=취소

  타임리프 메시지 적용 
    타임리프의 메시지 표현식 #{...}을 사용하면 스프링의 메시지를 편리하게 
	조회할 수 있다. 예를 들어서 방금 등록한 상품이라는 이름을 조회하려면 #{label.item}이라고 
	하면 된다. 
	
	타임리프 템플릿 파일에 메시지를 적용해보자.
	addForm.html
	editForm.html
	item.html
	items.html
	
	페이지 이름에 적용 
	  - <h2>상품 등록 폼</h2>
	    - <h2 th:text="#{page.addItem}">상품 등록</h2>
	
	레이블에 적용 
	  - <label for="itemName">상품명</label>
	    - <label for="itemName" th:text="#{label.item.itemName}">상품명</label>
		- <label for="price" th:text="#{label.item.price}">가격</label>
		- <label for="quantity" th:text="#{label.item.quantity}">수량</label>
	
	버튼에 적용 
	  - <button type="submit">상품 등록</button>
	    - <button type="submit" th:text="#{button.save}">저장</button>
		- <button type="button" th:text="#{button.cancel}"></button>
	
	실행 
	  - 잘 동작하는지 확인하기 위해 messages.properties 파일의 내용을 가격 -> 금액과 
	    같이 변경해서 확인해보자. 정상 동작하면 다시 돌려두자. 
	참고로 파라미터는 다음과 같이 사용할 수 있다. 
	  - hello.name=안녕 {0}
	  - <p th:text="#{hello.name(${item.itemName})}"></p>
	
	정리 
	  - 지금까지 메시지를 효율적으로 관리하는 방법을 알아보았다. 이제 여기에 더해서 국제화를 
	    웹 애플리케이션에 어떻게 적용하는지 알아보자. 
```

### 웹 애플리케이션에 국제화 적용하기 
```
  이번에는 웹 애플리케이션에 국제화를 적용해보자. 먼저 영어 메시지를 추가하자. 
  
  사실상 이것으로 국제화 작업은 거의 끝났다. 앞에서 템플릿 파일에는 모두 #{...}를 통해서 
  메시지를 사용하도록 적용해두었기 때문이다.
  
  웹으로 확인하기 
    - 웹 브라우저의 언어 설정 값을 변경하면서 국제화 적용을 확인해보자. 
	  크롬 브라우저 -> 설정 -> 언어를 검색하고, 우선 순위를 변경하면 된다. 
	  우선순위를 영어로 변겨아고 테스트해보자.
	  웹 브라우저의 언어 설정 값을 변경하면 요청시 Accept-Language의 값이 변경된다. 
	
	- Accept-Language는 클라이언트가 서버에 기대하는 언어 정보를 담아서 요청하는 
	  HTTP 요청 헤더이다. (더 자세한 내용은 모든 개발자를 위한 HTTP 웹 기본지식
	  강의를 참고하자.)
	
  스프링의 국제화 메시지 선택 
    - 앞서 MessageSource테스트에서 보았듯이 메시지 기능은 Locale 정보를 알아야 
	  언어를 선택할 수 있다. 
	- 결국 스프링도 Locale 정보를 알아야 언어를 선택할 수 있는데, 스프링은 언어 선택시 
	  기본으로 Accept-Language 헤더의 값을 사용한다. 
	
	- LocaleResolver
	  - 스프링은 Locale 선택 방식을 변경할 수 있도록 LocaleResolver라는 
	    인터페이스를 제공하는데, 스프링 부트는 기본으로 Accept-Language를 
		활용하는 AcceptHeaderLocaleResolver를 사용한다.
	
	- LocaleResolver 변경 
	  - 만약 Locale 선택 방식을 변경하려면 LocalResolver의 구현체를 
	    변경해서 쿠키나 세션 기반의 Locale 선택 기능을 사용할 수 있다. 
		예를 들어서 고객이 직접 Locale을 선택하도록 하는 것이다. 
		관련해서 LocaleResolver를 검색하면 수 많은 예제가 나오니 
		필요한 분들은 참고하자.
```

## 검증1 - Validation

### 검증 요구사항
```
  상품 관리 시스템에 새로운 요구사항이 추가되었다. 
  
  요구사항: 검증 로직 추가 
    - 타입 검증 
	  - 가격, 수량에 문자가 들어가면 검증 오류 처리 
	- 필드 검즈 
	  - 상품명: 필수, 공백X
	  - 가격: 1000원 이상, 1백만원 이하 
	  - 수량: 최대9999
	- 특정 필드의 범위를 넘어서는 검증 
	  - 가격 * 수량의 합은 10,000원 이상

  지금까지 만든 웹 애플리케이션은 폼 입력시 숫자를 문자로 작성하거나해서 검증 오류가 발생하면 
  오류 화면으로 바로 이동한다. 이렇게 되면 사용자는 처음부터 해당 폼으로 다시 이동해서 
  입력을 해야 한다. 아마도 이런 서비스라면 사용자는 금방 떠나버릴 것이다. 웹 서비스는 폼 
  입력시 오류가 발생하면, 고객이 입력한 데이터를 유지한 상태로 어떤 오류가 발생했는지 
  친절하게 알려주어야 한다. 
  
  컨트롤러의 중요한 역할중 하나는 HTTP 요청이 정상인지 검증하는 것이다. 그리고 정상 로직보다 이런 
  검증 로직을 잘 개발하는 것이 어쩌면 더 어려울 수 있다. 
  
  참고: 클라이언트 검증, 서버 검증
    - 클라이언트 검증은 조작할 수 있으므로 보안에 취약하다. 
	- 서버만으로 검증하면, 즉각적인 고객 사용성이 부족해진다. 
	- 둘을 적절히 섞어서 사용하되, 최종적으로 서버 검증은 필수 
	- API 방식을 사용하면 API 스펙을 잘 정의해서 검증 오류를 API 응답 결과에 
	  잘 남겨주어야 함

  먼저 검증을 직접 구현해보고, 뒤에서 스프링과 타임리프가 제공하는 검증 기능을 활용해보자.
```

### 검증 직접 처리 - 소개 
```
  상품 저장 성공 
    - 사용자가 상품 등록 폼에서 정상 범위의 데이터를 입력하면, 서버에서는 검증 로직이 
	  통과하고, 상품을 저장하고, 상품 상세 화면으로 redirect한다. 

  상품 저장 검증 실패 
    - 고객이 상품 등록 폼에서 상품명을 입력하지 않거나, 가격, 수량 등이 너무 작거나 
	  커서 검증 범위를 넘어서면, 서버 검증 로직이 실패해야 한다. 이렇게 검증에 
	  실패한 경우 고객에게 다시 상품 등록 폼을 보여주고, 어떤 값을 잘못 입력했는지 
	  친절하게 알려주어야 한다. 

  이제 요구사항에 맞추어 검증 로직을 직접 개발해보자.
```

### 검증 직접 처리 - 개발 
```
  상품 등록 검증 
    - 먼저 상품 등록 검증 코드를 작성해보자. 
	
    ValidationItemControllerV1 - addItem() 수정 
	  - 검증 오류 보관 
	    - Map<String, String> errors = new HashMap<>();
		- 만약 검증시 오류가 발생하면 어떤 검증에서 오류가 발생했는지 정보를 담아둔다. 
	  - 검증 로직 
	    - import org.springframework.util.StringUtils; 추가 필요 
	    - 검증시 오류가 발생하면 errors에 담아둔다. 이때 어떤 필드에서 오류가 
		  발생했는지 구분하기 위해 오류가 발생한 필드명을 key로 사용한다. 이후 
		  뷰에서 이 데이터를 사용해서 고객에게 친절한 오류 메시지를 출력할 수 있다. 
	  - 특정 필드의 범위를 넘어서는 검증 로직 
	    - 특정 필드를 넘어서는 오류를 처리해야 할 수도 있다. 이때는 필드 이름을 
		  넣을 수 없으므로 globalError라는 key를 사용한다. 
	  - 검증에 실패하면 다시 입력 폼으로 
	    - 만약 검증에서 오류 메시지가 하나라도 있으면 오류 메시지를 출력하기 위해 
		  model errors를 담고, 입력 폼이 있는 뷰 템플릿으로 보낸다. 
	  - 글로벌 오류 메시지 
	    - 오류 메시지는 errors에 내용이 있을 때만 출력하면 된다. 타임리프의 
		  th:if를 사용하면 조건에 만족할 때만 해당 HTML 태그를 출력할 수 있다. 
	
	참고 Safe Navigation Operator
	  - 만약 여기에서 errors가 null이라면 어떻게 될까?
	    생각해보면 등록폼에 진입한 시점에는 errors가 없다. 
		따라서 errors.containsKey()를 호출하는 순간 NullPointerException이 발생한다. 
		errors?.은 errors가 null일 때 NullPointerException이 발생하는 대신, 
		null을 반환하는 문법이다. 
		th:if에서 null은 실패로 처리되므로 오류 메시지가 출력되지 않는다.
		이것은 스프링의 SpringEL이 제공하는 문법이다. 자세한 내용은 다음을 참고하자. 
		https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#expressions-operator-safe-navigation
	
	  - 필드 오류 처리 
	    - classappend를 사용해서 해당 필드에 오류가 있으면 field-error라는 클래스 
		  정보를 더해서 폼의 색깔을 빨간색으로 강조한다. 만약 값이 없으면 _(No-Operation)을
		  사용해서 아무것도 하지 않는다. 
	  - 필드 오류 처리 - 메시지 
	    - 글로벌 오류 메시지에서 설명한 내용과 동일하고, 필드 오류를 대상으로 한다. 
	
	실행 
	  - 상품 등록을 실행하고 검증이 잘 동작 하는지 확인해보자. 
	  - 상품 수정의 검증은 더 효율적인 검증 처리 방법을 학습한 다음에 진행한다.
	정리 
	  - 만약 검증 오류가 발생하면 입력 폼을 다시 보여준다. 
	  - 검증 오류들을 고객에게 친절하게 안내해서 다시 입력할 수 있게 한다. 
	  - 검증 오류가 발생해도 고객이 입력한 데이터가 유지된다. 
	
	남은 문제점 
	  - 뷰 템플릿에서 중복 처리가 많다. 뭔가 비슷하다. 
	  - 타입 오류 처리가 안된다. Item의 price, quantity 같은 숫자 필드는 
	    타입이 Integer이므로 문자 타입으로 설정하는 것이 불가능하다. 숫자 타입에 
		문자가 들어오면 오류가 발생한다. 그런데 이러한 오류는 스프링MVC에서 
		컨트롤러에 진입하기도 전에 예외가 발생하기 때문에, 컨트롤러가 호출되지도 안고, 
		400 예외가 발생하면서 오류 페이지를 띄워준다. 
	  - Item의 price에 문자를 입력하는 것 처럼 타입 오류가 발생해도 고객이 입력한 
	    문자를 화면에 남겨야 한다. 만약 컨트롤러가 호출된다고 가정해도 Item의 
		price는 Integer이므로 문자를 보관할 수가 없다. 결국 문자는 바인딩이 
		불가능하므로 고객이 입력한 문자가 사라지게 되고, 고객은 본인이 어떤 내용을 
		입력해서 오류가 발생했는지 이해하기 어렵다. 
	  - 결국 고객이 입력한 값도 어딘가에 별도로 관리가 되어야 한다. 
	
	지금부터 스프링이 제공하는 검증 방법을 하나씩 알아보자.
```

### 프로젝트 준비 v2
```
  앞서 만든 기능을 유지하기 위해, 컨트롤러와 템플릿 파일을 복사하자. 
```

### BindingResult1 
```
  지금부터 스프링이 제공하는 검증 오류 처리 방법을 알아보자. 여기서 핵심은 
  BindingResult이다. 우선 코드를 확인해보자.
  
  ValidationItemControllerV2 - addItemV1
    - 코드 변경 
	  - 메서드 이름 변경: addItem() -> addItemV1()
	  - @Slf4j: 로그 출력을 위해 추가 
	  
	  주의 
	    - BindingResult bindingResult 파라미터의 위치는 
		  @ModelAttribute Item item 다음에 와야 한다. 
	
	- 필드 오류 - FieldError
	- FieldError 생성자 요약 
	  - 필드에 오류가 있으면 FieldError 객체를 생성해서 
	    bindingResult에 담아 두면 된다. 
		- objectName: @ModelAttribute 이름 
		- field: 오류가 발생한 필드 이름 
		- defaultMessage: 오류 기본 메시지 
	
	- 글로벌 오류 - ObjectError 
	- ObjectError 생성자 요약
	  - 특정 필드를 넘어서는 오류가 있으면 ObjectError 객체를 생성해서 
	    bindingResult에 담아 두면 된다.
		- objectName: @ModelAttribute 이름 
		- defaultMessage: 오류 기본 메시지

  validation/v2/addForm.html 수정
    - 타임리프 스프링 검즘 오류 통합 기능 
	  - 타임리프는 스프링의 BindingResult를 활용해서 편리하게 검증 오류를 
	    표현하는 기능을 제공한다. 
		- #fields: #fields로 BindingResult가 제공하는 검증 오류에
		  접근할 수 있다. 
		- th:errors: 해당 필드에 오류가 있는 경우에 태그를 출력한다. 
		  th:if의 편의 버전이다. 
		- th:errorclass: th:field에서 지정한 필드에 오류가 있으면 
		  class 정보를 추가한다.
```

### BindingResult2
```
  스프링이 제공하는 검증 오류를 보관하는 객체이다. 검증 오류가 발생하면 여기에 보관하면 된다. 
  BindingResult가 있으면 @ModelAttribute에 데이터 바인딩 시 오류가 발생해도 
  컨트롤러가 호출된다!
    
	- 예) @ModelAttribute에 바인딩 시 타입 오류가 발생하면?
	  - BindingResult가 없으면 -> 400 오류가 발생하면서 컨트롤러가 
	    호출되지 않고, 오류 페이지로 이동한다. 
	  - BindingResult가 있으면 -> 오류 정보(FieldError)를 
	    BindingResult에 담아서 컨트롤러를 정상 호출한다. 
	- BindingResult에 검증 오류를 적용하는 3가지 방법 
	  - @ModelAttribute의 객체에 타입 오류 등으로 바인딩이 실패하는 경우 
	    스프링이 FieldError 생성해서 BindingResult에 넣어준다. 
	  - 개발자가 직접 넣어준다.ㅏ 
	  - Validator 사용 -> 이것은 뒤에서 설명 
	  
	- 타입 오류 확인 
	  - 숫자가 입력되어야 할 곳에 문자를 입력해서 타입을 다르게 해서 BindingResult를 
	    호출하고 bindingResult의 값을 확인해보자. 
	- 주의 
	  - BindingResult는 검증할 대상 바로 다음에 와야한다. 순서가 중요하다. 
	    예를 들어서 @ModelAttribute Item item, 바로 다음에 
		BindingResult가 와야 한다. 
	  - BindingResult는 Model에 자동으로 포함된다. 
	
	- BindingResult와 Errors 
	  - org.springframework.validation.Errors
	  - org.springframework.validation.BindingResult
	  
	  - BindingResult는 인터페이스이고, Errors 인터페이스를 상속받고 있다. 
	    실제 넘어오는 구현체는 BeanPropertyBindingResult 라는 것인데, 
		둘다 구현하고 있으므로 BindingResult 대신에 Errors를 사용해도 된다. 
		Errors 인터페이스는 단순한 오류 저장과 조회 기능을 제공한다. 
		BindingResult는 여기에 더해서 추가적인 기능들을 제공한다. addError()도 
		BindingResult가 제공하므로 여기서는 BindingResult를 사용하자. 
		주로 관례상 BindingResult를 많이 사용한다. 
	
	- 정리 
	  - BindingResult, FieldError, ObjectError를 사용해서 오류 메시지를 
	    처리하는 방법을 알아보았다. 그런데 오류가 발생하는 경우 고객이 입력한 내용이 
		모두 사라진다. 이 문제를 해결해보자. 
```

### FieldError, ObjectError
```
  목표 
    - 사용자 입력 오류 메시지가 화면에 남도록 하자. 
	  - 예)가격을 1000원 미만으로 설정시 입력한 값이 남아있어야 한다. 
    - FieldError, ObjectError에 대해서 더 자세히 알아보자.
  
  ValidationItemControllerV2 - addItemV2
    - 코드변경 
      - addItemV1()의 @PostMapping("/add")을 주석 처리하자.

  FieldError 생성자 
    - FieldError는 두 가지 생성자를 제공한다. 
	  - 파라미터 목록 
	    - objectName: 오류가 발생한 객체 이름 
		- field: 오류 필드 
		- rejectedValue: 사용자가 입력한 값(거절된 값)
		- bindingFailure: 타입 오류 같은 바인딩 실패인지, 검증 실패인지 구분 값 
		- codes: 메시지 코드 
		- arguments: 메시지에서 사용하는 인자 
		- defaultMessage: 기본 오류 메세지 
	  
	  - ObjectError도 유사하게 두 가지 생성자를 제공한다. 코드를 참고하자. 

  오류 발생시 사용자 입력 값 유지 
    - new FieldError("item", "price", item.getPrice(), false, null, null,
	  "가격은 1,000 ~ 1,000,000 까지 허용합니다.")
	
	- 사용자의 입력 데이터가 컨트롤러의 @ModelAttribute에 바인딩되는 시점에 오류가 
	  발생하면 모델 객체에 사용자 입력 값을 유지하기 어렵다. 예를 들어서 가격에 숫자가 아닌 
	  문자가 입력된다면 가격은 Integer 타입이므로 문자를 보관할 수 있는 방법이 없다. 
	  그래서 오류가 발생한 경우 사용자 입력 값을 보관하는 별도의 방법이 필요하다. 
	  그리고 이렇게 보관한 사용자 입력 값을 검증 오류 발생시 화면에 다시 출력하면 된다. 
	- 여기서 rejectedValue가 바로 오류 발생시 사용자 입력 값을 저장하는 필드다. 
	  bindingFailure는 타입 오류 같은 바인딩이 실패했는지 여부를 적어주면 된다.
	  여기서는 바인딩이 실패한 것은 아니기 때문에 false를 사용한다. 

  타임리프의 사용자 입력 값 유지 
    - th:field="*{price}"
	  타임리프의 th:field는 매우 똑똑하게 동작하는데, 정상 상황에는 모델 객체의 값을 
	  사용하지만, 오류가 발생하면 FieldError에서 보관한 값을 사용해서 값을 출력한다. 

  스프링의 바인딩 오류 처리 
    - 타입 오류로 바인딩에 실패하면 스프링은 FieldError를 생성하면서 사용자가 
	  입력한 값을 넣어둔다. 그리고 해당 오류를 BindingResult에 담아서 
	  컨트롤러를 호출한다. 따라서 타입 오류 같은 바인딩 실패시에도 사용자의 
	  오류 메시지를 정상 출력할 수 있다. 
```

### 오류 코드와 메시지 처리1 
```
  목표 
    - 오류 메시지를 체계적으로 다루어보자. 
  
  FieldError 생성자 
    - FieldError는 두 가지 생성자를 제공한다. 
	- 파라미터 목록 
	  - objectName: 오류가 발생한 객체 이름 
	  - field: 오류 필드 
	  - rejectedValue: 사용자가 입력한 값(거절된 값)
	  - bindingFailure: 타입 오류 같은 바인딩 실패인지, 검증 실패인지 구분 값 
	  - codes: 메시지 코드 
	  - arguments: 메시지에서 사용하는 인자 
	  - defaultMessage: 기본 오류 메시지 
	- FieldError, ObjectError의 생성자는 errorCode, arguments를 
	  제공한다. 이것은 오류 발생시 오류 코드로 메시지를 찾기 위해 사용된다. 

  errors 메시지 파일 생성 
    - messages.properties를 사용해도 되지만, 오류 메세지를 구분하기 쉽게 
	  errors.properties라는 별도의 파일로 관리해보자. 
	- 먼저 스프링 부트가 해당 메시지 파일을 인식할 수 있게 다음 설정을 추가한다. 
	  이렇게하면 messages.properties, errors.properties 두 파일 
	  모두 인식한다.(생략하면 messages.properties를 기본으로 인식한다.)

  스프링 부트 메시지 설정 추가 
    - application.properties
	  - spring.messages.basename=messages,errors
	
  errors.properties 추가 
    - src/main/resources/errors.properties
	  required.item.itemName=상품 이름은 필수입니다.
	  range.item.price=가격은 {0} ~ {1} 까지 허용합니다. 
	  max.item.quantity=수량은 최대 {0} 까지 허용합니다.
	  totalPriceMin=가격 * 수량의 합은 {0}원 이상이어야 합니다. 현재 값 = {1}

    참고 
      - errors_en.properties 파일을 생성하면 오류 메시지도 국제화 처리를 할 수 있다. 

  이제 errors에 등록한 메시지를 사용하도록 코드를 변경해보자. 
    ValidationItemControllerV2 - addItemV3() 추가
	  - addItemV2()의 @PostMapping 부분 주석 처리 
	  - codes: required.item.itemName을 사용해서 메시지 코드를 지정한다. 
	  - arguments: Object[]{1000, 1000000}를 사용해서 코드의 {0}, {1}로 
	    치환할 값을 전달한다. 
	
	실행 
	  - 실행해보면 메시지, 국제화에서 학습한 MessageSource를 찾아서 메세지를 
	    조회하는 것을 확인할 수 있다. 
```

### 오류 코드와 메시지 처리2
```
  목표 
    - FieldError, ObjectError는 다루기 너무 번거롭다. 
	- 오류 코드도 좀 더 자동화 할 수 있지 않을까? 예) item.itemName 처럼?

  컨트롤러에서 BindingResult는 검증해야 할 객체인 target 바로 다음에 온다. 
  따라서 BindingResult는 이미 본인이 검증해야 할 객체인 target을 알고 있다. 
  
  rejectedValue(), reject() 
    - BindingResult가 제공하는 rejectedValue(), reject()를 사용하면 
	  FieldError, ObjectError를 직접 생성하지 않고, 깔끔하게 검증 오류를 
	  다룰 수 있다.
	- rejectValue(), reject()를 사용해서 기존 코드를 단순화해보자. 

  ValidationItemControllerV2 - addItemV4() 추가
    - addItemV3()의 @PostMapping 부분 주석 처리 
	- 실행 
	  - 오류 메시지가 정상 출력된다. 그런데 errors.properties에 있는 코드를 
	    직접 입력하지 않았는데 어떻게 된 것일까? 
	
	rejectValue() 
	  - field: 오류 필드명 
	  - errorCode: 오류 코드(이 오류 코드는 메시지에 등록된 코드가 아니다. 뒤에서 
	    설명할 messagaeResolver를 위한 오류 코드이다.)
	  - errorArgs: 오류 메시지에서 {0}을 치환하기 위한 값 
	  - defaultMessage: 오류 메시지를 찾을 수 없을 때 사용하는 기본 메시지 
	  
	- 앞에서 BindingResult는 어떤 객체를 대상으로 검증하는지 target을 이미 
	  알고 있다고 했다. 따라서 target(item)에 대한 정보는 없어도 된다. 
	  오류 필드명은 동일하게 price를 사용했다. 
	
	축약된 오류 코드 
	  - FieldError()를 직접 다룰 때는 오류 코드를 range.item.price와 같이 
	    모두 입력했다. 그런데 rejectValue()를 사용하고 부터는 오류 코드를 
		range로 간단하게 입력했다. 그래도 오류 메시지를 잘 찾아서 출력한다. 
		무언가 규칙이 있는 것 처럼 보인다. 이 부분을 이해하려면 MessageCodesResolver를 
		이해해야 한다. 왜 이런식으로 오류 코드를 구성하는지 바로 다음에 자세히 알아보자. 
```

### 오류 코드와 메시지 처리3
```
  오류 코드를 만들 때 다음과 같이 자세히 만들 수도 있고, 
  required.item.itemName: 상품 이름은 필수입니다.
  range.item.price: 상품의 가격 범위 오류 입니다. 
  
  또는 다음과 같이 단순하게 만들 수도 있다. 
  required: 필수 값 입니다. 
  range: 범위 오류 입니다. 
  
  단순하게 만들면 범용성이 좋아서 여러곳에서 사용할 수 있지만, 메시지를 세밀하게 작성하기 어렵다. 
  반대로 너무 자세하게 만들면 범용성이 떨어진다. 가장 좋은 방법은 범용성으로 사용하다가, 세밀하게 
  작성해야 하는 경우에는 세밀한 내용이 적용되도록 메시지에 단계를 두는 방법이다. 
  
  예를 들어서 required라고 오류 코드를 사용한다고 가정해보자. 
  다음과 같이 required라는 메시지만 있으면 이 메시지를 선택해서 사용하는 것이다. 
  
    required: 필수 값 입니다. 
	
  그런데 오류 메시지에 required.item.itemName와 같이 객체명과 필드명을 조합한 
  세밀한 나머지 코드가 있으면 이 메시지를 높은 우선순위로 사용하는 것이다. 
    
	#Level1
	required.item.itemName: 상품 이름은 필수 입니다. 
	
	#Level2
	required: 필수 값 입니다. 
  
  물론 이렇게 객체명과 필드명을 조합한 메시지가 있는지 우선 확인하고, 없으면 좀 더 범용적인 
  메시지를 선택하도록 추가 개발을 해야겠지만, 범용성 있게 잘 개발해두면, 메시지의 추가 만으로 
  매우 편리하게 오류 메시지를 관리할 수 있을 것이다. 
  
  스프링은 MessageCodesResolver라는 것으로 이러한 기능을 지원한다.
```

### 오류 코드와 메시지 처리4
```
  우선 테스트 코드로 MessageCodesResolver를 알아보자. 
  
  MessageCodesResolverTest
    - MessageCodesResolver
	  - 검증 오류 코드로 메시지 코드를 생성한다. 
	  - MessageCodesResolver 인터페이스이고 DefaultMessageCodesResolver는 
	    기본 구현체이다. 
	  - 주로 다음과 함께 사용 ObjectError, FieldError
	
	- DefaultMessageCodesResolver의 기본 메시지 생성 규칙
	  - 객체 오류 
	    - 객체 오류의 경우 다음 순서로 2가지 생성 
		  1.: code + "." + object name
		  2.: code
		  
		  예)오류 코드: required, object name: item
		  1.: required.item
		  2.: required
	
	  - 필드 오류 
	    - 필드 오류의 경우 다음 순서로 4가지 메시지 코드 생성 
		  1.: code + "." + object name + "." + field
		  2.: code + "." + field
		  3.: code + "." + field type
		  4.: code
		  
		  예)오류 코드: typeMismatch, object name "user", 
		    field "age", field type: int
		  1.: "typeMismatch.user.age"
		  2.: "typeMismatch.age"
		  3.: "typeMismatch.int"
		  4.: "typeMismatch"
	
	  - 동작 방식 
	    - rejectValue(), reject()는 내부에서 MessageCodesResolver를 사용한다. 
		  여기에서 메시지 코드들을 생성한다. 
		- FieldError, ObjectError의 생성자를 보면, 오류 코드를 하나가 아니라 
		  여러 오류 코드를 가질 수 있다. MessageCodesResolver를 통해서 
		  생성된 순서대로 오류 코드를 보관한다. 
		- 이 부분을 BindingResult의 로그를 통해서 확인해보자. 
		  - codes [range.item.price, range.price, range.java.lang.Integer, range]
	
	  - FieldError rejectValue("itemName", "required")
	    - 다음 4가지 오류 코드를 자동으로 생성 
		- required.item.itemName
		- required.itemName
		- required.java.lang.String
		- required
	
	  - ObjectError reject("totalPriceMin")
	    - 다음 2가지 오류 코드를 자동으로 생성 
		- totalPriceMin.item
		- totalPriceMin
	
	  - 오류 메시지 출력 
	    - 타임리프의 화면을 렌더링 할 때 th:errors가 실행된다. 만약 이때 오류가 있다면 
		  생성된 오류 메시지 코드를 순서대로 돌아가면서 메시지를 찾는다. 그리고 없으면 디폴트 
		  메시지를 출력한다. 
```

### 오류 코드와 메시지 처리5
```
  오류 코드 관리 전략 
  
  핵심은 구체적인 것에서! 덜 구체적인 것으로! 
    - MessageCodesResolver는 required.item.itemName처럼 구체적인 것을
	  먼저 만들어주고, required처럼 덜 구체적인 것을 가장 나중에 만든다. 
	  이렇게 하면 앞서 말한 것 처럼 메시지와 관련된 공통 전략을 편리하게 도입할 수 있다. 

  왜 이렇게 복잡하게 사용하는가?
    - 모든 오류 코드에 대해서 메시지를 각각 다 정의하면 개발자 입장에서 관리하기 
	  너무 힘들다. 크게 중요하지 않은 메시지는 범용성 있는 required 같은 메시지로 
	  끝내고, 정말 중요한 메시지는 꼭 필요할 때 구체적으로 사용하는 방식이 더 효과적이다. 

  이제 우리 애플리케이션에 이런 오류 코드 전략을 도입해보자.
  
  errors.properties 
    - 크게 객체 오류와 필드 오류를 나누었다. 그리고 범용성에 따라 레벨을 나누어두었다. 
	  - itemName의 경우 required 검증 오류 메시지가 발생하면 다음 코드 순서대로
	    메시지가 생성된다. 
		1. required.item.itemName
		2. required.itemName
		3. required.java.lang.String
		4. required
	
	- 그리고 이렇게 생성된 메시지 코드를 기반으로 순서대로 MessageSource 
	  메시지에서 찾는다. 
	- 구체적인 것에서 덜 구체적인 순서대로 찾는다. 메시지에 1번이 없으면 2번을 찾고, 
	  2번이 없으면 3번을 찾는다. 
	- 이렇게 되면 만약에 크게 중요하지 않은 오류 메시지는 기존에 정의된 것을 그냥 
	  재활용 하면 된다!
	
	실행 
	  - Level1 전부 주석해보자.
	  - Level2,3 전부 주석해보자
	  - Level4 전부 주석해보자 -> 못찾으면 코드에 작성한 디폴트 메시지를 사용한다. 
	  - Object 오류도 Level1, Level2로 재활용 가능하다.

  ValidationUtils
    - ValidationUtils 사용 전 
	  - if (!StringUtils.hasText(item.getItemName())) {
		 bindingResult.rejectValue("itemName", "required", "기본: 상품 이름은
		필수입니다.");
		}
	- ValidationUtils 사용 후
	  - 다음과 같이 한줄로 가능, 제공하는 기능은 Empty, 공백 같은 단순한 기능만 제공 
	  - ValidationUtils.rejectIfEmptyOrWhitespace(bindingResult, 
		"itemName","required");

  정리 
    - 1. rejectValue() 호출 
	  2. MessageCodesResolver를 사용해서 검증 오류 코드로 메시지 코드들을 생성 
	  3. new FieldError()를 생성하면서 메시지 코드들을 보관 
	  4. th:errors에서 메시지 코드들로 메시지를 순서대로 메시지에서 찾고, 노출 
```

### 오류 코드와 메시지 처리6
```
  스프링이 직접 만든 오류 메시지 처리 
  
  검증 오류 코드는 다음과 같이 2가지로 나눌 수 있다. 
    - 개발자가 직접 설정한 오류 코드 -> rejectValue()를 직접 호출 
	- 스프링이 직접 검증 오류에 추가한 경우(주로 타입 정보가 맞지 않음)
	
  지금까지 학습한 메시지 코드 전략의 강점을 지금부터 확인해보자. 
    - price 필드에 문자 "A"를 입력해보자. 
	  로그를 확인해보면 BindingResult에 FieldError가 담겨있고, 다음과 같은 
	  메시지 코드들이 생성된 것을 확인할 수 있다. 
	  - codes[typeMismatch.item.price, typeMismatch.price, 
	    typeMismatch.java.lang.Integer, typeMismatch]
	
	- 다음과 같이 4가지 메시지 코드가 입력되어 있다.
	  - typeMismatch.item.price
	  - typeMismatch.price
	  - typeMismatch.java.lang.Integer
	  - typeMismatch
	
	- 그렇다. 스프링은 타입 오류가 발생하면 typeMismatch라는 오류 코드를 사용한다. 
	  이 오류 코드가 MessageCodesResolver를 통하면서 4가지 메시지 코드가 
	  생성된 것이다. 
	
	실행해보자 
	  - 아직 errors.properties에 메시지 코드가 없기 때문에 스프링이 생성한 
	    기본 메시지가 출력된다. 
	
	errors.properties에 다음 내용을 추가하자 
	  #추가 
	  typeMismatch.java.lang.Integer=숫자를 입력해주세요.
	  typeMismatch=타입 오류입니다.
	
	다시 실행해보자. 
	  - 결과적으로 소스코드를 하나도 건들지 않고, 원하는 메시지를 단계별로 설정할 수 있다. 

  정리 
    - 메시지 코드 생성 전략은 그냥 만들어진 것이 아니다. 조금 뒤에서 Bean Validation을 
	  학습하면 그 진가를 더 확인할 수 있다.
```

### Validator 분리1
```
  목표 
    - 복잡한 검증 로직을 별도로 분리하자. 

  컨트롤러에서 검증 로직이 차지하는 부분은 매우 크다. 이런 경우 별도의 클래스로 역할을
  분리하는 것이 좋다. 그리고 이렇게 분리한 검증 로직을 재사용 할 수도 있다. 
  
  ItemValidator를 만들자.
    - 스프링은 검증을 체계적으로 제공하기 위해 다음 인터 페이스를 제공한다.
	  - public interface Validator {
		  boolean supports(Class<?> clazz);
		  void validate(Object target, Errors errors);
		}
	    - supports() {}: 해당 검증기를 지원하는 여부 확인(뒤에서 설명)
		- validate(Object target, Errors errors)
		  - 검증 대상 객체와 BindingResult

  ItemValidator 직접 호출하기
  ValidationItemControllerV2 - addItemV5()
    - addItemV4의 @PostMapping 부분 주석 처리 
	- ItemValidator를 스프링 빈으로 주입 받아서 직접 호출했다. 
	
	실행 
	  - 실행해보면 기존과 완전히 동일하게 동작하는 것을 확인할 수 있다. 
	    검증과 관련된 부분이 깔끔하게 분리되었다.
```

### Validator 분리2
```
  스프링이 Validator 인터페이스를 별도로 제공하는 이유는 체계적으로 검증 기능을 도입하기 위해서다. 
  그런데 앞에서는 검증기를 직접 불러서 사용했고, 이렇게 사용해도 된다. 그런데 Validator 인터페이스를
  사용해서 검증기를 만들면 스프링의 추가적인 도움을 받을 수 잇다. 
  
  WebDataBinder를 통해서 사용하기 
    - WebDataBinder는 스프링의ㅡ 파라미터 바인딩의 역할을 해주고 검증 기능도 내부에 포함한다.

  ValidationItemControllerV2에 다음 코드를 추가하자
    - @InitBinder
	  public void init(WebDataBinder dataBinder) {
		 log.info("init binder {}", dataBinder);
		 dataBinder.addValidators(itemValidator);
	  }
	  - 이렇게 WebDataBinder에 검증기를 추가하면 해당 컨트롤러에서는 검증기를 
	    자동으로 적용할 수 있다. @InitBinder -> 해당 컨트롤러에만 영향을 준다. 
		글로벌 설정은 별도로 해야한다.(마지막에 설명)

  @Validated 적용
  ValidationItemControllerV2 - addItemV6()
    - addItemV5()의 @PostMapping 부분 주석 처리 
	- validator를 직접 호출하는 부분이 사라지고, 대신에 검증 대상 앞에 
	  @Validated가 붙었다. 
	  
	- 실행 
	  - 기존과 동일하게 잘 동작하는 것을 확인할 수 있다. 
	  
	- 동작 방식 
	  - @Validated는 검증기를 실행하라는 애노테이션이다.
	  - 이 애노테이션이 붙으면 앞서 WebDataBinder에 등록한 검증기를 찾아서 실행한다.
	    그런데 여러 검증기를 등록한다면 그 중에 어떤 검증기가 실행되어야 할지 구분이 
		필요하다. 이때 supports()가 사용된다. 
	  - 여기서는 supports(Item.class)호출되고, 결과가 true이므로 
	    ItemValidator의 validate()가 호출된다.

  글로벌 설정 - 모든 컨트롤러에 다 적용 
    @SpringBootApplication
	public class ItemServiceApplication implements WebMvcConfigurer {
	
	 public static void main(String[] args) {
		SpringApplication.run(ItemServiceApplication.class, args);
	 }
	 
	 @Override
	 public Validator getValidator() {
		return new ItemValidator();
	 }
	 
	}
    - 이렇게 글로벌 설정을 추가할 수 있다. 기존 컨트롤러의 @InitBinder를 제거해도 
	  글로벌 설정으로 정상 동작하는 것을 확인할 수 있다. 이어지는 다음 강의를 위해서는 
	  글로벌 설정은 꼭 제거해두자. 
	
	주의 
	  - 글로벌 설정을 하면 다음에 설명할 Bean Validator가 자동 등록되지 않는다.
	    글로벌 설정 부분은 주석처리해두자. 참고로 글로벌 설정을 직접 사용하는 경우는 
		드물다.
	참고 
	  - 검증시 @Validated, @Valid 둘 다 사용가능하다. 
	  - javax.validation.@Valid를 사용하려면 build.gradle 의존관계
	    추가가 필요하다. 
	  - implementation 'org.springframework.boot:spring-boot-starter-validation'
	  - @Validated는 스프링 전용 검증 애노테이션이고, @Valid는 자바 표준 검증 
	    애노테이션이다. 자세한 내용은 다음 Bean Validation에서 설명하겠다.
```

## 검증2 - Bean Validation 

### Bean Validation - 소개 
```
  검증 기능을 지금처럼 매번 코드로 작성하는 것은 상당히 번거롭다. 특히 특정 필드에 대한 
  검증 로직은 대부분 빈 값인지 아닌지, 특정 크기를 넘는지 아닌지와 같이 매우 일반적인 
  로직이다. 다음 코드를 보자. 
    public class Item {
		private Long id;
		
		@NotBlank
		private String itemName;
		
		@NotNull
		@Range(min = 1000, max = 1000000)
		private Integer price;
		
		@NotNull
		@Max(9999)
		private Integer quantity;
		//...
	}
	- 이런 검증 로직을 모든 프로젝트에 적용할 수 있게 공통화하고, 표준화 한 것이 
	  바로 Bean Validation이다.
	- Bean Validation을 잘 활용하면, 애노테이션 하나로 검증 로직을 매우 
	  편리하게 적용할 수 있다. 

  Bean Validation 이란? 
    - 먼저 Bean Validation은 특정한 구현체가 아니라 Bean Validation 2.0(JSR-380)
	  이라는 기술 표준이다. 쉽게 이야기해서 검증 애노테이션과 여러 인터페이스의 모음이다. 
	  마치 JPA 표준 기술이고 그 구현체로 하이버네이트가 있는 것과 같다. 
	- Bean Validation을 구현한 기술중에 일반적으로 사용하는 구현체는 하이버네트 
	  Validator이다. 이름이 하이버네이트가 붙어서 그렇지 ORM과는 관련이 없다. 
```

### Bean Validation - 시작 
```
  Bean Validation 기능을 어떻게 사용하는지 코드로 알아보자. 먼저 스프링과 통합하지 않고, 순수한 
  Bean Validation 사용법 부터 테스트 코드로 알아보자. 
  
  Bean Validation 의존관계 추가 
  
  의존 관계 추가 
    - Bean Validation을 사용하려면 다음 의존관계를 추가해야 한다. 
	- build.gradle
	  - implementation 'org.springframework.boot:spring-boot-starter-validation'
	- spring-boot-starter-validation 의존관계를 추가하면 라이브러리가 추가 된다. 

  Jakarta Bean Validation
    - jakarta.validation-api: Bean Validation 인터페이스 
	- hibernate-validator 구현체 

  테스트 코드 작성 
  
  Item - Bean Validation 애노테이션 적용 
    - 검증 애노테이션 
	  - @NotBlank: 빈값 + 공백만 있는 경우를 허용하지 않는다. 
	  - @NotNull: null을 허용하지 않는다. 
	  - @Range(min=1000, max=1000000):범위 안의 값이어야 한다. 
	  - @Max(9999): 최대 9999까지만 허용한다. 
	
	참고 
	  - javax.validation.constraints.NotNull
	  - org.hibernate.validator.constraints.Range
	  
	  - javax.validation으로 시작하면 특정 구현에 관계없이 제공되는 표준 인터페이스이고, 
	    org.hibernate.validator로 시작하면 하이버네이트 validator 구현체를 
		사용할 때만 제공되는 검증 기능이다. 실무에서 대부분 하이버네이트 validator를 
		사용하므로 자유롭게 사용해도 된다. 

  BeanValidationTest - Bean Validation 테스트 코드 작성 
    - 검증기 생성 
	  - 다음 코드와 같이 검증기를 생성한다. 이후 스프링과 통합하면 우리가 직접 이런 코드를 
	    작성하지는 않으므로, 이렇게 사용하는구나 정도만 참고하자 
		- ValidatorFactory factory = Validation.buildDefaultValidatorFactory();
		  Validator validator = factory.getValidator();
	
	- 검증 실행 
	  - 검증 대상(item)을 직접 검증기에 넣고 그 결과를 받는다. Set에는 ConstraintViolation이라는 
	    검증 오류가 담긴다. 따라서 결과가 비어있으면 검증 오류가 없는 것이다. 
		- Set<ConstraintViolation<Item>> violations = validator.validate(item);
	
	- 실행 결과 
	  - ConstraintViolation 출력 결과를 보면, 검증 오류가 발생한 객체, 필드, 메시지 정보등 
	    다양한 정보를 확인할 수 있다. 

  정리 
    - 이렇게 빈 검증기(Bean Validation)를 직접 사용하는 방법을 알아보았다. 아마 지금까지 배웠던 
	  스프링 MVC 검증 방법에 빈 검증기를 어떻게 적용하면 좋을지 여러가지 생각이 들 것이다. 
	  스프링은 이미 개발자를 위해 빈 검증기를 스프링에 완전히 통합해두었다. 
``` 

### Bean Validation - 프로젝트 준비 V3
```
  앞서 만든 기능을 유지하기 위해, 컨트롤러와 템플릿 파일을 복사하자.
``` 

### Bean Validation - 스프링 적용 
```
  ValidationItemControllerV3 코드 수정 
    - 제거: addItemV1() ~ addItemV5()
	- 변경: addItemV6() -> addItem()
	
	코드 제거 
	  - 기존에 등록함 ItemValidator를 제거해두자! 오류 검증기가 중복 적용된다. 
	
	참고 
	  - 특정 필드의 범위를 넘어서는 검증(가격*수량의 합은 10,000원 이상) 기능이 빠졌는데,
	    이 부분은 조금 뒤에 설명한다. 

  스프링 MVC는 어떻게 Bean Validator를 사용? 
    - 스프링 부트가 spring-boot-starter-validation 라이브러리를 넣으면 자동으로 
	  Bean Validator를 인지하고 스프링에 통합한다. 

  스프링 부트는 자동으로 글로벌 Validator로 등록한다. 
    - LocalValidatorFactoryBean을 글로벌 Validator로 등록한다. 
	  이 Validator는 @NotNull같은 애노테이션을 보고 검증을 수행한다. 이렇게 글로벌 
	  Validator가 적용되어 있기 때문에, @Valid, @Validated만 적용하면 된다. 
	  검증 오류가 발생하면, FieldError, ObjectError를 생성해서 
	  BindingResult에 담아준다. 
	
	- 주의 
	  - 글로벌 Validator를 직접 등록하면 스프링 부트는 Bean Validator를 
	    글로벌 Validator로 등록하지 않는다. 따라서 애노테이션 기반의 빈 검증기가 
		동작하지 않는다. 
	
	- 참고 
	  - 검증시 @Validated, @Valid 둘다 사용가능하다. 
	  - javax.validation.@Valid를 사용하려면 build.gradle 의존관계 추가가 
	    필요하다.(이전에 추가했다.)
	  - implementation 'org.springframework.boot:spring-boot-starter-validation'
	    @Validated는 스프링 전용 검증 애노테이션이고, @Valid는 자바 표준 검증 
		애노테이션이다. 둘중 아무거나 사용해도 동일하게 작동하지만, @Validated는 
		내부에 groups라는 기능을 포함하고 있다. 이 부분은 조금 뒤에 다시 설명하겠다.
		
  검증 순서 
    1. @ModelAttribute 각각의 필드에 타입 변환 시도 
	  1-1). 성공하면 다음으로 
	  1-2). 실패하면 typeMismatch로 FieldError 추가 
	2. Validator 적용 

  바인딩에 성공한 필드만 Bean Validation 적용 
    - BeanValidator는 바인딩에 실패한 필드는 BeanValidation을 적용하지 않는다. 
	  생각해보면 타입 변환에 성공해서 바인딩에 성공한 필드여야 BeanValidation 
	  적용이 의미 있다. (일단 모델 객체에 바인딩 받는 값이 정상으로 들어와야 
	  검증도 의미가 있다.)
	
	- @ModelAttribute -> 각각의 필드 타입 변환 시도 -> 변환에 성공한 필드만 
	  BeanValidation 적용 
	
	- 예) 
	  - itemName에 문자 "A"입력 -> 타입 변환 성공 -> itemName 필드에 BeanValidation 적용 
	  - price에 문자 "A" 입력 -> "A"를 숫자 타입 변환 시도 실패 
	    -> typeMismatch FieldError추가 -> price 필드는 BeanValidation 적용 X
```

### Bean Validation - 에러 코드
```
  Bean Validation이 기본으로 제공하는 오류 메시지를 좀더 자세히 변경하고 싶으면 
  어떻게 하면 될까?
  
  Bean Validation을 적용하고 bindingResult에 등록된 검증 오류 코드를 보자.
  오류 코드가 애노테이션 이름으로 등록된다. 마치 typeMismatch와 유사하다. 
  
  NotBlank라는 오류 코드를 기반으로 MessageCodesResolver를 통해 다양한 메시지 코드가 
  순서대로 생성된다. 
  
  @NotBlank
    - NotBlank.item.itemName
	- NotBlank.itemName
	- NotBlank.java.lang.String
	- NotBlank

  @Range
    - Range.item.price
	- Range.price
	- Range.java.lang.Integer
	- Range

  메시지 등록 
	- 이제 메시지를 등록해보자.
	- errors.properties 
	  #Bean Validation 추가
	  NotBlank={0} 공백X 
	  Range={0}, {2} ~ {1} 허용
	  Max={0}, 최대 {1}
	  
	- {0}은 필드명이고, {1},{2}...은 각 애노테이션 마다 다르다. 

  BeanValidation 메시지 찾는 순서 
    1. 생성된 메시지 코드 순서대로 messageSource에서 메시지 찾기 
	2. 애노테이션의 message 속성 사용 -> @NotBlank(message = "공백! {0}")
	3. 라이브러리가 제공하는 기본 값 사용 -> 공백일 수 없습니다. 
```

### Bean Validation - 오브젝트 오류 
```
  Bean Validation에서 특정 필드(FieldError)가 아닌 해당 오브젝트 관련 오류(ObjectError)는 
  어떻게 처리할 수 있을가?
  다음과 같이 @ScriptAssert()를 사용하면 된다. 
    @Data
	@ScriptAssert(lang = "javascript", script = "_this.price * _this.quantity >= 
	10000")
	public class Item {
	 //...
	}

  - 실행해보면 정상 수행되는 것을 확인할 수 있다. 메시지 코드도 다음과 같이 생성된다. 
    - 메시지 코드 
	  - ScriptAssert.item
	  - ScriptAssert
	
	- 그런데 실제 사용해보면 제약이 많고 복잡하다. 그리고 실무에서는 검증 기능이 
	  해당 객체의 범위를 넘어서는 경우들도 종종 등장하는데, 그런 경우 대응이 어렵다. 
	- 따라서 오브젝트 오류(글로벌 오류)의 경우 @ScriptAssert를 억지로 
	  사용하는 것 보다는 오브젝트 오류 관련 부분만 직접 자바 코드로 
	  작성하는 것을 권장한다. 
	- @ScriptAssert 부분 제거
```

### Bean Validation - 수정에 적용 
```
  상품 수정에도 빈 검증(Bean Validation)을 적용해보자. 
  
  수정에도 검증 기능을 추가하자 
  ValidationItemControllerV3 - edit() 변경 
    - edit(): Item 모델 객체에 @Validated를 추가하자 
	- 검증 오류가 발생하면 editForm으로 이동하는 코드 추가 

  validation/v3/editForm.html 변경
    - .field-error css 추가 
	- 글로벌 오류 메시지 
	- 상품명, 가격, 수량 필드에 검증 기능 추가 
``` 

### Bean Validation - 한계 
```
  수정시 검증 요구사항 
    - 데이터를 등록할 때와 수정할 때는 요구사항이 다를 수 있다. 
	
	등록시 기존 요구사항 
	  - 타입 검증 
	    - 가격, 수량에 문자가 들어가면 검증 오류 처리 
	  - 필드 검증 
	    - 상품명: 필수, 공백X
		- 가격: 1000원 이상, 1백만원 이하 
		- 수량: 최대 9999 
	  - 특정 필드의 범위를 넘어서는 검증 
	    - 가격 * 수량의 합은 10,000원 이상 
	
	수정시 요구사항
	  - 등록시에는 quantity 수량을 최대 9999까지 등록할 수 있지만 
	    수정시에는 수량을 무제한으로 변경할 수 있다. 
	  - 등록시에는 id에 값이 없어도 되지만, 수정시에는 id 값이 필수이다. 
	
	수정 요구사항 적용 
	  - 수정시에는 Item에서 id 값이 필수이고, quantity도 무제한으로 적용할 수 있다. 
	  - 수정 요구사항을 적용하기 위해 다음을 적용했다. 
	    - id: @NotNull 추가 
		- quantity: @Max(9999)제거 
	
	참고 
	  - 현재 구조에서는 수정시 item의 id값은 항상 들어있도록 로직이 구성되어 있다. 
	    그래서 검증하지 않아도 된다고 생각할 수 있다. 그런데 HTTP요청은 언제든지 
		악의적으로 변경해서 요청할 수 있으므로 서버에서 항상 검증해야 한다. 예를 들어서 
		HTTP 요청을 변경해서 item의 id 값을 삭제하고 요청할 수도 있다. 
		따라서 최종 검증은 서버에서 진행하는 것이 안전하다. 
	
	수정을 실행해보자. 
	  - 정상 동작을 확인할 수 있다. 
	그런데 수정은 잘 동작하지만 등록에서 문제가 발생한다. 
	  - 등록시에는 id에 값도 없고, quantity 수량 제한 최대 값인 9999도 
	    적용되지 않는 문제가 발생한다. 
	등록시 화면이 넘어가지 않으면서 다음과 같은 오류를 볼 수 있다. 
	  - 'id': rejected value [null];
	  - 왜냐하면 등록시에는 id에 값이 없다. 따라서 @NotNull id를 적용한 것 
	    때문에 검증에 실패하고 다시 폼 화면으로 넘어온다. 결국 등록 자체도 불가능하고, 
		수량 제한도 걸지 못한다. 
	  - 결과적으로 item은 등록과 수정에서 검증 조건의 충돌이 발생하고, 등록과 수정은 
	    같은 BeanValidation을 적용할 수 없다. 이 문제를 어떻게 해결할 수 있을까?
``` 

### Bean Validation - groups
```
  동일한 모델 객체를 등록할 때와 수정할 때 각각 다르게 검증하는 방법을 알아보자. 
  
  방법 2가지 
    - BeanValidation의 groups 기능을 사용한다. 
	- Item을 직접 사용하지 않고, ItemSaveForm, ItemUpdateForm 같은 폼 전송을 위한 
	  별도의 모델 객체를 만들어서 사용한다. 

  BeanValidation groups 기능 사용 
    - 이런 문제를 해결하기 위해 Bean Validation은 groups라는 기능을 제공한다. 
	- 예를 들어서 등록시에 검증할 기능과 수정시에 검증할 기능을 각각 그룹으로 나누어 
	  적용할 수 있다. 
	
	코드로 확인해보자 
	
	groups 적용 
	  - 저장용 groups 생성 
	  - 수정용 groups 생성 
	  - Item - groups 적용 
	  - ValidationItemControllerV3 - 저장 로직에 SaveCheck Groups 적용
	    - addItem()을 복사해서 addItemV2() 생성, SaveCheck.class 적용 
		- 기존 addItem() @PostMapping("/add") 주석처리 
	  - ValidationItemControllerV3 - 수정 로직에 UpdateCheck Groups 적용
	    - edit()를 복사해서 editV2() 생성, UpdateCheck.class 적용 
		- 기존 edit() @PostMapping("/{itemId}/edit") 주석처리 
		
	  참고
		- @Valid에는 groups를 적용할 수 있는 기능이 없다. 따라서 groups를 
		  사용하려면 @Validated를 사용해야 한다. 

  정리 
    - groups 기능을 사용해서 등록과 수정시에 각각 다르게 검증을 할 수 있었다. 그런데 
	  groups 기능을 사용하니 Item은 물론이고, 전반적으로 복잡도가 올라갔다. 
	  사실 groups 기능은 실제 잘 사용되지는 않는데, 그 이유는 실무에서는 주로 
	  다음에 등장하는 등록용 폼 객체와 수정용 폼 객체를 분리해서 사용하기 때문이다. 
```

### Form 전송 객체 분리 - 소개
```
  ValidationItemControllerV4
    - 실무에서는 groups를 잘 사용하지 않는데, 그 이유가 다른 곳에 있다. 바로 
	  등록시 폼에서 전달하는 데이터가 Item 도메인 객체와 딱 맞지 않기 때문이다. 
	  소위 "Hello World"예제에서는 폼에서 전달하는 데이터와 Item 도메인 
	  객체가 딱 맞는다. 하지만 실무에서는 회원 등록시 회원과 관련된 데이터만 
	  전달받는 것이 아니라, 약관 정보도 추가로 받는 등 Item과 관계없는 
	  수 많은 부가 데이터가 넘어온다. 
	  그래서 보통 Item을 직접 전달 받는 것이 아니라, 복잡한 폼의 데이터를 
	  컨트롤러까지 전달할 별도의 객체를 만들어서 전달한다. 예를 들면 ItemSaveForm
	  이라는 폼을 전달받는 전용 객체를 만들어서 @ModelAttribute로 사용한다. 
	  이것을 통해 컨트롤러에서 폼 데이터를 전달 받고, 이후 컨트롤러에서 
	  필요한 데이터를 사용해서 Item을 생성한다. 
	
  폼 데이터 전달에 Item 도메인 객체 사용 
    - HTML Form -> Item -> Controller -> Item -> Repository 
	  - 장점
	    - Item 도메인 객체를 컨트롤러, 리포지토리 까지 직접 전달해서 
	      중간에 Item을 만드는 과정이 없어서 간단하다. 
	  - 단점 
	    - 간단한 경우에만 적용할 수 있다. 수정시 검증이 중복될 수 있고, groups를 
	      사용해야 한다. 
	
  폼 데이터 전달을 위한 별도의 객체 사용 
    - HTML Form -> ItemSaveForm -> Controller -> Item 생성 -> Repository
	  - 장점 
	    - 전송하는 폼 데이터가 복잡해도 거기에 맞춘 별도의 폼 객체를 사용해서 데이터를 
		  전달 받을 수 있다. 보통 등록과 수정용으로 별도의 폼 객체를 만들기 때문에 검증이 
		  중복되지 않는다. 
		- 단점
		  - 폼 데이터를 기반으로 컨트롤러에서 Item 객체를 생성하는 변환 과정이 추가된다.
	
	- 수정의 경우 등록과 수정은 완전히 다른 데이터가 넘어온다. 생각해보면 회원 가입시 다루는 
	  데이터와 수정시 다루는 데이터는 범위에 차이가 있다. 예를 들면 등록시에는 로그인 id, 
	  주민번호 등등을 받을 수 있지만, 수정시에는 이런 부분이 빠진다. 그리고 검증 로직도 
	  많이 달라진다. 그래서 ItemUpdateForm이라는 별도의 객체로 데이터를 전달받는
	  것이 좋다. 
	- Item 도메인 객체를 폼 전달 데이터로 사용하고, 그대로 쭉 넘기면 편리하겠지만, 
	  앞에서 설명한 것과 같이 실무에서는 Item의 데이터만 넘어오는 것이 아니라 
	  무수한 추가 데이터가 넘어온다. 그리고 더 나아가서 Item을 생성하는데 필요한 
	  추가 데이터를 데이터베이스나 다른 곳에서 찾아와야 할 수도 있다. 
	- 따라서 이렇게 폼 데이터 전달을 위한 별도의 객체를 사용하고, 
	  등록 수정용 폼 객체를 나누면 등록, 수정이 완전히 분리되기 때문에 
	  groups를 적용할 일은 드물다. 

  Q.: 이름은 어떻게 지어야 하나요?
    - 이름은 의미있게 지으면 된다. ItemSave라고 해도 되고, ItemSaveForm,
	  ItemSaveRequest, ItemSaveDto등으로 사용해도 된다. 
	  중요한 것은 일관성이다. 

  Q.: 등록, 수정용 뷰 템플릿이 비슷한데 합치는게 좋을까요?
    - 한 페이지에 그러니까 뷰 템플릿 파일을 등록과 수정을 합치는게 좋을지 
	  고민이 될 수 있다. 각각 장단점이 있으므로 고민하는게 좋지만,
	  어설프게 합치면 수 많은 분기분(등록일 때, 수정일 때)때문에 
	  나중에 유지보수에서 고통을 맛본다. 
	  이런 어설픈 분기분들이 보이기 시작하면 분리해야 할 신호이다. 
```

### Form 전송 객체 분리 - 개발 
```
  ITEM 원복 
    - 이제 Item의 검증은 사용하지 않으므로 검증 코드를 제거해도 된다. 

  ItemSaveForm - ITEM 저장용 폼
  ItemUpdateForm - ITEM 수정용 폼
  
  이제 등록, 수정용 폼 객체를 사용하도록 컨트롤러를 수정하자.
  ValidationItemControllerV4
    - 기존 코드 제거: addItem(), addItemV2()
    - 기존 코드 제거: edit(), editV2()
    - 추가: addItem() , edit()
	
	- 폼 객체 바인딩 
	  - Item 대신에 ItemSaveForm을 전달 받는다. 그리고 @Validated로 
	    검증도 수행하고, BindingResult로 검증 결과도 받는다. 
	- 주의
	  - @ModelAttribute("item")에 item 이름을 넣어준 부분을 주의하자. 
	    이것을 넣지 않으면 ItemSaveForm의 경우 규칙에 의해 itemSaveForm이라는 
		이름으로 MVC Model에 담기게 된다. 이렇게 되면 뷰 템플릿에서는 
		접근하는 th:object이름도 함께 변경해주어야 한다. 
	
	- 폼 객체를 Item으로 변환
	  - 폼 객체의 데이터를 기반으로 Item 객체를 생성한다. 이렇게 폼 객체 처럼 
	    중간에 다른 객체가 추가되면 변환하는 과정이 추가된다. 
	- 수정 
	  - 수정의 경우도 등록과 같다. 그리고 폼 객체를 Item 객체로 변환하는 과정을 거친다. 

  정리 
    - Form 전송 객체 분리해서 등록과 수정에 딱 맞는 기능을 구성하고, 
	  검증도 명확히 분리했다. 
```

### Bean Validation - HTTP 메시지 컨버터
```
  @Valid, @Validated는 HttpMessageConverter(@RequestBody)에도 
  적용할 수 있다. 
  
  참고 
    - @ModelAttribute는 HTTP 요청 파라미터(URL 쿼리 스트링, POST Form)를 
	  다룰 때 사용한다. 
	- @RequestBody는 HTTP Body의 데이터를 객체로 변환할 때 사용한다. 
	  주로 API JSON 요청을 다룰 때 사용한다. 

  ValidationItemApiController 생성
    - Postman을 사용해서 테스트 해보자. 
	
	- 성공 요청 
	  - Postman에서 Body -> raw -> JSON을 선택해야 한다. 
	
	- API의 경우 3가지 경우를 나누어 생각해야 한다. 
	  - 성공 요청: 성공 
	  - 실패 요청: JSON을 객체로 생성하는 것 자체가 실패함 
	  - 검증 오류 요청: JSON을 객체로 생성하는 것은 성공했고, 검증에서 실패함 
	
	- 성공 요청 로그 
	  - API 컨트롤러 호출 
	    성공 로직 실행 
	
	- 실패 요청 
	  - POST http://localhost:8080/validation/api/items/add
	    {"itemName": "hello", "price":"A", "quantity":10}
	
	  - price의 값에 숫자가 아닌 문자를 전달해서 실패하게 만들어보자 
	    - HttpMessageConverter에서 요청 JSON을 Item 객체로 
	      생성하는데 실패한다. 이 경우는 Item 객체를 만들지 못하기 때문에 
		  컨트롤러 자체가 호출되지 않고 그 전에 예외가 발생한다. 
		  물론 Validation도 실행되지 않는다. 
	- 검증 오류 요청 
	  - POST http://localhost:8080/validation/api/items/add
		{"itemName":"hello", "price":1000, "quantity": 10000}
	  - 수량(quantity)이 10000이면 BeanValidation @Max(9999)에서 걸린다. 
	    - return bindingResult.getAllErrors();는 ObjectError와 
		  FieldError를 반환한다. 스프링이 이 객체를 JSON으로 변환해서 
		  클라이언트에 전달했다. 여기서는 예시로 보여주기 위해서 검증 오류 객체들을 
		  그대로 반환했다. 실제 개발할 때는 이 객체들을 그대로 사용하지 말고, 
		  필요한 데이터만 뽑아서 별도의 API 스펙을 정의하고 그에 맞는 객체를 
		  만들어서 반환해야 한다. 

  @ModelAttribute vs @RequestBody
    - HTTP 요청 파라미터를 처리하는 @ModelAttribute는 각각의 필드 단위로 
	  세밀하게 적용된다. 그래서 특정 필드에 타입이 맞지 않는 오류가 발생해도 
	  나머지 필드는 정상 처리할 수 있었다. 
	  HttpMessageConverter는 @ModelAttribute와 다르게 각각의 
	  필드 단위로 적용되는 것이 아니라, 전체 객체 단위로 적용된다. 
	  따라서 메시지 컨버터의 작동이 성공해서 Item 객체를 만들어야 @Valid, 
	  @Validated가 적용된다. 
	
	  - @ModelAttribute는 필드 단위로 정교하게 바인딩이 적용된다.
	    특정 필드가 바인딩 되지 않아도 나머지 필드는 정상 바인딩 되고, 
		Validator를 사용한 검증도 적용할 수 있다. 
	  - @RequestBody는 HttpMessageConverter 단계에서 
	    JSON 데이터를 객체로 변경하지 못하면 이후 단계 자체가 
		진행되지 않고 예외가 발생한다. 컨트롤러도 호출되지 않고, 
		Validator도 적용할 수 없다. 
	
	참고 
	  - HttpMessageConverter 단계에서 실패하면 예외가 발생한다. 
	    예외 발생시 원하는 모양으로 예외를 처리하는 방법은 예외 처리 부분에서 
		다룬다. 
```

## 로그인 처리1 - 쿠키, 세션 

### 로그인 요구사항
```
  홈 화면 - 로그인 전 
    - 회원가입
	- 로그인 
  홈 화면 - 로그인 후 
    - 본인 이름(누구님 환영합니다.)
	- 상품 관리 
	- 로그 아웃 
  보안 요구사항 
    - 로그인 사용자만 상품에 접근하고 관리할 수 있음 
	- 로그인 하지 않은 사용자가 상품 관리에 접근하면 로그인 화면으로 이동 
  회원 가입, 상품관리 
```

### 프로젝트 생성 
```
  패키지 구조 설계 
    
	package 구조 
	  - hello.login
	    - domain 
		  - item 
		  - member
		  - login
		- web 
		  - item 
		  - member 
		  - login 
	
	도메인이 가장 중요하다. 
	  - 도메인 = 화면, UI, 기술 인프라 등등의 영역은 제외한 시스템이 구현해야하는 
	    핵심 비즈니스 업무 영역을 말함 
	  - 향후 web을 다른 기술로 바꾸어도 도메인은 그대로 유지할 수 있어야 한다. 
	    이렇게 하려면 web은 domain을 알고있지만 domain은 web을 모르도록 
		설계해야 한다. 이것을 web은 domain에 의존하지만, domain은 
		web에 의존하지 않는다고 표현한다. 예를 들어 web 패키지 모두 
		삭제해도 domain에는 전혀 영향이 없도록 의존관계를 설계하는 것이 
		중요하다. 반대로 이야기하면 domain은 web을 참조하면 안된다. 
```

### 홈 화면 
```
  홈 화면을 개발하자 
  HomeController - home() 수정 
  templates/home.html 추가 
```

### 회원 가입 
```
  Member 
  MemberRepository
  MemberController
  
  회원가입 뷰 템플릿 
    - templates/members/addMemberForm.html

  실행하고 로그로 결과를 확인하자 
  
  회원용 테스트 데이터 추가 
    - 편의상 테스트용 회원 데이터를 추가하자.
	  - loginId: test
	  - password: test!
	  - name: 테스터 
``` 

### 로그인 기능 
```
  로그인 기능을 개발해보자. 지금은 로그인 ID, 비밀번호를 입력하는 부분에 집중하자 
  
  LoginService 
    - 로그인의 핵심 비즈니스 로직은 회원을 조회한 다음에 파라미터로 넘어온 
	  password와 비교해서 같으면 회원을 반환하고, 만약 password가 다르면 
	  null을 반환한다. 

  LoginForm
  LoginController
    - 로그인 컨트롤러는 로그인 서비스를 호출해서 로그인에 성공하면 홈 화면으로 이동하고, 
	  로그인에 실패하면 bindingResult.reject()를 사용해서 글로벌 오류(ObjectError)를
	  생성한다. 그리고 정보를 다시 입력하도록 로그인 폼을 뷰 템플릿으로 사용한다. 

  로그인 폼 뷰 템플릿 
  templates/login/loginForm.html
    - 로그인 폼 뷰 템플릿에는 특별한 코드는 없다. loginId, passwd가 틀리면 글로벌 
	  오류가 나타난다. 

  실행 
    - 실행해보면 로그인이 성공하면 홈으로 이동하고, 로그인에 실패하면 "아이디 비밀번호가 
	  맞지 않습니다."라는 경고와 함께 로그인 폼이 나타난다. 
	- 그런데 아직 로그인이 되면 홈 화면에 고객 이름이 보여야 한다는 요구사항을 만족하지 
	  못한다. 로그인의 상태를 유지하면서, 로그인에 성공한 사용자는 홈 화면에 접근시 
	  고객의 이름을 보여주려면 어떻게 해야할까?
```

### 로그인 처리하기 - 쿠기 사용 
```
  참고 
    - 여기서는 여러분이 쿠키의 기본 개념을 이해하고 있다고 가정한다. 쿠키에 대해서는 
	  모든 개발자를 위한 HTTP 기본 지식 강의를 참고하자. 혹시 잘 생각이 안나면 쿠키
	  관련 내용을 꼭! 복습하고 돌아오자. 
	  
  쿠기를 사용해서 로그인, 로그아웃 기능을 구현해보자. 
  
  로그인 상태 유지하기 
    - 로그인의 상태를 어떻게 유지할 수 있을까?
	  HTTP 강의에서 일부 설명했지만, 쿼리 파라미터를 계속 유지하면서 보내는 것은 
	  매우 어렵고 번거로운 작업이다. 쿠키를 사용해보자 

  쿠키 
    - 서버에서 로그인에 성공하면 HTTP 응답에 쿠키를 담아서 브라우저에 전달하자. 
	  그러면 브라우저는 앞으로 해당 쿠키를 지속해서 보내준다. 
	
	- 쿠키에는 영속 쿠키와 세션 쿠키가 있다 
	  - 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지 
	  - 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시 까지만 유지 
	  
	- 브라우저 종료시 아웃되길 기대하므로, 우리에게 필요한 것은 세션 쿠키이다. 

  LoginController - login()
    - 로그인 성공시 세션 쿠키를 생성하자. 
	- 로그인에 성공하면 쿠키를 생성하고 HttpServletResponse에 담는다. 쿠키 이름은 
	  memberId이고, 값은 회원의 id를 담아둔다. 웹 브라우저는 종료 전까지 회원의 id를 
	  서버에 계속 보내줄 것이다. 
	
	실행 
	  - 크롬 브라우저를 통해 HTTP 응답 헤더에 쿠키가 추가된 것을 확인할 수 있다. 

  이제 요구사항에 맞추어 로그인에 성공하면 로그인 한 사용자 전용 홈 화면을 보여주자 
  홈 - 로그인 처리
    - 기존 home()에 있는 @GetMapping("/")은 주석 처리하자. 
	- @CookieValue를 사용하면 편리하게 쿠키를 조회할 수 있다. 
	- 로그인 하지 않은 사용자도 홈에 접근할 수 있기 때문에 required = false를 사용한다. 
	
	로직 분석 
	  - 로그인 쿠키(memberId)가 없는 사용자는 기존 home으로 보낸다. 추가로 
	    로그인 쿠키가 있어도 회원이 없으면 home으로 보낸다.
	  - 로그인 쿠키(memberId)가 있는 사용자는 로그인 사용자 전용 홈 화면인 
	    loginHome으로 보낸다. 추가로 홈 화면에 회원 관련 정보도 출력해야 해서 
		member 데이터도 모델에 담아서 전달한다. 

  홈 - 로그인 사용자 전용 
    - templates/loginHome.html
	  - th:text="|로그인: ${member.name}|"
	    - 로그인에 성공한 사용자 이름을 출력한다 
	  - 상품 관리, 로그아웃 버튼을 노출한다. 
	
	실행 
	  - 로그인에 성공하면 사용자 이름이 출력되면서 상품 관리, 로그아웃 버튼을 확인할 수 있다. 
	    로그인에 성공시 세션 쿠키가 지속해서 유지되고, 웹 브라우저에서 서버에 요청시 
		memberId 쿠키를 계속 보내준다. 

  로그아웃 기능 
    - 이번에는 로그아웃 기능을 만들어보자. 로그아웃 방법은 다음과 같다. 
	  - 세션 쿠키 이므로 웹 브라우저 종료시 
	  - 서버에서 해당 쿠키의 종료 날짜를 0으로 지정 
	
	- LoginController - logout 기능 추가
	  - 로그아웃도 응답 쿠키를 생성하는데 Max-Age=0을 확인할 수 있다. 해당 쿠키는 
	    즉시 종료된다.
``` 

### 쿠키와 보안 문제 
```
  쿠키를 사용해서 로그인 ID를 전달해서 로그인을 유지할 수 있었다. 그런데 여기에는 심각한 
  보안 문제가 있다. 
  
  보안 문제 
    - 쿠키 값은 임의로 변경할 수 있다. 
	  - 클라이언트가 쿠키를 강제로 변경하면 다른 사용자가 된다. 
	  - 실제 웹 브라우저 개발자모드 -> Application -> Cookie 변경으로 확인 
	  - Cookie: memberId=1 -> Cookie: memberId=2(다른 사용자의 이름이 보임)
	- 쿠키에 보관된 정보는 훔쳐갈 수 있다. 
	  - 만약 쿠키에 개인정보나, 신용카드 정보가 있다면?
	  - 이 정보가 웹 브라우저에도 보관되고, 네트워크 요청마다 계속 클라이언트에서 
	    서버로 전달된다. 
	  - 쿠키의 정보가 나의 로컬 PC에서 털릴 수 도 있고, 네트워크 전송 구간에서 털릴 수도 있다. 
	- 해커가 쿠키를 한번 훔쳐가면 평생 사용할 수 있다. 
	  - 해커가 쿠키를 훔쳐가서 그 쿠키로 악의적인 요청을 계속 시도할 수 있다. 

  대안 
    - 쿠키에 중요한 값을 노출하지 않고, 사용자 별로 예측 불가능한 임의의 토큰(랜덤 값)을 
	  노출하고, 서버에서 토큰과 사용자 id를 매핑해서 인식한다. 그리고 서버에서 토큰을 
	  관리한다. 
	- 토큰은 해커가 임의이 값을 넣어도 찾을 수 없도록 예상 불가능 해야 한다. 
	- 해커가 토큰을 털어가도 시간이 지나면 사용할 수 없도록 서버에서 해당 토큰의 만료시간을 
	  짧게(예:30분)유지한다. 또는 해킹이 의심되는 경우 서버에서 해당 토근을 강제로 
	  제거하면 된다. 
```

### 로그인 처리하기 - 세션 동작 방식 
```
  목표 
    - 앞서 쿠키에 중요한 정보를 보관하는 방법은 여러가지 보안 이슈가 있었다. 이 문제를 
	  해결하려면 결국 중요한 정보를 모두 서버에 저장해야 한다. 그리고 클라이언트와 서버는 
	  추정 불가능한 임의의 식별자 값으로 연결해야 한다. 
	  
	  이렇게 서버에 중요한 정보를 보관하고 연결을 유지하는 방법을 세션이라 한다. 

  세션 동작 방식 
    - 세션을 어떻게 개발할지 먼저 개념을 이해해보자. 
	
	로그인 
	  - 사용자가 loginId, password 정보를 전달하면 서버에서 해당 사용자가 맞는지 확인한다.
	
	세션 생성 
	  - 세션 ID를 생성하는데, 추정 불가능해야 한다. 
	  - UUID는 추정이 불가능하다.
	    - Cookie: mySessionId=zz0101xx-bab9-4b92-9b32-dadb280f4b61
	  - 생성된 세션 ID와 세션에 보관할 값(memberA)을 서버의 세션 저장소에 보관한다. 
	
	세션id를 응답 쿠키로 전달 
	
	클라이언트와 서버는 결국 쿠키로 연결이 되어야 한다. 
	  - 서버는 클라이언트에 mySessionId라는 이름으로 세션ID만 쿠키에 담아서 전달한다. 
	  - 클라이언트는 쿠키 저장소에 mySessionId 쿠키를 보관한다. 
	
	중요 
	  - 여기서 중요한 포인트는 회원과 관련된 정보는 전혀 클라이언트에 전달하지 않는다는 것이다. 
	  - 오직 추정 불가능한 세션 ID만 쿠키를 통해 클라이언트에 전달한다. 
	
	클라이언트의 세션id 쿠키 전달 
	  - 클라이언트는 요청시 항상 mySessionId 쿠키를 전달한다. 
	  - 서버에서는 클라이언트가 전달한 mySessionId 쿠키 정보로 세션 저장소를 조회해서 
	    로그인시 보관한 세션 정보를 사용한다. 

  정리 
    - 세션을 사용해서 서버에서 중요한 정보를 관리하게 되었다. 덕분에 다음과 같은 보안 문제들을 
	  해결할 수 있다. 
	  - 쿠키 값을 변조 가능 -> 예상 불가능한 복잡한 세션ID를 사용한다. 
	  - 쿠키에 보관하는 정보는 클라이언트 해킹시 털릴 가능성이 있다. -> 세션ID가 털려도 
	    여기에는 중요한 정보가 없다. 
	  - 쿠키 탈취 후 사용 -> 해커가 토큰을 털어가도 시간이 지나면 사용할 수 없도록 서버에서 
	    세션의 만료시간을 짧게(예:30분) 유지한다. 또는 해킹이 의심되는 경우 서버에서 
		해당 세션을 강제로 제거하면 된다. 
```

### 로그인 처리하기 - 세션 직접 만들기 
```
  세션을 직접 개발해서 적용해보자. 
  세션 관리는 크게 다음 3가지 기능을 제공하면 된다. 
    - 세션 생성 
	  - sessionId 생성(임의의 추정 불가능한 랜덤 값)
	  - 세션 저장소에 sessionId와 보관할 값 저장 
	  - sessionId로 응답 쿠키를 생성해서 클라이언트에 전달 
	- 세션 조회 
	  - 클라이언트가 요청한 sessionId 쿠키의 값으로, 세션 저장소에 보관한 값 조회 
	- 세션 만료 
	  - 클라이언트가 요청한 sessionId 쿠키의 값으로, 세션 저장소에 보관한 
	    sessionId와 값 제거 

  SessionManager - 세션 관리
    - 로직은 어렵지 않아서 쉽게 이해가 될 것이다. 
	  - @Component: 스프링 빈으로 자동 등록한다. 
	  - ConcurentHashMap: HashMap은 동시 요청에 안전하지 않다. 
	    동시 요청에 안전한 ConcurentHashMap를 사용했다. 

  SessionManagerTest - 테스트
    - 간단하게 테스트를 진행해보자. 여기서는 HttpServletRequest,
	  HttpServletResponse 객체를 직접 사용할 수 없기 때문에 테스트에서 
	  비슷한 역할을 해주는 가짜 MockHttpServletRequest,
	  MockHttpServletResponse를 사용했다. 
``` 

### 로그인 처리하기 - 직접 만든 세션 적용 
```
  지금까지 개발한 세션 관리 기능을 실제 웹 애플리케이션에 적용해보자. 
  
  LoginController - loginV2()
    - 기존 login()의 @PostMapping("/login")주석 처리 
	- private final SessionManager sessionManager; 주입 
	- sessionManager.createSession(loginMember, response);
	  로그인 성공시 세션을 등록한다. 세션에 loginMember를 저장해두고, 
	  쿠키도 함께 발행한다.

  LoginController - logoutV2()
    - 기존 logout()의 @PostMapping("/logout") 주석 처리 
	  로그 아웃시 해당 세션의 정보를 제거한다. 

  HomeController - homeLoginV2()
    - private final SessionManager sessionManager; 주입 
	- 기존 homeLogin()의 @GetMapping("/") 주석 처리 
	
	- 세션 관리자에서 저장된 회원 정보를 조회한다. 만약 회원 정보가 없으면, 
	  쿠키나 세션이 없는 것 이므로 로그인 되지 않은 것으로 처리한다. 

  정리 
    - 이번 시간에는 세션과 쿠키의 개념을 명확하게 이해하기 위해서 직접 만들어보았다. 
	  사실 세션이라는 것이 뭔가 특별한 것이 아니라 단지 쿠키를 사용하는데, 서버에서 
	  데이터를 유지하는 방법일 뿐이라는 것을 이해했을 것이다. 
	- 그런데 프로젝트마다 이러한 세션 개념을 직접 개발하는 것은 상당히 불편할 것이다. 
	  그래서 서블릿도 세션 개념을 지원한다. 
	- 이제 직접 만드는 세션 말고, 서블릿이 공식 지원하는 세션을 알아보자. 서블릿이 
	  공식 지원하는 세션은 우리가 직접 만든 세션과 동작 방식이 거의 같다. 추가로 
	  세션을 일정시간 사용하지 않으면 해당 세션을 삭제하는 기능을 제공한다. 
``` 

### 로그인 처리하기 - 서블릿 HTTP 세션1 
```
  세션이라는 개념은 대부분의 웹 애플리케이션에 필요한 것이다. 어쩌면 웹이 등장하면서 부터 
  나온 문제이다. 서블릿은 세션을 위해 HttpSession이라는 기능을 제공하는데, 지금까지 
  나온 문제들을 해결해준다. 우리가 직접 구현한 세션의 개념이 이미 구현되어 있고, 더 잘 
  구현되어 있다. 
  
  HttpSession 소개 
    - 서블릿이 제공하는 HttpSession도 결국 우리가 직접 만든 SessionManager와 
	  같은 방식으로 동작한다. 서블릿을 통해 HttpSession을 생성하면 다음과 같은 
	  쿠키를 생성한다. 쿠키 이름이 JESSIONID이고, 값은 추정 불가능한 랜덤 값이다. 
	  - Cookie: JSESSIONID=5B78E23B513F50164D6FDD8C97B0AD05

  HttpSession 사용 
    - 서블릿이 제공하는 HttpSession을 사용하도록 개발해보자. 

  SessionConst
    - HttpSession에 데이터를 보관하고 조회할 때, 같은 이름이 중복 되어 사용되므로, 
	  상수를 하나 정의했다. 

  LoginController - loginV3()
    - 기존 loginV2()의 @PostMapping("/login") 주석 처리 
	
	- 세션 생성과 조회 
	  - 세션을 생성하려면 request.getSession(true)를 사용하면 된다. 
	    public HttpSession getSession(boolean create);
	
	  - 세션의 create 옵션에 대해 알아보자. 
	    - request.getSession(true)
		  - 세션이 있으면 기존 세션을 반환한다. 
		  - 세션이 없으면 새로운 세션을 생성해서 반환한다. 
		- request.getSession(false)
		  - 세션이 있으면 기존 세션을 반환한다. 
		  - 세션이 없으면 새로운 세션을 생성하지 않는다. null을 반환한다. 
		- request.getSession()
		  - 신규 세션을 생성하는 request.getSession(true)와 동일하다. 
		  
	- 세션에 로그인 회원 정보 보관 
	  - session.setAttribute(SessionConst.LOGIN_MEMBER, loginMember);
	  - 세션에 데이터를 보관하는 방법은 request.setAttribute(...)와 비슷하다. 
	    하나의 세션에 여러 값을 저장할 수 있다. 

  LoginController - logoutV3()
    - 기존 logoutV2()의 @PostMapping("/logout") 주석 처리 
	- session.invalidate(): 세션을 제거한다. 

  HomeController - homeLoginV3()
    - 기존 homeLoginV2()의 @GetMapping("/") 주석 처리 
	- request.getSession(false)
	  - request.getSession()을 사용하면 기본 값이 create: true 이므로, 
	    로그인 하지 않을 사용자도 의미없는 세션이 만들어진다. 따라서 세션을 찾아서 
		사용하는 시점에는 create: false 옵션을 사용해서 세션을 생성하지 
		않아야 한다. 
	- session.getAttribute(SessionConst.LOGIN_MEMBER)
	  - 로그인 시점에 세션에 보관한 회원 객체를 찾는다. 

  실행 
    - JSESSIONID 쿠키가 적절하게 생성되는 것을 확인하자. 
```

### 로그인 처리하기 - 서블릿 HTTP 세션2
```
  @SessionAttribute 
    - 스프링은 세션을 더 편리하게 사용할 수 있도록 @SessionAttribute를 지원한다. 
	- 이미 로그인 된 사용자를 찾을 때는 다음과 같이 사용하면 된다. 참고로 이 기능은 
	  세션을 생성하지 않는다. 
	  - @SessionAttribute(name="loginMember", required=false) Member loginMember

  HomeController - homeLoginV3Spring()
    - homeLoginV3()의 @GetMapping("/") 주석 처리 
	- 세션을 찾고, 세션에 들어있는 데이터를 찾는 번거로운 과정이 스프링이 한번에 
	  편리하게 처리해주는 것을 확인할 수 있다. 

  TrackingModes 
    - 로그인을 처음 시도하면 URL이 다음과 같이 jsessionid를 포함하고 있는 것을 확인할 수 있다. 
	  - http://localhost:8080/;jsessionid=F59911518B921DF62D09F0DF8F83F872
	  
	- 이것은 웹 브라우저가 쿠키를 지원하지 않을 때 쿠키 대신 URL을 통해서 세션을 유지하는 방법이다. 
	  이 방법을 사용하려면 URL에 이 값을 계속 포함해서 전달해야 한다. 타임리프 같은 템플릿은 
	  엔진을 통해서 링크를 걸면 jsessionid를 URL에 자동으로 포함해준다. 서버 입장에서 
	  웹 브라우저가 쿠키를 지원하는지 하지 않는지 최초에는 판단하지 못하므로, 쿠키 값도 전달하고, 
	  URL에 jsessionid도 함께 전달한다. 
	
	- URL 전달 방식을 끄고 항상 쿠키를 통해서만 세션을 유지하고 싶으면 다른 옵션을 넣어주면 된다. 
	  이렇게 하면 URL에 jsessionid가 노출되지 않는다. 
	  
	  application.properties
	    - server.servlet.session.tracking-modes=cookie
```

### 세션 정보와 타임아웃 설정 
```
  세션 정보 확인 
    - 세션이 제공하는 정보들을 확인해보자 

  SessionInfoController 
    - sessionId: 세션Id, JSESSIONID의 값이다. 예) 34B14F008AA3527C9F8ED620EFD7A4E1
	- maxInactiveInterval: 세션의 유효 시간. 예) 1800초, (30분)
	- createTime: 세션 생성일시 
	- lastAccessedTime: 세션과 연결된 사용자가 최근에 서버에 접근한 시간, 
	  클라이언트에서 서버로 sessionId(JSESSIONID)를 요청한 경우에 갱신된다. 
	- isNew: 새로 생성된 세션인지, 아니면 이미 과거에 만들어졌고, 클라이언트에서 
	  서버로 sessionId(JSESSIONID)를 요청해서 조회된 세션인지 여부 

  세션 타임아웃 설정 
    - 세션은 사용자가 로그아웃을 직접 호출해서 session.invalidate()가 호출 되는 경우에 
	  삭제된다. 그런데 대부분의 사용자는 로그아웃을 선택하지 않고, 그냥 웹 브라우저를 종료한다. 
	  문제는 HTTP가 비 연결성(ConnectionLess)이므로 서버 입장에서는 해당 사용자가 
	  웹 브라우저를 종료한 것인지 아닌지를 인식할 수 없다. 따라서 서버에서 세션 데이터를 
	  언제 삭제해야 하는지 판단하기가 어렵다. 
	  
	- 이 경우 남아 있는 세션을 무한정 보관하면 다음과 같은 문제가 발생할 수 있다. 
	  - 세션과 관련된 쿠키(JSESSIONID)를 탈취 당했을 경우 오랜 시간이 지나도 
	    해당 쿠키로 악의적인 요청을 할 수 있다. 
	  - 세션은 기본적으로 메모리에 생성된다. 메모리의 크기가 무한하지 않기 때문에 
	    꼭 필요한 경우만 생성해서 사용해야 한다. 10만명의 사용자가 로그인하면 
		10만개의 세션이 생성되는 것이다. 

  세션의 종료 시점 
    - 세션의 종료 시점을 어떻게 정하면 좋을까? 가장 단순하게 생각해보면, 세션 생성 
	  시점으로부터 30분 정도로 잡으면 될 것 같다. 그런데 문제는 30분이 지나면 
	  세션이 삭제되기 때문에, 열심히 사이트를 돌아다니다가 또 로그인을 해서 세션을 
	  생성해야 한다. 그러니까 30분 마다 계속 로그인해야 하는 번거로움이 발생한다. 
	- 더 나은 대안은 세션 생성 시점이 아니라 사용자가 서버에 최근 요청한 시간을 
	  기준으로 30분 정도를 유지해주는 것이다. 이렇게 하면 사용자가 서비스를 
	  사용하고 있으면, 세션의 생존 시간이 30분으로 계속 늘어나게 된다. 
	  따라서 30분 마다 로그인해야 하는 번거로움이 사라진다. HttpSession은 
	  이 방식을 사용한다. 

  세션 타임아웃 설정 
    - 스프링 부트로 글로벌 설정 
	  - application.properties
	    - server.servlet.session.timeout=60, 60초, 기본은 1800(30분)
		  (글로벌 설정은 분 단위로 설정해야 한다. 60(1분), 120(2분),...)
	
	- 특정 세션 단위로 시간 설정 
	  - session.setMaxInactiveInterval(1800) //1800초 
	
  세션 타임아웃 발생 
    - 세션의 타임아웃 시간은 해당 세션과 관련된 JSESSIONID를 전달하는 HTTP 요청이 
	  있으면 현재 시간으로 다시 초기화 된다. 이렇게 초기화 되면 세션 타임아웃으로 설정한 
	  시간동안 세션을 추가로 사용할 수 있다. 
	  session.getLastAccessedTime(): 최근 세션 접근 시간 
	
	- LastAccessedTime 이후로 timeout 시간이 지나면, WAS가 내부에서 
	  해당 세션을 제거한다. 

  정리 
    - 서블릿의 HttpSession이 제공하는 타임아웃 기능 덕분에 세션을 안전하고 편리하게 
	  사용할 수 있다. 실무에서 주의할 점은 세션에는 최소한의 데이터만 보관해야 한다는 점이다. 
	  보관한 데이터 용량 * 사용자 수로 세션의 메모리 사용량이 급격하게 늘어나서 장애로 
	  이어질 수 있다. 추가로 세션의 시간을 너무 길게 가져가면 메모리 사용이 계속 
	  누적 될 수 있으므로 적당한 시간을 선택하는 것이 필요하다. 기본이 30분이라는 
	  것을 기준으로 고민하면 된다. 
```

## 로그인 처리2 - 필터, 인터셉터 

### 서블릿 필터 - 소개 
```
  공통 관심 사항 
    - 요구사항을 보면 로그인 한 사용자만 상품 관리 페이지에 들어갈 수 있어야 한다. 
	  앞에서 로그인을 하지 않은 사용자에게는 상품 관리 버튼이 보이지 않기 때문에 
	  문제가 없어 보인다. 그런데 문제는 로그인 하지 않은 사용자도 다음 URL을 
	  직접 호출하면 상품 관리 화면에 들어갈 수 있다는 점이다. 
	  
	- 상품 관리 컨트롤러에서 로그인 여부를 체크하는 로직을 하나하나 작성하면 
	  되겠지만, 등록, 수정, 삭제, 조회 등등 상품관리의 모든 컨트롤러에서 
	  로직에 공통으로 로그인 여부를 확인해야 한다. 더 큰 문제는 향후 
	  로그인과 관련된 로직이 변경될 때 이다. 작성한 모든 로직을 다 
	  수정해야 할 수 있다. 
	
	- 이렇게 애플리케이션 여러 로직에서 공통으로 관심이 있는 것을 공통 관심사 
	  (cross-cutting-concern)라고 한다. 여기서는 등록, 수정, 삭제, 
	  조회 등등 여러 로직에서 공통으로 인증에 대해서 관심을 가지고 있다.
	
	- 이러한 공통 관심사는 스프링의 AOP로도 해결할 수 있지만, 웹과 관련된 
	  공통 관심사는 지금부터 설명할 서블릿 필터 또는 스프링 인터셉터를 
	  사용하는 것이 좋다. 웹과 관련된 공통 관심사를 처리할 때는 HTTP의 
	  헤더나 URL의 정보들이 필요한데, 서블릿 필터나 스프링 인터셉터는 
	  HttpServletRequest를 제공한다. 

  서블릿 필터 소개 
    - 필터는 서블릿이 지원하는 수문장이다. 필터의 특성은 다음과 같다. 
	
	필터 흐름 
	  - HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 컨트롤러 
	  
	  - 필터를 적용하면 필터가 호출 된 다음에 서블릿이 호출된다. 그래서 
	    모든 고객의 요청 로그를 남기는 요구사항이 있다면 필터를 사용하면 된다. 
		참고로 필터는 특정 URL 패턴에 적용할 수 있다. /* 이라고 하면 
		모든 요청에 필터가 적용된다. 
		참고로 스프링을 사용하는 경우 여기서 말하는 서블릿은 스프링의 
		디스패처 서블릿으로 생각하면 된다. 
	
	필터 제한 
	  - HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 컨트롤러 //로그인 사용자
	  - HTTP 요청 -> WAS -> 필터(적절하지 않은 요청이라 판단, 서블릿 호출X) //비 로그인 사용자
	  
	  - 필터에서 적절하지 않은 요청이라고 판단하면 거기에서 끝을 낼 수도 있다. 
	    그래서 로그인 여부를 체크하기에 딱 좋다. 
	
	필터 체인 
	  - HTTP 요청 -> WAS -> 필터1 -> 필터2 -> 필터3 -> 서블릿 -> 컨트롤러 
	  
	  - 필터는 체인으로 구성되는데, 중간에 필터를 자유롭게 추가할 수 있다. 예를 들어서 
	    로그를 남기는 필터를 먼저 적용하고, 그 다음에 로그인 여부를 체크하는 필터를 
		만들 수 있다. 
	
	필터 인터페이스 
	  - 필터 인터페이스를 구현하고 등록하면 서블릿 컨테이너가 필터를 싱글톤 객체로 생성하고, 
	    관리한다 
		- init()
		  - 필터 초기화 메서드, 서블릿 컨테이너가 생성될 때 호출된다.
		- doFilter()
		  - 고객의 요청이 올 때 마다 해당 메서드가 호출된다. 필터의 로직을 구현하면 된다. 
		- destroy()
		  - 필터 종료 메서드, 서블릿 컨테이너가 종료될 때 호출한다. 
```

### 서블릿 필터 - 요청 로그 
```
  필터가 정말 수문장 역할을 잘 하는지 확인하기 위해 가장 단순한 필터인, 모든 요청을 로그로 
  남기는 필터를 개발하고 적용해보자. 
  
  LogFilter - 로그 필터 
    - public class LogFilter implements Filter {}
	  - 필터를 사용하려면 필터 인터페이스를 구현해야 한다. 
	- doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
	  - HTTP 요청이 오면 doFilter가 호출된다. 
	  - ServletRequest request는 HTTP 요청이 아닌 경우까지 고려해서 만든 인터페이스이다. 
	    HTTP를 사용하면 HttpServletRequest httpRequest = (HttpServletRequest) request;
		와 같이 다운 캐스팅 하면 된다. 
	- String uuid = UUID.randomUUID().toString();
	  - HTTP 요청을 구분하기 위해 요청 당 임의의 uuid를 생성해둔다. 
	- log.info("REQUEST [{}] [{}]", uuid, requestURI);
	  - uuid와 requestURI를 출력한다. 
	- chain.doFilter(request, response);
	  - 이 부분이 가장 중요하다. 다음 필터가 있으면 필터를 호출하고, 필터가 없으면 
	    서블릿을 호출한다. 만약 이 로직을 호출하지 않으면 다음 단계로 진행되지 않는다. 

  WebConfig - 필터 설정
    - 필터를 등록하는 방법은 여러가지가 있지만, 스프링 부트를 사용한다면 FilterRegistrationBean을 
	  사용해서 등록하면 된다. 
	  - setFilter(new LogFilter())
	    - 등록할 필터를 지정한다. 
	  - setOrder(1)
	    - 필터는 체인으로 동작한다. 따라서 순서가 필요하다. 낮을 수록 먼저 동작한다. 
	  - addUrlPatterns("/")
	    - 필터를 적용할 URL 패턴을 지정한다. 한번에 여러 패턴을 지정할 수 있다. 
	
	참고 
	  - URL 패턴에 대한 툴은 필터도 서블릿과 동일하다. 자세한 내용을 서블릿 
	    URL 패턴으로 검색해보자. 
	  - @ServletComponentScan @WebFilter(filterName="logFilter", urlPatterns="/*")로 
	    필터 등록이 가능하지만 필터 순서 조절이 안된다. 따라서 FilterRegistrationBean을 사용하자. 

  실행 
    - 필터를 등록할 때 urlPatterns를 /*로 등록했기 때문에 모든 요청에 해당 필터가 적용된다.
	
	참고 
	  - 실무에서 HTTP 요청시 같은 요청의 로그에 모두 같은 식별자를 자동으로 남기는 
	    방법은 logback mdc로 검색해보자. 
```