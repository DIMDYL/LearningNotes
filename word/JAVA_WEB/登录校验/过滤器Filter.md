## 介绍

Filter可以把对资源的请求拦截下来，从而实现一些特殊功能

过滤器一般完成一些通用的操作，比如：登录校验、统一编码处理、敏感字符处理等

过滤器执行顺序：按照类名字符串的自然顺序排序A在最前面这样的

## 拦截路径

|   拦截路径   | urlPatterns值 |              含义              |
| :----------: | :-----------: | :----------------------------: |
| 拦截具体路径 |    /login     | 只有访问/login路径，才会被拦截 |
|   目录拦截   |    /emps/*    |  访问emps下的资源，都会被拦截  |
|   拦截所有   |      /*       |       所有资源都会被拦截       |

## 定义Filer

定义一个类，实现Filter接口，并重写全部方法  

配置Filter：Filter类上添加@webFiler注解，配置拦截资源的路径，在启动类中 @ServletComponentScan ，标识当前项目支持Servlet相关组件的，Filter并不是SpringBoot提供的

@WebFilter：那些请求路径会被拦截

init：初始化函数，可以不用写因为是默认实现了

doFilter：拦截后的操作，每次请求都会执行，需要注意，请求后需要放行资源，放行后访问到web资源了，会回到过滤器中执行放行后的操作，然后再返回给客户端

destroy：销毁方法，只执行一次，也是默认实现了不需要自己写

```java
/*
* 注意这里的Filter是java.servlet中的
* */
/*
* WebFilter 表示那些请求会被拦截
* */
@WebFilter(urlPatterns = "/*")
public class DemoFilter implements Filter {
    // 初始化方法，只调用一次
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);
    }

    // 拦截请求之后调用，调用多次
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("拦截到了");
        // 放行
        filterChain.doFilter(servletRequest, servletResponse);
        /*
        * 放行就是让其访问对用的web资源 ，处理完还会回到filter中
        * 放行之后的逻辑执行完毕再给浏览器返回数据
        * */
        System.out.println("放行之后");
    }
    // 销毁方法，只调用一次
    @Override
    public void destroy() {
        Filter.super.destroy();
    }
}
```

## 将对象转换为json

因为当前是在过滤器中返回数据无法自动转换为json

#### 引入依赖

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.76</version>
</dependency>
```

#### 使用

JSONObject.toJSONString：将对象转换为一个json字符串

 response是响应对象，通过响应对象获取一个输出流.write(值) 即可响应

```java
    // token不存在直接放行
    Result error =  Result.error("错误");
    /*
    * 因为是在过滤器不是在控制器中所以没法直响应对象
    * 所以需要手动将对象转换为json
    * */
    String err = JSONObject.toJSONString(error);
    /*
    * getWriter获取一个输出流
    * write返回讲过
    * */
    response.getWriter().write(err);
```

## 过滤器链

一个web应用如果配置多个过滤器，就会形成过滤器链，会一个一个执行过滤器，只有执行完最后一个过滤器才会去访问web资源

访问完web资源后执行放行后的逻辑，放行后的逻辑是反着的，从最后一个过滤器放行后的逻辑开始执行，全部执行完成放行后的逻辑会返回给客户端

## 一个查看是否登录的过滤器

```java
package rog.studymybatis.springbootanli1.filter;

import com.alibaba.fastjson.JSONObject;
import com.github.pagehelper.util.StringUtil;
import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import org.springframework.util.StringUtils;
import rog.studymybatis.springbootanli1.pojo.Result;
import rog.studymybatis.springbootanli1.utils.Jwtutils;

import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebFilter(urlPatterns = "/*")
public class login  implements Filter {
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        /*
        * 获取请求对象
        * HttpServletRequest继承于servletRequest
        * 左边是子接口，右边是父接口需要强转
        * */
        HttpServletRequest request = (HttpServletRequest) servletRequest;
        /*
         * 获取请求对象
         * HttpServletResponse继承于servletResponse
         * 左边是子接口，右边是父接口需要强转
         * */
        HttpServletResponse response = (HttpServletResponse) servletResponse;
        // 获取请求URL
        String URL = request.getRequestURL().toString();
        // 判断是否是login登录
        if (URL.contains("login")){ // 如果请路径包含login说明是登录接口
            // 登录接口直接放行
            filterChain.doFilter(servletRequest,servletResponse);
            // 因为登录接口不需要执行后面的操作所以直接return掉
            return;
        }
        // 获取请求头的token
        String token = request.getHeader("token");
        // 判断token为空
        if (!StringUtils.hasLength(token)){
            // token不存在直接放行
            Result error =  Result.error("错误");
            /*
            * 因为是在过滤器不是在控制器中所以没法直响应对象
            * 所以需要手动将对象转换为json
            * */
            String err = JSONObject.toJSONString(error);
            /*
            * getWriter获取一个输出流
            * write返回讲过
            * */
            response.getWriter().write(err);
            return;
        }
        // 解析token，如果解析失败返回错误
        try {
            Jwtutils.parsejwt(token);
        }catch (Exception e) {
            e.printStackTrace();
            Result d = Result.error("token错误");
            String s = JSONObject.toJSONString(d);
            response.getWriter().write(s);
            return;
        }
        // 放行
        filterChain.doFilter(servletRequest,servletResponse);
    }
}
```
