## 注意事项

1.在style元素中，定义类选择器的时候必须以.为前缀，定义ID选择器的时候以#为前缀

2.在<style>的class声明的顺序是重要的，第二个声明将始终优于第一个声明。浏览器是从上到下读取CSS。

3.使用!important关键字可以确定这个样式为最后使用

4.@component（把普通pojo实例化到spring容器中，相当于配置文件中的<bean id="" class=""/>）

5.如需从JavaScript访问某个HTML元素，您可以使用 document.getElementById(id)方法

6.String：适用于少量的字符串操作的情况,(最慢,String对象一旦创建之后该对象是不可更改的)

　StringBuilder：适用于单线程下在字符缓冲区进行大量操作的情况（线程不安全）

　StringBuffer：适用多线程下在字符缓冲区进行大量操作的情况（线程安全）

7.在spring boot的项目中，配置文件上面写的value对应到yml文件的配置名字