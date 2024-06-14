**map是一种对象，而json是一种规范，我们进行数据传输的时候就是传输的符合json规范的map,而jackson和fastjson就实现了这个功能。**

细节区别：

1. Map的键不一定是String类型，而JSON的键值都必须是String
2. 我们传到前端的Map之所以键值都是String类型，那是因为@RestController注解帮助我们将Map转化成了JSON

https://www.cnblogs.com/henuliulei/p/14893735.html