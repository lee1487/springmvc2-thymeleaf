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