### Servlet vs JSP
- Servlet: 웹 페이지를 동적으로 생성하기 위한 자바측 프로그램, Java 언어를 기반으로 만들어지며 웹 어플리케이션 서버(Web Application Server) 위에서 컴파일되고 동작
- JSP: HTML 코드에 Java 코드를 넣어 동적 웹 페이지를 생성하는 웹 애플리케이션 도구, JSP는 Servlet 코드로 변환되어 실행

### WAS 
- DB처리, 로직 처리를 요구하는 동적 타입을 제공하는 소프트웨어 프레임워크, Web Application과 Server Environment를 만들어 동작시켜줌
  - 프로그램 실행 환경가 데이터베이스 접속 기능을 제공
  - 여러 개의 트랜잭션 관리
  - 업무를 처리하는 비즈니스 로직 수행

### Tomcat 
- JSP와 Servlet을 구동하기 위한 서블릿 컨테이너 역할

### Embed Tomcat
- 하나의 톰캣 서버 안에 여러 개의 라이프 사이클을 분리해서 WAR 파일을 저장

### Maven 
- Java 프로젝트 관리를 위한 도구
  - Apache software foundation에서 개발한 Java 기반 프로젝트 관리
  - 프로젝트의 컴파일, 빌드, 테스트, 배포, 실행
  - 서버측 Deploy 자원과 라이브러리 관리

### Maven command
- mvn clean compile package: 현재 작업되어 있었던 폴더를 지우고 패키징
- mvn clean: 이전에 만들었던 결과물을 다 초기화, 만들었던 결과물을 지워버리는 역할
- mvn compile: Java code를 build해서 class bytecode로 만들어주는 과정 (build, target/classes path에 dir 생성)
- mvn package: 만들었던 결과물의 파일을 하나의 단일 압축 파일로 만들어주는 것
- mvn install: 저장소에 만들었던 결과물 파일을 복사해 놓는 과정
- -DskipTest Option: 테스트를 진행 여부에 대한 옵션

### Tomcat Server에 배포
- 패키징된 war 파일 복사
- %TOMCAT_HOME%₩bin₩startup.sh

### Tomcat Manager 이용
- Tomcat Server에 Web Application을 배포하기 위한 관리도구
- %TOMCAT_HOME%₩conf₩tomcat-users.xml 수정

```
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>

<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status" />
<user username="deployer" password="depleyer" roles="manager-script" />
<user username="tomcat" password="tomcat" roles="manager-gui" />

```

### tomcat의 war 파일 적용

- 압축을 푼 프로젝트 확인을 위해 localhost:8080/url을 쳐서 들어갔지만 404 Error 뜨는 경우
- apache-tomcat-${version}/conf로 들어가 server.xml 편집 
```
<Host>
<Context docBase="Servlet" path="/" reloadable="false" />
<Host>
```

### web.xml Servlet 등록

```
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>
  <servlet>
    <servlet-name>hello-servlet</servlet-name>
    <servlet-class>org.example.HelloServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>hello-servlet</servlet-name>
    <url-pattern>/hello-servlet</url-pattern>
  </servlet-mapping>
</web-app>
```

- @WebServlet Annotation 
  - web.xml의 설정 작업을 한꺼번에 해주는 역할