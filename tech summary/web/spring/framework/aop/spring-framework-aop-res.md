# spring framework aop research #

AOP（aspect-oriented programming）：主要是面向贯穿整个应用的功能开发而产生的，例如切面日志，声明事务管理，安全。

With AOP, you still define the common functionality in one place, but you can declaratively define how and where this functionality is applied without having to modify the class to which you are applying the new feature. *aop的通用功能也是在一块，通过声明式定义在那些类上添加新功能而不改变原有的类*

## AOP terminology ##

- **Aspect** *An aspect is the cross-cutting functionality you are implementing.*
- **JoinPoint** *A joinpoint is a point in the execution of the application where an aspect can be plugged in*
- **Advice** *Advice is the actual implementation of our aspect.*
- **Pointcut** *A pointcut defines at what joinpoints advice should be applied.*
- **Introduction** *An introduction allows you to add new methods or attributes to existing classes*
- **Target** *A target is the class that is being advised.*
- **Proxy** *A proxy is the object created after applying advice to the target object* 
- **Weaving** *Weaving is the process of applying aspects to a target object to create a new,proxied object*

AOP有不同的实现框架有很多，除了spring aop还有AspectJ等。
Spring只支持method joinpoints而其他的框架例如AspectJ或者JBoss允许提供field joinpoints

## creating advice ##

adivice in spring

1. Around -> org.aopalliance.intercept.MethodInterceptor 
2. Before -> org.springframework.aop.BeforeAdvice
3. After -> org.springframework.aop.AfterReturningAdvice
4. Throws -> org.springframework.aop.ThrowsAdvice  

## Aop实战 ##
1. aop拦截方法，记录方法到日志中

## spring 支持的4中aop ##

1.  基于代理的经典AOP（已经摈弃了，过于笨重与繁琐）