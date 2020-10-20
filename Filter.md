# Filter 过滤器
Filter 是 JavaEE 提供的一个 interface，它可负责拦截多个请求或响应；一个请求或响应也可被多个 Filter 拦截。

## 用处
- 在 HttpServletRequest 到达 Servlet 之前，拦截客户的 HttpServletRequest
- 根据需要检查 HttpServletRequest，也可以修改 HttpServletRequest 头和数据
- 在 HttpServletResponse 到达客户端之前，拦截 HttpServletResponse
- 根据需要检查 HttpServletResponse，也可以修改HttpServletResponse 头和数据

---

## 生命周期
创建 Filter 需要实现 javax.servlet.Filter 接口，该接口定义了如下 3 个方法：
- void init(FilterConfig config)：初始化
- void destroy()：可以做资源回收工作
- void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)：实现过滤功能，可以调用 chain.doFilter() 方法，执行该方法之前，是对用户请求的预处理，执行该方法之后，是对服务器响应进行后处理。

init() -> doFilter() -> destroy()

### doFilter
```java
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws ServletException, IOException {
  // ...
}
```

---

## 配置 Filter 的 2 种方式

### 注解（annotation）
|属性|类型|说明|
|---|----|——--|
|filterName|String|指定过滤器的name属性，等价于<filter-name>|
|value|String[]|该属性等价于urlPatterns属性，但是两者不应该同时使用|
|urlPatterns|String[]|指定一组过滤器的URL匹配模式。等价于<url-pattern>标签|
|servletNames|String[]|可指定多个Servlet名，使Filter仅对这几个Servlet执行，取值是@WebServlet中的name属性的取值，或者是web.xml中<servlet-name>的取值|
|dispatcherTypes|DispatcherType|指定该Filter仅对那种模式的请求进行过滤。具体取值包括：ASYNC、ERROR、FORWARD、INCLUDE、REQUEST。默认全部过滤|
|initParams|WebInitParam[]|指定一组过滤器初始化参数，等价于<init-param>标签|
|asyncSupported|boolean|声明过滤器是否支持异步操作模式。等价于<async-supported>标签|
|description|String|该过滤器的描述信息。等价于<description>标签|
|displayName|String|该过滤器的显示名，通常配合工具使用，等价于<display-name>标签|
  

### web.xml 配置
```html
<filter>
    <filter-name>filterName</filter-name>
    <filter-class>filterClass</filter-class>
</filter>
<filter-mapping>
    <filter-name>filterName</filter-name>
    <url-pattern>/*</url-pattern>           指定 Filter 负责拦截的 URL，指定 url-pattern 为 /* 表示拦截所有用户请求
</filter-mapping>
```
