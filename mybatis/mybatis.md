# mybatis

## 一·环境boot+mybatis

### 1.pom文件

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>3.0.1</version>
</dependency>
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <scope>runtime</scope>
</dependency>
```

### 2.数据库配置

application.yml

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybrand?severTimezone=UTC
    username: root
    password: '000214'
```

### 3.新建文件

建立实体类、建立接口XXXMapper  使用@Mapper注解、新建xml文件

![Snipaste_2023-01-10_18-17-24](images\Snipaste_2023-01-10_18-17-24.png)

BrandMapper

```java
@Mapper
public interface BrandMapper {
   //  @Select("selec * from tb_brand")
    List<Brand> selectAll();
}
```

在resources下新建与XXXMapper同目录同名称的后缀为xml的文件、其实生成的target目录中会自动与类文件在同一文件夹内，注意多级目录写下来、写类时用的  .  但resources下用  /  

![Snipaste_2023-01-10_18-31-29](images\Snipaste_2023-01-10_18-31-29.png)

xml文件参考写法

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">



<mapper namespace="org.gzy.mapper.BrandMapper">

    <select id="selectAll" resultMap="brandResultMap">
        select * from  tb_brand;
    </select>


    <resultMap id="brandResultMap" type="org.gzy.dao.Brand">
        <result column="brand_name" property="brandName"/>
        <result column="company_name" property="companyName"/>
    </resultMap>


</mapper>
```

## 二.一些关键字及用法

### 1.resultType标注返回值类型

**注意在返回东西时写、增删改不用写**

```xml
<select id="selectAll" resultType="org.gzy.dao.Brand">
    select *
    from tb_brand;
</select>
```

### 2.resultMap解决字段名称不相符问题

```xml
<select id="selectAll" resultMap="brandResultMap">
    select * from  tb_brand;
</select>
```


```xml
<resultMap id="brandResultMap" type="org.gzy.dao.Brand">
    <result column="brand_name" property="brandName"/>
    <result column="company_name" property="companyName"/>
</resultMap>
```

resultMap中标注了type、其它语句使用了resultMap后就不用写resultType

### 3.parameterType标注参数类型（一般可省略不写）

### 4.#{ }占位符

* #{} ：执行SQL时，会将 #{} 占位符替换为？，将来自动设置参数值。

* ${} ：拼接SQL。底层使用的是 `Statement`，会存在SQL注入问题。

### 5.@Param标注对应参数

```java
Brand selectByIdAndStatus(@Param("status") int id,@Param("id") int status1);
```

### 6.使用特殊字符

< 等这些字符在xml中有特殊含义，所以此时我们需要将这些符号进行转义

`&lt;` 就是 `<` 的转义字符。

## 三.多条件多参数

* 使用 `@Param("参数名称")` 标记每一个参数，在映射配置文件中就需要使用 `#{参数名称}` 进行占位

  ```java
  List<Brand> selectByCondition(@Param("status") int status, @Param("companyName") String companyName,@Param("brandName") String brandName);
  ```

* **将多个参数封装成一个 实体对象 ，将该实体对象作为接口的方法参数。该方式要求在映射配置文件的SQL中使用 `#{内容}` 时，里面的内容必须和实体类属性名保持一致。**

  ```java
  List<Brand> selectByCondition(Brand brand);
  ```

```xml
<select id="selectByCondition" resultMap="brandResultMap">
    select *
    from tb_brand
    where status = #{status}
      and company_name like #{companyName}
      and brand_name like #{brandName}
</select>
```

* 将多个参数封装到map集合中，将map集合作为接口的方法参数。该方式要求在映射配置文件的SQL中使用 `#{内容}` 时，里面的内容必须和map集合中键的名称一致。

  ```
  List<Brand> selectByCondition(Map map);
  ```

## 四.动态sql

* if

* choose (when, otherwise)

* trim (where, set)

* foreach

我们先学习 if 标签test属性和 where 标签：

![image-20210729204458815](images\image-20210729204458815.png)

* if 标签：条件判断

  * test 属性：逻辑表达式

  ```xml
  <select id="selectByCondition" resultMap="brandResultMap">
      select *
      from tb_brand
      where
          <if test="status != null">
              and status = #{status}
          </if>
          <if test="companyName != null and companyName != '' ">
              and company_name like #{companyName}
          </if>
          <if test="brandName != null and brandName != '' ">
              and brand_name like #{brandName}
          </if>
  </select>
  ```

  如上的这种SQL语句就会根据传递的参数值进行动态的拼接。如果此时status和companyName有值那么就会值拼接这两个条件。

