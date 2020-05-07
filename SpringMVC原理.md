# Spring MVC原理

一、上下文在Web容器中的启动
1. Tomcat中的应用部署描述文件web.xml
    - 监听器（javax.servlet.ServletContextListener）
    - 过滤器（filter）
    - servlet（javax.servlet.http.HttpServlet ）
    **注：**在springboot中省去了web.xml的配置，替代策略是通过Servlet3.0中的javax.servlet.ServletContainerInitializer来实现，实现类为org.springframework.web.SpringServletContainerInitializer。

    Servlet容器启动时，例如Tomcat、Jetty启动，则会被 ContextLoaderListener 监听到，从而调用 ContextLoaderListener 的 contextInitialized（ServletContextEvent event）方法，初始化 Root WebApplicationContext容器（内部存放controller层以下的用于web应用的bean）。

    DispatcherServlet 可以初始化一个 WebApplicationContext，用于存放controller 层的bean。
2. IOC容器启动
相当于Root WebApplicationContext 初始化过程
- ContextLoaderListener 的 contextInitialized（ServletContextEvent event）
- createWebApplicationContext(servletContext);
- determineContextClass
- configureAndRefreshWebApplicationContext();
二、DispatcherServlet的启动和初始化
相当于 Servlet WebApplicationContext容器的初始化
- HttpServletBean:负责将ServletConfig设置到当前Servlet对象中
- FrameworkServlet，负责初始化Spring Servlet——WebApplicationContext容器
- DispatcherServlet，负责初始化Spring MVC的各个组件，以及处理客户端的请求
9个组件
- MultipartResolver
- LocaleResolver
- ThemeResolver
- HandlerMapping
- HandlerAdapter
- HandlerExceptionResolver
- RequestToViewNameTranslator
- ViewResolver
- FlashMapManager
三、HTTP请求分发
![mvc过程](picture/MVC.png)
1. 处理不同HttpMethod的请求
FrameworkServlet实现方法
- doGet
- doPost
- doPut
- doDelete
- doOptions
- doTrace
- service
以上方法都调用processRequest方法处理请求
processRequest中的真正执行逻辑是dispatcherServlet中的doService

2. DispatcherServlet处理请求
1）检查是否是上传请求
2）获得请求对应的 HandlerExecutionChain对象
3）获得当前 handler 对应的HandlerAdapter 对象
4）前置处理 拦截器
5）真正的调用 handler 方法，并返回视图（handler）
6）视图
7）后置处理器
8）处理正常和异常的请求调用结果

四、MVC视图呈现
