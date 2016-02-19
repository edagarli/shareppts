title: Greys-anatomy分享
speaker: 卤肉(@edagarli)
url: https://github.com/edagarli/shareppts
transition: slide3
files: /js/index.js,/css/index.css,/js/zoom.js
theme: moon
usemathjax: yes

[slide]
#Greys-anatomy分享
## Java在线问题诊断工具

url:https://github.com/oldmanpushcart/greys-anatomy

----

<small> speaker: 卤肉（@edagarli）</small>


[slide]

## 几种诊断方式
----
* 肉眼诊断 {:&.rollIn}
* 日志诊断
>通过给出问题的代码入参或者上下游加上日志,或者出问题的时候加上日志来诊断;这种方式的问题就是出现问题你需要重新拉分支,加日志,本地测试再上限这一系列流程.另外一个问题是过多的日志会影响应用性能;
* 监控诊断
>通过完善的监控,通常包括完善且精确的异常划分.对不同的异常情况有独立的监控.加上完善的报警机制.这是最理想的情况.其优势是能快速定位问题点,问题是建立这一套完善的机制需要很长时间.并且监控只能发现问题类型,比如监控发现是数据错误,但是到底那条数据错误还是需要日志等手段来定位.
* 在线诊断工具
>在不需要重新发布的情况下,在线诊断应用的问题所在.通常还可以用于定位接口瓶颈等问题;


[slide]

## 几个在线诊断工具
----
* Btrace(bytecode trace) (JVM Crash风险)
* HouseMD  (scala)
>能快速指定拦截的类与方法，但却无法支持对观察到的对象进行展开、条件过滤等操作

* Greys-Anatomy (java)

[slide]

## 软件特点

* ClassLoader隔离
* 运行时加载
* 常用问题定位命令化(业务代码疑难杂症定位的常用技术手段)
* 表达式支持(OGNL表达式)
* 多用户同时访问
* 高性能(用ASM设计了字节码增强)
* 纯Java编写

[slide]

## 实战

* 软件安装 
>curl -sLk http://ompc.oss.aliyuncs.com/greys/install.sh|sh

* 参数说明
> ./greys.sh <PID>[@IP:PORT]

[slide]

##坑
###illegal ENV, please set $JAVA_HOME to JDK6+

```

justhacker:greys justhacker$ sudo ./greys.sh <PID>
illegal ENV, please set $JAVA_HOME to JDK6+
justhacker:greys justhacker$ echo  $JAVA_HOME
/Library/Java/JavaVirtualMachines/jdk1.7.0_67.jdk/Contents/Home
justhacker:greys justhacker$ java -version
java version "1.7.0_67"
Java(TM) SE Runtime Environment (build 1.7.0_67-b01)
Java HotSpot(TM) 64-Bit Server VM (build 24.65-b04, mixed mode)

```

* -H是sudo命令的参数，意思是使用sudo命令切换身份的时候，仍然采用当前用户的ENV设置。你的$JAVA_HOME是配置在用户justhacker下的，但在root用户下却没有，所以需要用这个参数将$JAVA_HOME带过去，即可 {:&.rollIn}

[slide]

##演示