* 但是它也存在问题，如果此时给的参数值是

  ```java
  Map map = new HashMap();
  // map.put("status" , status);
  map.put("companyName", companyName);
  map.put("brandName" , brandName);
  ```

  拼接的SQL语句就变成了

  ```sql
  select * from tb_brand where and company_name like ? and brand_name like ?
  ```

  而上面的语句中 where 关键后直接跟 and 关键字，这就是一条错误的SQL语句。这个就可以使用 where 标签解决

* where 标签

  * 作用：
    * 替换where关键字
    * 会动态的去掉第一个条件前的 and 
    * 如果所有的参数没有值则不加where关键字

  ```xml
  <select id="selectByCondition" resultMap="brandResultMap">
      select *
      from tb_brand
      <where>
          <if test="status != null">
              and status = #{status}
          </if>
          <if test="companyName != null and companyName != '' ">
              and company_name like #{companyName}
          </if>
          <if test="brandName != null and brandName != '' ">
              and brand_name like #{brandName}
          </if>
      </where>
  </select>
  ```

  > 注意：需要给每个条件前都加上 and 关键字。



只选择其中之一

![image-20210729213613029](images\image-20210729213613029.png)

如上图所示，在查询时只能选择 `品牌名称`、`当前状态`、`企业名称` 这三个条件中的一个，但是用户到底选择哪儿一个，我们并不能确定。这种就属于单个条件的动态SQL语句。 

这种需求需要使用到  `choose（when，otherwise）标签`  实现，  而 `choose` 标签类似于Java 中的switch语句。

```xml
<select id="selectByConditionSingle" resultMap="brandResultMap">
    select *
    from tb_brand
    <where>
        <choose><!--相当于switch-->
            <when test="status != null"><!--相当于case-->
                status = #{status}
            </when>
            <when test="companyName != null and companyName != '' "><!--相当于case-->
                company_name like #{companyName}
            </when>
            <when test="brandName != null and brandName != ''"><!--相当于case-->
                brand_name like #{brandName}
            </when>
        </choose>
    </where>
</select>
```

## 五.添加及主键返回

void add(Brand brand);

<insert id="add">
    insert into tb_brand (brand_name, company_name, ordered, description, status)
    values (#{brandName}, #{companyName}, #{ordered}, #{description}, #{status});
</insert>

```xml
<insert id="add" useGeneratedKeys="true" keyProperty="id">
    insert into tb_brand (brand_name, company_name, ordered, description, status)
    values (#{brandName}, #{companyName}, #{ordered}, #{description}, #{status});
</insert>
```

在 insert 标签上添加如下属性：

* useGeneratedKeys：是够获取自动增长的主键值。true表示获取
* keyProperty  ：指定将获取到的主键值封装到哪儿个属性里

```java
Brand brand = new Brand(null, "百度1", "百度有限公司1", 303, "搜索引擎用的多1", 1);
System.out.println(brand);  //id为null
Integer add = brandMapper.add(brand);
System.out.println(add);  //打印1，（插入成功或一行受到影响）
System.out.println(brand);  //此时打印发现id并不为null，与数据库中一致
```

## 六.修改与删除

void update(Brand brand);

```xml
<update id="update">
    update tb_brand
    <set>
        <if test="brandName != null and brandName != ''">
            brand_name = #{brandName},
        </if>
        <if test="companyName != null and companyName != ''">
            company_name = #{companyName},
        </if>
        <if test="ordered != null">
            ordered = #{ordered},
        </if>
        <if test="description != null and description != ''">
            description = #{description},
        </if>
        <if test="status != null">
            status = #{status}
        </if>
    </set>
    where id = #{id};
</update>
```

*set* 标签可以用于动态包含需要更新的列，忽略其它不更新的列。



删除

void deleteById(int id);

```xml
<delete id="deleteById">
    delete from tb_brand where id = #{id};
</delete>
```

### 批量删除foreach标签

void deleteByIds(int[] ids);

**foreach 标签**

用来迭代任何可迭代的对象（如数组，集合）。

* collection 属性：
  * mybatis会将数组参数，封装为一个Map集合。
    * 默认：array = 数组
    * 使用@Param注解改变map集合的默认key的名称
* item 属性：本次迭代获取到的元素。
* separator 属性：集合项迭代之间的分隔符。`foreach` 标签不会错误地添加多余的分隔符。也就是最后一次迭代不会加分隔符。
* open 属性：该属性值是在拼接SQL语句之前拼接的语句，只会拼接一次
* close 属性：该属性值是在拼接SQL语句拼接后拼接的语句，只会拼接一次

```xml
<delete id="deleteByIds">
    delete from tb_brand where id
    in
    <foreach collection="array" item="id" separator="," open="(" close=")">
        #{id}
    </foreach>
    ;
</delete>
```

> 假如数组中的id数据是{1,2,3}，那么拼接后的sql语句就是：
>
> ```sql
> delete from tb_brand where id in (1,2,3);
> ```

**collection="array"里面填array默认一个数组，但尽量填写标明的@Param的值例如ids**