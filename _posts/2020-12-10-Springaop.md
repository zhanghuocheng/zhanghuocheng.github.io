---
layout: pages
---
*  目录
{:toc}
Spring aop



```java
package com.example.transactional.test.aop;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

/**
 * 切面的一套语法
 *
 * @author yp-m-2598
 */
@Aspect
@Component
@Order(-5)
public class AspectTest {

	/**
	 * 定义切点  包名必须是public开头 
	 */
	@Pointcut("execution(public * com.example.transactional.test.action.*.*(..))")
	public void webLog() {
	}

	/**
	 * 在切点之前执行
	 *
	 * @param joinPoint
	 */
	@Before("webLog()")
	public void doBefore(JoinPoint joinPoint) {
		System.out.println("==========doBefore");
	}

	/**
	 * 在切点之后执行
	 *
	 * @param joinPoint
	 */
	@AfterReturning("webLog()")
	public void doAfterReturning(JoinPoint joinPoint) {
		Object object = joinPoint.getArgs();
		System.out.println("==========AfterReturning");

	}

	/**
	 * 在切点抛异常执行
	 */
	@AfterThrowing("webLog()")
	public void webLogAfterThrowing() {
		System.out.println("===========webLogAfterThrowing");
	}

	@AfterReturning("webLog()")
	public void afterReturningWebLog() {
		System.out.println("=========afterReturningWebLog");
	}

	/**
	 * 手动调用切点命中的方法
	 *
	 * @param jp
	 * @return
	 * @throws Throwable
	 */
	@Around("webLog()")
	public Object around(ProceedingJoinPoint jp) throws Throwable {
		System.out.println("1 -- around before...");
		//--显式的调用目标方法
		Object obj = jp.proceed();
		System.out.println("1 -- around after...");
		return obj;
	}
}
```







参考地址 https://www.cnblogs.com/cxuanBlog/p/13060510.html