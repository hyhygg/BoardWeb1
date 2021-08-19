# study_spring
교재: 스프링 퀵 스타트 (채규태) 📗 

MVC 프레임워크 개발
- MVC 변환 이유 : JSP파일에서 Controller 로직에 해당하는 자바 코드를 제거하기 위함
- Controller 로직 : 사용자 입력 정보 추출, DB 연동 처리, 화면 네비게이션 같은 자바 코드 의미
- 남은 자바 코드 제거 -> EL(표현식 대체 ex.${}) / JSTL 이용(태그 형태로 대체 ex.for루프 -> <c:forEach>)

Spring MVC 구조, 적용
- 가장 중요한 요소 : 모든 클라이언트의 요청을 가장 먼저 받아들이는 DispatcherServlet / 스프링 프레임워크에서 제공
- 클라이언트 요청 > DispatcherServlet객체 생성 > 스프링 컨테이너 구동 > HandlerMapping, Controller, ViewResolver객체 생성(<bean>등록)
- 리턴타입 String -> ModelAndView : Model과 View 정보를 모두 저장하여 리턴할 때 사용
- 인코딩 처리 위한 web.xml 필터 등록
- ViewResolver : WEB-INF 폴더로 이동한 JSP 파일들은 절대 클라이언트 브라우저에 접근X > 직접적인 JSP 호출 차단,
  'redirect:' : ViewResolver 설정되어 있더라도 무시하고 리다이렉트

어노테이션 게시판 기능 구현
- @RequestMapping : 클라이언트의 요청 방식(GET/POST)에 따라 수행될 메소드 다르게 설정 가능
- @RequestParam : Command 클래스에 없는 파라미터 정보 추출 가능/ getParameter()메소드와 같은 기능의 어노테이션(HttpServletRequest 제공)
- @ModelAttribute : Command 객체의 이름 변경/ View에서 사용할 데이터를 설정,
  @RequestMapping 적용 메소드보다 먼저 호출, @ModelAttribute 메소드 실행 결과 리턴 객체 > 자동으로 Model 저장 >  View 페이지에서 사용 가능
- @SessionAttributes : 수정 작업 처리 시 유용/ ex.@SessionAttirbutes("board") : Model에 "board"로 저장된 데이터 있으면 그 데이터르 세션(HttpSession)에도 자동으로 저장하라는 설정,
  사용자가 입력한 수정 정보값만 새롭게 할당, 나머지느 세션에 저장된 데이터가 유지
                                                             
데이터 변환(JSON으로 변환 / XML로 변환)
- 다른 시스템과 데이터 교환 시 변환
- <mvc:annotation-driven> 설정 : 자바객체를 JSON 응답보디 변환 클래스 / XML 응답보디 변환 클래스 같이 등록해줌
- JAXB2 API는 Java6 ~ Java8까지는 지원됨 -> Java 10 부터는 자동 지원 안됨 -> 따로 설치 필요(pom.xml에 Jaxb 관련 설정 추가*) -> xml 변환 완료

Mybatis 프레임워크 환경설정 후 구현
<Mybatis 프레임워크 특징 2가지>
- 한두 줄의 자바 코드로 DB 연동 로직을 처리한다는 것,
  XML 파일에 저장된 SQL 명령어를 대신 실행하고 실행 결과를 VO 같은 자바 객체에 자동으로 매핑(데이터 맵퍼 Data Mapper)
- SQL 명령어를 자바 코드에서 분리하여 XML 파일에 따로 관리한다는 것,
  SQL 명령어에 대한 통합 관리 필요 / SQL Mapper XML 파일 : DB연동에 필요한 SQL 명령어 저장(Mybatis에서 가장 중요한 파일)
  
스프링 - MyBatis 연동
- Dynamic SQL : SQL의 재사용성과 유연성 향상
  <if> 사용 : 조건에 따른 분기 처리 / 새로운 검색 조건 추가되도 메소드 수정 필요X
