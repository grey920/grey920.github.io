---
title: "[Spring] Interceptor 사용시 의존성 주입이 안되는 경우"
excerpt: "분명 @Autowired를 붙였는데 빈이...null이라고...?"
categories:
  - ErrorDiary
tags:
  - spring
  - DI
toc: true
toc_sticky: true
toc_label: 목차
---

## 현상

MobileControllerInterceptor에서 mainDAO.insertTXLog(logParamMap) 부분이 계속 `nullPointerException`이 일어났다.

logParamMap에 insert시 필요한 값이 안들어간 줄 알고 계속 값을 넣어줬으나 해결되지 않았다.

```java
public class MobileControllerInterceptor extends HandlerInterceptorAdapter {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Autowired private MainDAO mainDAO;

	public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

		(...중략...)

		if( !mobilePath.equals("mobile_") ){
				**mainDAO.insertTXLog(logParamMap);**
		}else{
				**mainDAO.insertTXLog(logParamMap);**
		}

	}

}
```

- 에러로그

  ```
  java.lang.NullPointerException
  	at XXXXXXXXXx.interceptor.MobileControllerInterceptor.preHandle(MobileControllerInterceptor.java:98)
  	at org.springframework.web.servlet.HandlerExecutionChain.applyPreHandle(HandlerExecutionChain.java:151)
  	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1035)
  	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:943)
  	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:1006)
  	at org.springframework.web.servlet.FrameworkServlet.doGet(FrameworkServlet.java:898)
  	at javax.servlet.http.HttpServlet.service(HttpServlet.java:626)
  	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:883)
  	at javax.servlet.http.HttpServlet.service(HttpServlet.java:733)
  	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:231)
  	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
  	at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:53)
  	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
  	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
  	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:201)
  	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119)
  	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
  	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
  	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:202)
  	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:97)
  	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:541)
  	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:143)
  	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:92)
  	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:78)
  	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:343)
  	at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:374)
  	at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:65)
  	at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:868)
  	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1590)
  	at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49)
  	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
  	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
  	at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61)
  	at java.lang.Thread.run(Thread.java:748)
  ```

## 원인

**mainDAO**가 제대로 빈등록이 되어있지 않았다.

원인은 WebMvcConfigurer를 구현한 **WebMvcConfig**에 있었다.

기존 코드

```java
@EnableWebMvc
@Configuration
public class WebMvcConfig implements WebMvcConfigurer {
		@Autowired
		ApplicationContext applicationContext;

		@Autowired
		Environment env;

		(...중략...)

		@Override
		public void addInterceptors( InterceptorRegistry registry ) {
		registry.addInterceptor( new MobileControllerInterceptor() )
	                              .addPathPatterns("/user/login/userLogin.do")
	                              .addPathPatterns("/user/login/logOut.do")
	                              .addPathPatterns("/index/mainIndex.do")

		(...중략...)
		}
}
```

> 위와 같이 `new()`를 통해 Interceptor 객체를 만들어서 등록하면 Spring Container에서 이 Interceptor를 관리하지 못한다고 한다.

Interceptor에서 new로 등록하면 스프링이 이를 관리하지 못하게 되고, 따라서 의존성을 주입하려고 해도 스프링이 관리하지 않기 때문에 null이 되는 것이었다.

## 해결

`@Bean`으로 생성해서 스프링이 관리하도록 만든다. 이것을 통해 Interceptor를 등록하게 되면 다른 곳에서도 @Autowired를 통해 동작하게 된다.

```java
@EnableWebMvc
@Configuration
public class WebMvcConfig implements WebMvcConfigurer {
		@Autowired
		ApplicationContext applicationContext;

		@Autowired
		Environment env;

		(...중략...)

		@Override
		public void addInterceptors( InterceptorRegistry registry ) {
			registry.addInterceptor( mobileInterceptor() )
	                            .addPathPatterns("/user/login/userLogin.do")
	                            .addPathPatterns("/user/login/logOut.do")
	                            .addPathPatterns("/index/mainIndex.do")

			(...중략...)
		}

		**@Bean**
		public ControllerInterceptor controllerInterceptor() {
			return new ControllerInterceptor();
		}
}
```

---

## 느낀점

- mainDAO.insertTXLog(logParamMap) 에서 nullPointerException이 떨어질 때 mainDAO부터 확인하신 대표님.. 이게 바로 짬의 차이인가..
- 구글링을 잘하자..
- 스프링의 작동 원리부터 제대로 공부하자. 스프링이 관리하지 않는데 어떻게 주입을 받을 수 있었겠어???

---

## 참고

[[Spring]Interceptor 사용 시 의존성 주입이 안되는 경우](https://eastglow.github.io/back-end/2019/08/01/Spring-Interceptor-%EC%82%AC%EC%9A%A9-%EC%8B%9C-%EC%9D%98%EC%A1%B4%EC%84%B1-%EC%A3%BC%EC%9E%85%EC%9D%B4-%EC%95%88%EB%90%98%EB%8A%94-%EA%B2%BD%EC%9A%B0.html)
