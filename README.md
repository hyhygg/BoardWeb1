# study_spring
교재: 스프링 퀵 스타트 (채규태) 📗 

210730
MVC 프레임워크 개발
- MVC 변환 이유 : JSP파일에서 Controller 로직에 해당하는 자바 코드를 제거하기 위함
- Controller 로직 : 사용자 입력 정보 추출, DB 연동 처리, 화면 네비게이션 같은 자바 코드 의미
- 남은 자바 코드 제거 -> EL(표현식 대체 ex.${}) / JSTL 이용(태그 형태로 대체 ex.for루프 -> <c:forEach>)

210801
Spring MVC 구조, 적용
- 가장 중요한 요소 : 모든 클라이언트의 요청을 가장 먼저 받아들이는 DispatcherServlet / 스프링 프레임워크에서 제공
- 클라이언트 요청 > DispatcherServlet객체 생성 > 스프링 컨테이너 구동 > HandlerMapping, Controller, ViewResolver객체 생성(<bean>등록)
- 리턴타입 String -> ModelAndView : Model과 View 정보를 모두 저장하여 리턴할 때 사용
- 인코딩 처리 위한 web.xml 필터 등록
- ViewResolver : WEB-INF 폴더로 이동한 JSP 파일들은 절대 클라이언트 브라우저에 접근X > 직접적인 JSP 호출 차단,
  'redirect:' : ViewResolver 설정되어 있더라도 무시하고 리다이렉트
  
210804
어노테이션 게시판 기능 구현
- @RequestMapping : 클라이언트의 요청 방식(GET/POST)에 따라 수행될 메소드 다르게 설정 가능
- @RequestParam : Command 클래스에 없는 파라미터 정보 추출 가능/ getParameter()메소드와 같은 기능의 어노테이션(HttpServletRequest 제공)
- @ModelAttribute : Command 객체의 이름 변경/ View에서 사용할 데이터를 설정,
  @RequestMapping 적용 메소드보다 먼저 호출, @ModelAttribute 메소드 실행 결과 리턴 객체 > 자동으로 Model 저장 >  View 페이지에서 사용 가능
- @SessionAttributes : 수정 작업 처리 시 유용/ ex.@SessionAttirbutes("board") : Model에 "board"로 저장된 데이터 있으면 그 데이터르 세션(HttpSession)에도 자동으로 저장하라는 설정,
  사용자가 입력한 수정 정보값만 새롭게 할당, 나머지느 세션에 저장된 데이터가 유지
                                                             
