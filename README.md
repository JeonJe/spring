# 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술

---
Tags: Back-End, JAVA, Spring

마지막수정시간: 2022년 2월 3일 오후 1:06
---
[https://www.inflearn.com/course/스프링-입문-스프링부트/lecture/49603?tab=curriculum](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49603?tab=curriculum)


- 1일차
    1. 간단한 웹 애플리케이션 개발
        1. 스프링 프로젝트 생성
        2. 스프링 부트로 웹 서버 실행
        3. 회원 도메인 개발
        4. 웹MVC roqkf
        5. DB 연동 - JDBC, JPA, 스프링 데이터 JPA
        6. 테스트 케이스 작성
    2. 스프링 완전 정복 로드맵
        1. 스프링 입문
        2. 스프링 핵심 원리
        3. 스프링 웹 MVC
        4. 스프링 DB 데이터 접근 기술
        5. 실전! 스프링 부트
    3. jdk 11, 인텔리J 설치 
    4. [https://start.spring.io/](https://start.spring.io/) - 스프링 부트 프로젝트 생성
        
        메이븐, 그레들 → 최신에는 Gradle 을 주로 씀 
        
        Dependencies추가  
        
        spring web, Thymeleft(HTML을 만들어주는 템플릿 엔진)
        
        생성 - > 인텔리제이에서 Open or Import 으로 build.gradle 오픈
        
        → 외부에서 라이브러리를 다운받기 때문에 네트워크가 되어야함
        
    5. main과 test 폴더가 기본적으로 있음
        
        main > java 밑에 실세 소스
        
        test는 테스트 코드 관련 소스가 들어가있음
        
        resources 는 xml 이나 설정파일 등
        
    6. build.gradle → 스프링부트에서 자동으로 설정파일을 만들어준 것 
        
        gradle ← 버전 설정, 라이브러리 땡겨옴 
        
        mavenCentral이라는 공개된 사이트에서 dependencies 를 다운로드 받으라고 명시되어있음 (repositories)
        
        .gitignore → 소스코드 외 실행파일 제외 등이 자동 설정됨
        
    7. main 밑의 java 코드에서 SpringBootApplication 실행 시 내장된 톰캣이 실행됨
        
        setting에서 gradle 실행을 IntelliJ 로 변경하면 빠르게 실행됨
        
    
    ![Untitled](https://user-images.githubusercontent.com/43032391/153753930-6f0bbd89-b79a-48b8-94b2-b4248b44c1c6.png)
    
- 2일차
    - View 환경설정
        - 템플릿엔진을 사용해서 원하는대로 변경가능
        - @GetMapping("hello") → 웹 어플리케이션에서 /hello 로 들어오면
        
        ```java
        
        // → 웹 어플리케이션에서 /hello 로 들어오면 
        
        public class HelloController {
        @GetMapping("hello")
        public String hello(Model model) {
        model.addAttribute("data", "hello!!");
        return "hello";
        //templates 폴더 하위의 hello.html을 찾아서 렌더링
        }
        //호출
        ```
        
        ![Untitled 1](https://user-images.githubusercontent.com/43032391/153753945-366432cc-0054-4888-aeaf-0a1c3ee45bb1.png)
        
- 3일차
    - 빌드하고 실행하기
        - 콘솔로 이동
            1. ./gradlew build
            2. cd build/libs
            3. java -jar hello-spring-0.0.1-SNAPSHOT.jar
            
            윈도우는 git bash로
            
            잘안되면 .gradlew clean build 로 삭제 후 빌드 진행
            
    - 스프링 웹 개발 기초
        - 정적 컨텐츠
            - 스프링부트는 정적 컨텐츠 자동으로 제공
                
                [https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-bootfeatures](https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-bootfeatures).html#boot-features-spring-mvc-static-content
                
                static 폴더에 html 파일 작성하고 URL을 입력하여 들어오면 정적 페이지가 열린다.
                
                컨트롤러가 우선순위를 가지고 찾고, 그 다음으로 내부의 resource을 찾는다
                
                ![Untitled 2](https://user-images.githubusercontent.com/43032391/153753947-e2f3dcc5-cb92-4c93-b5f8-79ef59156f1f.png)
                
        - MVC와 템플릿 엔진
            - Model , View, Controller
            - View는 화면을 그리는데 집중, Controller, Model 은 내부 비지어스에 집중
            
            ```java
            
            @GetMapping("hello-mvc")
            // 외부에서 파라미터를 받음, 모델로 담아서 view에서 render
            //파라미터에서 넘어온 키 name을 모델에 담아서 넘김
                public String helloMvc(@RequestParam("name") String name, Model model){
                    model.addAttribute("name",name);
                    return "hello-template";
                }
            
            //resources/template/hello-template.html
            <html xmlns:th="http://www.thymeleaf.org">
            <body>
            <p th:text="'hello ' + ${name}">hello! empty</p>
            </body>
            </html>
            
            //컨트롤러에서 @RequestParam(value = "name",required = true으로 바꾸고
            //URL에서 hello-mvc?name="쓰고싶은말"로 하면 name으로 넘어감
            ```
            
            ![Untitled 3](https://user-images.githubusercontent.com/43032391/153753948-29c9ed7d-3d34-4976-9f4a-b3902af6f7ef.png)
            
        - API
            
            ```java
            @GetMapping("hello-string")
            @ResponseBody
            //http body에 return 내용을 직접 넣어주겠다 선언하는 것 
            public String helloString(@RequestParam("name") String name) {
            return "hello " + name;
            }
            ```
            
            view가 없이 그대로 내려감
            
            ```java
            @GetMapping("hello-api")
            @ResponseBody
            public Hello helloApi(@RequestParam("name") String name) {
            	Hello hello = new Hello();
            	hello.setName(name);
            	return hello;
            }
            static class Hello {
            	private String name;
            	public String getName() {
            	return name;
            }
            public void setName(String name) {
            	this.name = name;
            }
            }
            ```
            
            ![Untitled 4](https://user-images.githubusercontent.com/43032391/153753950-72254136-2b47-4c71-ac21-41af6a9941ec.png)
            
            @ResponseBody에 객체가 오면 JSONConverter 가 동작하여 JSON으로 만들어서 반환
            
    - 비지니스 요구사항 정리
        
        데이터 : 회원 ID, 이름
        
        기능 : 회원 등록, 조회
        
        ![Untitled 5](https://user-images.githubusercontent.com/43032391/153753952-3619398c-f5d6-4857-b1a1-48ded5995e9e.png)
        
        ![Untitled 6](https://user-images.githubusercontent.com/43032391/153753953-5cd30646-a9bf-4faa-9ac0-2b48d9a1d5c6.png)
        
    - 테스트
        - Junit사용
        - @Test를 붙이고 메소드를 확인할 수 있음
        - Assertions.assertEquals(result,name)으로 값이 같은지 다른지 확인
        - Assertions.assertThat(member).isEqualTo(result);
        - 테스트가 끝나면 데이터를 클리어해줘야함 @AfterEach 는 각 메소드 테스트가 끝나고 호출하는 메소드
        - 테스트 코드 부터 작성하고 개발코드를 작성하는 방법을 테스트 주도 개발이라고 함 TDD
    - 회원서비스
        
        ```java
        /**
        * 회원가입
        */
        public Long join(Member member) {
        validateDuplicateMember(member); //중복 회원 검증
        memberRepository.save(member);
        return member.getId();
        }
        private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
        .ifPresent(m -> {
        throw new IllegalStateException("이미 존재하는 회원입니다.");
        });
        }
        
        /**
        * 전체 회원 조회
        */
        public List<Member> findMembers() {
        return memberRepository.findAll();
        }
        public Optional<Member> findOne(Long memberId) {
        return memberRepository.findById(memberId);
        }
        ```
        
- 4일차
    - 회원서비스테스트
    - 클래스 이름에서 ctl + shfit + T > Create New test t선택 > 선택
    - 테스트는 한글로 해도 됨 (빌드될때 실제 코드 에 포함되지 않음)
        
        ```
        //given
        테스트 검증 데이터
        //when
        조건 
        //then
        결과 
        ```
        
        ![Untitled 7](https://user-images.githubusercontent.com/43032391/153753955-733bc430-9238-41ef-a790-c6f4562d1812.png)
        ![Untitled 8](https://user-images.githubusercontent.com/43032391/153753956-1cf80666-fcf2-4ff0-be4e-11053aa4229b.png)
        
          dependency injection : 각 테스트에서 레포지토리를 나누는게 아니고 하나의 레포지토리로 사용할 수 있게끔 변경 
        
- 5일차
    - 스프링 빈과 의존관계
    
    ![Untitled 9](https://user-images.githubusercontent.com/43032391/153753957-d53c358a-1ddf-4cf1-9ffe-70d3bdd4cb5e.png)
    ![Untitled 10](https://user-images.githubusercontent.com/43032391/153753958-97221199-e2a9-4e4b-bd8b-e797a52667e7.png)
    
    멤버 컨트롤러를 통해 멤버 서비스를 등록 
    
    ![Untitled 12](https://user-images.githubusercontent.com/43032391/153753961-da7a5356-ee11-4f51-9090-44b85e6ec5db.png)
    
    기능은 없지만,  스프링 시작 시 스프링 컨테이너이라는 통이 생기는데 @Controller 라는 노테이션이 있으면 멤버컨트롤러 객체를 생성해서 스프링에 넣어 둠. 그리고 스프링이 관리 함 
    
    멤버 서비스를 가보면 순수 자바 클래스이고 스프링이 알 수 없음. 멤버 컨트롤러는  
    
    @Controller 가 붙어있어서 스프링이 알 수 있는 것.
    
    ![Untitled 12](https://user-images.githubusercontent.com/43032391/153753961-da7a5356-ee11-4f51-9090-44b85e6ec5db.png)
    
    정형화된 패턴 
    
    컨트롤러 : 컨트롤러를 통해서 외부 요청을 받음
    
    서비스 : 서비스에서 비지니스 로직을 만듬
    
    레포지토리 : 데이터 저장 
    
    연결은 Autowired
    
    ![Untitled 13](https://user-images.githubusercontent.com/43032391/153753962-752685ca-9f24-4691-9f7f-d426aa659804.png)
    
    아무곳에나 컴포넌트를 넣어도 될까?
    
    → 되지 않음. 실행되는 어플리케이션 시작지점의 하위지점에 있어야 함  (동일 + 하위 패키지)
    
    ![Untitled 14](https://user-images.githubusercontent.com/43032391/153753964-e1df3cce-da0c-49ef-8ac7-afdd4bd0b028.png)
    
- 6일차
    - 자바 코드로 직접 스프링 빈 등록하기
        
        회원 서비스와 회원 리포지토리의 @Service, @Repository, @Autowired 애노테이션을 제거하고  진행한다.
        
        ![Untitled 15](https://user-images.githubusercontent.com/43032391/153753966-8ceb741c-6762-4f71-bc3d-95c6d22fa141.png)
        
        SpringConfig라는 자바 클래스를 만들고 ‘@Configuration’ 애노테이션을 단 뒤
        
        ‘@Bean’ 을 선언하여 만들어줌 → 스프링이 뜰 때 Configuration을 읽고 MemberService를 빈에 등록을 함 
        
        ![Untitled 16](https://user-images.githubusercontent.com/43032391/153753967-5599a802-6c01-4357-926b-aed60d8a260f.png)
        
        - 인자값 확인은 ctrl + p
        - DI에는 필드 주입, setter 주입, 생성자 주입 이렇게 3가지 방법이 있다. 의존관계가 실행중에 동적으로 변하는 경우는 거의 없으므로 생성자 주입을 권장
        - 직접 주입의 장점은 바꿔치기할 때 컴포넌트 스캔보다 훨씬 간편하다.
        - Autowired 를 통한 DI는 helloConroller , memberService 등과 같이 스프링이 관리하는
        객체에서만 동작한다. 스프링 빈으로 등록하지 않고 내가 직접 생성한 객체에서는 동작하지 않는다.
    - 회원 웹 기능
        - 아래와 같이 소스코드를 추가하면 template 에 있는 home.html을 불러온다.
        
        ![Untitled 17](https://user-images.githubusercontent.com/43032391/153753969-2f9ae768-4cbd-4f25-b56e-1a9edcfa94e4.png)
        
        - 참고: 컨트롤러가 정적 파일보다 우선순위가 높다.
        - 컨트롤러를 뒤지고 없으면 정적 리소스를 찾음
        
        ![Untitled 18](https://user-images.githubusercontent.com/43032391/153753970-4b262c2c-be41-4ea9-b519-bd316e3f99f0.png)
        
        ![Untitled 19](https://user-images.githubusercontent.com/43032391/153753971-77b27b9e-6fee-4d57-9d65-293fab87728c.png)
        ![Untitled 20](https://user-images.githubusercontent.com/43032391/153753972-6b1c00a1-89ef-4790-a935-3651866b84a7.png)
        ![Untitled 21](https://user-images.githubusercontent.com/43032391/153753973-efa5db8a-9fa2-4e7c-bfed-d89aa6c8f6df.png)
        
        - members를 읽어 들임(모델 안의 값) members 안에는 리스트로 멤버들이 들어와 있음 (`MemberController`)
        - 메모리에 있기 때문에 서버를 껏다 키면 날라감.
        
    - 스프링 DB 접근 기술
        
        ![Untitled 22](https://user-images.githubusercontent.com/43032391/153753974-63225a10-f821-484e-b3aa-aa211bae76cc.png)
        ![Untitled 23](https://user-images.githubusercontent.com/43032391/153753975-c998dd14-68f0-4709-8371-13b1fa5c725b.png)
        ![Untitled 24](https://user-images.githubusercontent.com/43032391/153753976-3d7047c7-6e52-4d3f-b146-4d40034cdee4.png)

        
    - 순수 JDBC
        
        ![Untitled 25](https://user-images.githubusercontent.com/43032391/153753977-c02b3f17-bb78-4619-8100-c6adf4dd2a55.png)
        ![Untitled 26](https://user-images.githubusercontent.com/43032391/153753978-b959d69d-5f35-4147-b0d7-95cf83ad8c4c.png)
        ![Untitled 27](https://user-images.githubusercontent.com/43032391/153753979-79d76f29-d3cb-461c-90cc-4a4b0d72578d.png)
        ![Untitled 28](https://user-images.githubusercontent.com/43032391/153753980-de988b79-cde4-4992-ad42-2ba8505d0b5a.png)

        
    - 스프링 통합 테스트
        
        ![Untitled 29](https://user-images.githubusercontent.com/43032391/153753981-eee63b03-3498-486f-9df7-7530ccb69d49.png)
        
    - JDBCTemplate
        
        순수 Jdbc와 동일한 환경설정을 하면 된다.
        스프링 JdbcTemplate과 MyBatis 같은 라이브러리는 JDBC API에서 본 반복 코드를 대부분
        제거해준다. 하지만 SQL은 직접 작성해야 한다.
        
- 7일차
    - JPA
        
        JPA는 기존의 반복 코드는 물론이고, 기본적인 SQL도 JPA가 직접 만들어서 실행해준다.
        JPA를 사용하면, SQL과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환을 할 수 있다.
        JPA를 사용하면 개발 생산성을 크게 높일 수 있다.
        
        ![Untitled 30](https://user-images.githubusercontent.com/43032391/153753983-652a1ac8-36a8-4129-b6ee-8319e06ec3ca.png)
        
        show-sql : JPA가 생성하는 SQL을 출력한다.
        ddl-auto : JPA는 테이블을 자동으로 생성하는 기능을 제공하는데 none 를 사용하면 해당
        
        create 를 사용하면 엔티티 정보를 바탕으로 테이블도 직접 생성해준다. 해보자.
        
        ![Untitled 31](https://user-images.githubusercontent.com/43032391/153753985-1fd22521-171e-4595-b55c-c7b58a1b02a9.png)
        
        DB가 ID 자동 생성하는 전략 
        
        JPA는 EntityManager를 통해 동작
        
        org.springframework.transaction.annotation.Transactional 를 사용하자.
        스프링은 해당 클래스의 메서드를 실행할 때 트랜잭션을 시작하고, 메서드가 정상 종료되면 트랜잭션을
        커밋한다. 만약 런타임 예외가 발생하면 롤백한다.
        JPA를 통한 모든 데이터 변경은 트랜잭션 안에서 실행해야 한다.
        
- 8일차
    - 스프링데이터 JPA
        
        스프링 데이터 JPA는 JPA를 편리하게 사용하도록 도와주는 기술입니다. 따라서 JPA를 먼저 학습한
        후에 스프링 데이터 JPA를 학습
        
        테스트 중  아래와 같이 뜬다면 [appliaction.properties](http://appliaction.properties) 부분에 db url 커넥션 뒤 ;MODE=LEGACY 추가 + 데이터베이스 활성화 
        
        ```java
        javax.persistence.PersistenceException: org.hibernate.exception.ConstraintViolationException: could not execute statement
        Caused by: org.hibernate.exception.ConstraintViolationException: could not execute statement
        ```
        
        [https://stackoverflow.com/questions/70818631/upgrade-h2-version-2-0-202-from-1-4-200](https://stackoverflow.com/questions/70818631/upgrade-h2-version-2-0-202-from-1-4-200)
        
       ![Untitled 32](https://user-images.githubusercontent.com/43032391/153753986-3ddd9053-dd2e-42b9-b719-1f905f091254.png)
       ![Untitled 33](https://user-images.githubusercontent.com/43032391/153753987-1876b474-28a9-4522-ac40-ae0568b86e7f.png)
        
        실무에서는 JPA와 스프링 데이터 JPA를 기본으로 사용하고, 복잡한 동적 쿼리는 Querydsl이라는
        라이브러리를 사용하면 된다. Querydsl을 사용하면 쿼리도 자바 코드로 안전하게 작성할 수 있고, 동적
        쿼리도 편리하게 작성할 수 있다. 이 조합으로 해결하기 어려운 쿼리는 JPA가 제공하는 네이티브 쿼리를
        사용하거나, 앞서 학습한 스프링 JdbcTemplate를 사용
        
    - AOP
        
        모든 메소드의 호출 시간을 측정하고 싶다면?
        공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern)
        회원 가입 시간, 회원 조회 시간을 측정하고 싶다면?
        
        ![Untitled 34](https://user-images.githubusercontent.com/43032391/153753988-38d831f0-d36e-4806-a2a4-8fcb7a2e39a3.png)
        
        공통관심사항 / 핵심관심 사항 
        
        문제점 
        
        회원가입, 회원 조회에 시간을 측정하는 기능은 핵심 관심 사항이 아니다.
        시간을 측정하는 로직은 공통 관심 사항이다.
        시간을 측정하는 로직과 핵심 비즈니스의 로직이 섞여서 유지보수가 어렵다.
        시간을 측정하는 로직을 별도의 공통 로직으로 만들기 매우 어렵다.
        시간을 측정하는 로직을 변경할 때 모든 로직을 찾아가면서 변경해야 한다.
        
        ![Untitled 35](https://user-images.githubusercontent.com/43032391/153753990-3e16daeb-2fca-42e0-9790-be88b74872c2.png)
        
        해결
        회원가입, 회원 조회등 핵심 관심사항과 시간을 측정하는 공통 관심 사항을 분리한다.
        시간을 측정하는 로직을 별도의 공통 로직으로 만들었다.
        핵심 관심 사항을 깔끔하게 유지할 수 있다.
        변경이 필요하면 이 로직만 변경하면 된다.
        원하는 적용 대상을 선택할 수 있다.
        
        <AOP 적용 전 의존관계>
        
        ![Untitled 36](https://user-images.githubusercontent.com/43032391/153753993-ae779efb-4627-44c9-9c58-38af703b3568.png)
        
        <AOP 적용 후 의존관계>
        
        ![Untitled 37](https://user-images.githubusercontent.com/43032391/153753994-f7923a2c-9e8a-4e68-ad2e-75539a273c41.png)
        
        <AOP 적용 전 전체 그림>
        
        ![Untitled 38](https://user-images.githubusercontent.com/43032391/153753996-2d63ce04-ec4c-40f9-92de-d1221c09ec07.png)
        
        <AOP 적용 후 전체 그림>
        
        ![Untitled 39](https://user-images.githubusercontent.com/43032391/153753997-60c607a5-2488-43b7-9090-6df07b217fee.png)


---
단축키

```java
IntelliJ 단축키
alt + insert 는 생성자, getter setter 자동
ctl + shift + 엔터는 현재 구문 자동 완성
ctl + alt + insert 새파일 추가 
ctl + b  사용처 찾기 
자동완성 soutv => system.out.println 이 자동으로 뜸 
ctl + alt + v 변수출하기
Ctrl + Alt + l 코드 정렬
ctrl + Alt + M 코드 -> 함수로 Extract
Ctrl + Shift + T -> 클래스 이름에서 테스트 코드 자동 만들기 
SHIFT + F10 이전 실행 그대로 실행 
Alt + Insert 컨스트럭터 
Ctrl + N 위치 찾기 
Ctrl + E 최근에 봤던 것 
Shift + F10 이전 실행 
Ctrl + Alt + N line 합치기 
--------------------------------------------------------------
실행환경 실행
- 현재포커스
맥 : Command + Shift + R
윈도우, 리눅스 : Shift + Ctrl + F10
- 이전실행
맥 : Ctrl + R
윈도우 : Shift + F10
라인 수정하기
-라인 복사
맥 : Command + D
윈도우 : Ctrl + D

-라인 삭제
맥 : Command + 백스페이스
윈도우 : Ctrl + Y

-라인 합치기(라인단위)
맥 : Command + Shift + J
윈도우 : Ctrl + Shift + J

라인 단위로 옮기기
- 구문 이동
맥 : Command + Shift + 위,아래
윈도우 : Ctrl + Shift + 위,아래
- 라인 이동
맥 : Option + Shift + 위,아래
윈도우 : Alt + Shift + 위,아래

- Element 단위로 옮기기
맥 : Option + Shift + Command+ 왼쪽,오른쪽
윈도우 : Alt + Ctrl + Shift + 왼쪽,오른쪽

코드 즉시보기
- 인자값 즉시 보기
맥 : Command + P
윈도우 : Ctrl + P

- 코드 구현부 즉시 보기
맥 : Option + Space
윈도우 : Shift + Ctrl + I

- Doc 즉시 보기
맥 : F1
윈도우 : Ctrl + Q
포커스 에디터

- Page Up/Down
맥 : Fn + 위/아래
윈도우 : Page Up / Down
포커스 특수키
- 포커스 범위 한 단계씩 늘리기
맥 : Alt + 위/아래 화살표
윈도우, 리눅스 : Ctrl + W(위) / Shift + Ctrl + W(아래) 

- 포커스 뒤로/앞으로 가기
맥 : Command + [ , ]
윈도우, 리눅스 : Ctrl + Alt + 좌,우

- 멀티 포커스
맥 : Alt + Alt + 아래
윈도우, 리눅스 : Ctrl + Ctrl + 아래

- 오류 라인 자동 포커스
맥 : F2
윈도우, 리눅스 : F2
검색 텍스트
- 현재 파일에서 검색
맥 : Command + F
윈도우 : Ctrl + F

- 현재 파일에서 교체
맥 : Command + R
윈도우 : Ctrl + R

- 전체 검색
맥 : Command + Shift + F
윈도우 : Ctrl + Shift + F

- 정규표현식으로 검색, 교체
맥, 윈도우 : Regex 체크
검색기타
- 파일 검색
맥 : Shift + Command + O
윈도우 : Shift + Ctrl +  N

- 메소드 검색
맥 : Alt + Command + O
윈도우 : Shift + Ctrl + Alt + N

- Action 검색
맥 : Shift + Command + A
윈도우 : Shift + Ctrl + A

- 최근 열었던 파일 목록 보기
맥 : Command + E
윈도우 : Ctrl + E

- 최근 수정했던 파일 목록 보기
맥 : Command + Shift+ E
윈도우 : Ctrl + Shift + E

- 변수/필드의 데이터 변경 지점 찾기
변경되는 포인트 : 변수나 필드에 커서를 놓고 action 에서 "dataflow" 입력 후 "Analyze Dataflow to Here" 선택
영향주는 포인트 : 변수나 필드에 커서를 놓고 action 에서 "dataflow" 입력 후 "Analyze Dataflow from Here" 선택

- 중복된 코드 찾기
action에서 " Locate Duplicate" 입력

자동완성
- 스마트 자동완성
맥 : control + Shift + Space
윈도우 : control + Shift + Space

- 스태틱 메소드 자동완성
맥 : control + Shift * 2
윈도우 : control + Shift * 2

- Getter/Setter/생성자 자동완성
맥 : Command + N
윈도우 : Alt + Insert

- 자동완성
맥 : control + I
윈도우 : Ctrl + I
Live Template
- Live Template 목록 보기
맥 : Command + J
윈도우, 리눅스 : Ctrl + J

- Live Template 메뉴에서 나만의 템플릿 추가 가능
리팩토링 Extract
- 변수 추출하기
맥 : Command + Option + V
윈도우, 리눅스 :  Ctrl + Alt + V

- 파라미터 추출하기
맥 : Command + Option + P
윈도우, 리눅스 : Ctrl + Alt + P

- 메소드 추출하기
맥 : Command + Option + M
윈도우, 리눅스 : Ctrl + Alt + M

- 이너클래스 추출하기
맥 : F6
윈도우, 리눅스 : F6
리팩토링 기타
- 이름 일괄 변경 하기
맥 : Shift + F6
윈도우, 리눅스 : Shift + F6

- 메소드 일괄 변경하기
맥 : Shift + Command + F6
윈도우, 리눅스 : Shift + Ctrl + F6

- Import 정리하기
맥 : control + Option + O
윈도우, 리눅스 : Ctrl + Alt + O

- Import 자동 정리하기
Settings | Editor | General | Auto Import에서 Optimize imports on the fly 선택

- 코드 자동 정렬하기
맥 : Command + Option + L
윈도우, 리눅스 : Ctrl + Alt + L
디버깅
- Debug 모드로 실행하기(현재 위치의 메소드)
맥 : control + Shift + D
윈도우, 리눅스 : 없음

- Debug 모드로 실행하기(이전에 실행한 메소드)
맥 : control + D
윈도우, 리눅스 : Shift + F9

- Resume(다음 브레이크 포인트로 이동하기)
맥 : Command + Option + R
윈도우, 리눅스 : F9

- Step Over(현재 브레이크에서 다음 한줄로 이동하기)
맥 : F8
윈도우, 리눅스 : F8

- Step Into(현재 브레이크의 다음 메소드로 이동)
맥 : F7
윈도우, 리눅스 : F7

- Step Out(현재 메소드의 밖으로 이동)
맥 : Shift + F8
윈도우, 리눅스 : Shift + F8

- Evaluate Expression(브레이크된 상태에서 코드 사용하기)
맥 : Option+ F8
윈도우, 리눅스 : Alt + F8

- Watch(브레이크 이후의 코드 변경 확인하기)
맥 : 없음
윈도우, 리눅스 : 없음
Git 기본 기능 사용하기
- Git View On
맥 : Command + 9
윈도우, 리눅스 : Alt + 9

- Git Option Popup
맥 : control + V
윈도우, 리눅스 : Alt + '(Tab 위 버튼)

- Git History
맥 : control + V --> 4
윈도우, 리눅스 : Alt + '(Tab 위 버튼) --> 4

- Branch
맥 : control + V --> 7
윈도우, 리눅스 : Alt + '(Tab 위 버튼) --> 7

- Commit
맥 : Command + k
윈도우, 리눅스 : Ctrl + k

- Push
맥 : Command + Shift + k
윈도우, 리눅스 : Ctrl + Shift + k

- Pull
맥 : Command + Shift + A --> git pull
윈도우, 리눅스 : Ctrl + Shift + A --> git pull
GitHub 연동하기
- GitHub 연동하기
맥 : Command + Shift + A --> Share github
윈도우, 리눅스 : Command + Shift + A --> Share github

- GitHub Clone
메인 화면에서 Check out from Version Control 선택 후 Git 선택

클래스
- 클래스 구조 확인
맥 : command+7
윈동, : Alt + 7

플러그인
- 플러그인 설치
맥 : Command + Shift + A --> Plugins(Preferences)
윈도우, 리눅스 : Command + Shift + A --> Plugins(Preferences)

- Terminal
맥 : Option+ F12
윈도우, 리눅스 : Alt + F12

```
