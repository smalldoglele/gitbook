+ 代理链的生成
```java
/***
*注解里描述的是指定拦截方法的签名  [type,method,args] 
*（即对哪种对象的哪种方法进行拦截），它在拦截前用于判断。
*/
@Intercepts({@Signature(type = Executor.class, method ="update", args = {MappedStatement.class, Object.class})})
public class ExamplePlugin implements Interceptor {
	/**
	*是实现拦截逻辑的地方，内部要通过invocation.proceed()显式地推进责任链前进，
	*也就是调用下一个拦截器拦截目标方法。
	*/
    @Override
    public Object intercept(Invocation invocation) throws Throwable {
        return invocation.proceed();
    }
    /**
    *就是用当前这个拦截器生成对目标target的代理，
    *实际是通过Plugin.wrap(target,this) 来完成的，把目标target和拦截器this传给了包装函数。
    */
    @Override
    public Object plugin(Object target) {
        return Plugin.wrap(target, this);
    }
    /**
    *用于设置额外的参数，参数配置在拦截器的Properties节点里。
    */
    @Override
    public void setProperties(Properties properties) {
    }
}
```
+ Plugin.wrap方法
```java
    public static Object wrap(Object target, Interceptor interceptor) {
       //从拦截器的注解中获取拦截的类名和方法信息
       Map<Class<?>, Set<Method>> signatureMap =getSignatureMap(interceptor);
       Class<?> type = target.getClass();
       //解析被拦截对象的所有接口（注意是接口）
       Class<?>[] interfaces = getAllInterfaces(type, signatureMap);
       if(interfaces.length > 0) {
            //生成代理对象， Plugin对象为该代理对象的InvocationHandler  
            //（InvocationHandler属于java代理的一个重要概念，不熟悉的请参考相关概念）
            return Proxy.newProxyInstance(type.getClassLoader(), interfaces, new Plugin(target,interceptor,signatureMap));
        }
        returntarget;
    } 
```