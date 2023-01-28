i++我们明白是先把i值赋值给前方自身再+1；

++i是自增一再赋值给前方变量。

```java
@RestController
 public  class ShiYan2 {
    public static Integer i = 0;
    @GetMapping("/num1")
    public synchronized void num1(){
        i=i++;
        System.out.print(i+" ");

    }
    @GetMapping("/num2")
    public synchronized void num2(){
        i=++i;
        System.out.print(i+" ");
    }
}

```

我将使用jmeter来发送10个请求测试

![g](images\g.png)

当请求路径/num1时进入num1()方法、相应的num2也是如此；

当10个请求完成后、不管num1还是num2、理应是从1输出至10；

可现实并非如此

num1方法内输出：全部输出0

![1000](images\100.png)

num2方法输出：从1到10

![1001](images\101.png)

查看编译生成target目录中相应类ShiYan2.class

```java
@RestController
public class ShiYan2 {
    public static Integer i = 0;

    public ShiYan2() {
    }

    @GetMapping({"/num1"})
    public synchronized void num1() {
        Integer var1 = i;
        i = i + 1;
        i = var1;
        System.out.print(i + " ");
    }

    @GetMapping({"/num2"})
    public synchronized void num2() {
        i = i = i + 1;
        System.out.print(i + " ");
    }
}

```

可以看明白为什么num1方法中的i++为什么一直输出0了。

从前理解的i++（先把i值赋值给前方变量自身再增一）应该为（先把i值暂存、i值增一、再把暂存的值赋值给前方的变量）



另外：咱们再看一下不加synchronized关键字后的效果（这次一秒发送100个线程请求）

num2输出

![nospng](images\nospng.png)

看到只输出到66、并且一些数值是重复的

原因：自增语句与输出语句并不为一次原子性操作