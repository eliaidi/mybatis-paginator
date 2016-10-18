Support Mybatis version >= 3.1

Basic usage -->  [here](https://github.com/miemiedev/mybatis-paginator/blob/master/src/test/java/com/github/miemiedev/mybatis/paginator/PaginatorTester.java)

Plugin config -->  [here](https://github.com/miemiedev/mybatis-paginator/blob/master/src/test/resources/mybatis-config.xml)

Use in Spring+Mybatis -->  [spring-mybaits-template](https://github.com/miemiedev/spring-mybaits-template)

BTW： [中文文档](http://my.oschina.net/miemiedev/blog/135516)

Downloading from the Maven central repository
```xml
<dependencies>
  ...
    <dependency>
        <groupId>com.github.miemiedev</groupId>
        <artifactId>mybatis-paginator</artifactId>
        <version>1.2.17</version>
    </dependency>
 ...
</dependencies>
```调用方式（分页加多列排序）： 


int page = 1; //页号 
int pageSize = 20; //每页数据条数 
String sortString = "age.asc,gender.desc";//如果你想排序的话逗号分隔可以排序多列 
PageBounds pageBounds = new PageBounds(page, pageSize , Order.formString(sortString)); 
List list = findByCity("BeiJing",pageBounds); 

//获得结果集条总数 
PageList pageList = (PageList)list; 
System.out.println("totalCount: " + pageList.getPaginator().getTotalCount()); 

PageList类是继承于ArrayList的，这样Dao中就不用为了专门分页再多写一个方法。 

使用PageBounds这个对象来控制结果的输出，常用的使用方式一般都可以通过构造函数来配置。 



new PageBounds();//默认构造函数不提供分页，返回ArrayList 
new PageBounds(int limit);//取TOPN操作，返回ArrayList 
new PageBounds(Order... order);//只排序不分页，返回ArrayList 

new PageBounds(int page, int limit);//默认分页，返回PageList 
new PageBounds(int page, int limit, Order... order);//分页加排序，返回PageList 
new PageBounds(int page, int limit, List<Order> orders, boolean containsTotalCount);//使用containsTotalCount来决定查不查询totalCount，即返回ArrayList还是PageLi


Thanks for [rapid-framework](https://code.google.com/p/rapid-framework) and [plum](https://github.com/yfyang/plum) author.
