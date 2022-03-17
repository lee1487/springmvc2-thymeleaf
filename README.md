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