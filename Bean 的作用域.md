# Bean 的作用域
1. singleton
单例模式，使用singleton定义的Bean在Spring容器中只有一个实例，这也是Bean默认的作用域
2. prototype
原型模式，每次通过Spring容器获取prototype定义Bean时，容器都将创建一个新的Bean实例。
3. request
在一次HTTP请求中，容器会返回该bean的同一个实例。而对不同的HTTP请求，会返回不同的实例，该作用域仅在当前HTTP Request内有效
4. session
在一次 HTTP Session 中，容器会返回该 Bean 的同一个实例。而对不同的 HTTP 请求，会返回不同的实例，该作用域仅在当前 HTTP Session 内有效。
5. global Session
在一个全局的 HTTP Session 中，容器会返回该 Bean 的同一个实例。该作用域仅在使用 portlet context 时有效。
