## Dynamic Proxy
- 就是为了对原来的功能进行扩展
- JDK自带的功能，但是只能代理接口方法，性能好。
- 还有一种代理叫CGLIB，非JDK自带，可以代理非接口方法，性能弱一点。
- Spring就2个代理方法结合着用，实现了AOP。

### 为什么叫动态代理
- 从下面的代码可以看出：代理类CalculatorProxy其实没有实现类CalculatorImpl（及其接口Calculator）的任何信息。
- 具体的实现对象和代理对象都是运行的时候才创建并绑定关系。

### Example
```java
public interface Calculator {
    int add(int a, int b);
}

public class CalculatorImpl implements Calculator {
    @Override
    public int add(int a, int b) {
        int result = a + b;
        System.out.println("执行加法操作，结果为：" + result);
        return result;
    }
}
```

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

public class CalculatorProxy implements InvocationHandler {
    private Object target;

    public CalculatorProxy(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("调用方法：" + method.getName());
        System.out.println("参数：" + args[0] + ", " + args[1]);

        Object result = method.invoke(target, args);

        System.out.println("方法调用完成，结果为：" + result);
        return result;
    }
}
```

```java
import java.lang.reflect.Proxy;

public class CalculatorTest {
    public static void main(String[] args) {
        Calculator calculator = new CalculatorImpl();

        Calculator proxy = (Calculator) Proxy.newProxyInstance(
                calculator.getClass().getClassLoader(),
                calculator.getClass().getInterfaces(),
                new CalculatorProxy(calculator)
        );

        int result = proxy.add(2, 3);
        System.out.println("最终结果：" + result);
    }
}
```