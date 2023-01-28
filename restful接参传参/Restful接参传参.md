

# Restful接参传参

## 1.简单类型

```java
@RestController
@RequestMapping("/para")
public class ShiYan3 {
    @GetMapping("/person")
    public String getPara(@RequestParam("like") String username, @RequestParam("username") String like){
        return "{'username':'"+username+"','like':'"+like+"'}";
    }
}
```

http://localhost:8082/para/person?username=gzy&like=18

如果在后端方法参数前，指定了@RequestParam()的话，那么前端必须要有对应字段才行(当然可以通过设置
    该注解的required属性来调节是否必须传)，否者会报错；如果参数前没有任何该注解，那么前端可以传，也可
    以不传，如：

## 2.实体类接收

==请求参数key的名称要和POJO中属性的名称一致，否则无法封装。==

接收json使用实体类接收、在方法参数前加上@RequestBody

```java
@PostMapping("/student")
public Student getStudent(@RequestBody Student student){
    System.out.println(student);
    return student;
}
```

```java
@Data
public class Student {
    private String name;
    private Integer age;
    private Score score;
}
```

```java
@Data
public class Score {
    private String subject;
    private Integer sc;

}
```

![Snipaste_2023-01-17_16-45-00](images\Snipaste_2023-01-17_16-45-00.png)



关于json参数key值与实体类不相协调的情况：

![Snipaste_2023-01-17_16-40-58](images\Snipaste_2023-01-17_16-40-58.png)



非json使用实体类接收

http://localhost:8082/para/student?name=gzy&age=18&score.subject=语文&score.sc=2

**如果Body体内没有传递json数据，需要把@RequestBody注解去掉、否则报400 BadRequest**

**如果Body体内有传递json数据，不把@RequestBody注解去掉、默认就接收了Body体内的数据**

**如果Body体内有传递json数据、把@RequestBody注解去掉、默认就接收了路径参数上的数据**

```java
@PostMapping("/student")
public Student getStudent(Student student){
    System.out.println(student);
    return student;
}
```

**此时从路径上接收数据、把Student认为对象、创造对象并封装数据**

## 接收数组集合数据

![1630484283773](images\1630484283773.png)

```java
//数组参数：同名请求参数可以直接映射到对应名称的形参数组对象中
@RequestMapping("/arrayParam")
@ResponseBody
public String arrayParam(String[] likes){
    System.out.println("数组参数传递 likes ==> "+ Arrays.toString(likes));
    return "{'module':'array param'}";
}
```

```java
//集合参数：同名请求参数可以使用@RequestParam注解映射到对应名称的集合对象中作为数据
@RequestMapping("/listParam")
@ResponseBody
public String listParam(@RequestParam List<String> likes){
    System.out.println("集合参数传递 likes ==> "+ likes);
    return "{'module':'list param'}";
}
```

SpringMVC将List看做是一个POJO对象来处理，将其创建一个对象并准备把前端的数据封装到对象中，但是List是一个接口无法创建对象，所以报错。

解决方案是:使用`@RequestParam`注解



## 接收日期参数

先修改UserController类，添加第三个参数

```java
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date,
                        @DateTimeFormat(pattern="yyyy-MM-dd") Date date1,
                        @DateTimeFormat(pattern="yyyy/MM/dd HH:mm:ss") Date date2)
    System.out.println("参数传递 date ==> "+date);
	System.out.println("参数传递 date1(yyyy-MM-dd) ==> "+date1);
	System.out.println("参数传递 date2(yyyy/MM/dd HH:mm:ss) ==> "+date2);
    return "{'module':'data param'}";
}
```

使用PostMan发送请求，携带两个不同的日期格式，

`http://localhost/dataParam?date=2088/08/08&date1=2088-08-08&date2=2088/08/08 8:08:08`



## 3.常见注解

### @RequestBody

### @RespondBody

​     在@RestController中包含

### @RequestParam

​    @Param是sql语句传参时的注解

### @RequestMapping

### @RestController

### **@PathVariable**

   一般就接@RequestMapping后写的路径中的   {id}      如@RequestMapping("/users/{id}")

