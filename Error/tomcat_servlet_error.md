# Servlet of class org.apache.catalina.servlets.InvokerServlet is privileged and cannot be loaded by this web application
- 17.10.10
  + 사용한 버전 - `tomcat v6.0`, `jdk 1.6`
  + SVN에서 과거 프로젝트를 내려받았는데, 톰캣 6버전이길래 6버전으로 실행했더니 발생
## 해결 방법
- `톰캣 설치 폴더/conf/context.xml`에서 `<Context>`부분을 `<Context reloadable="true" privileged="true">`로 수정
