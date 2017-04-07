# java container note #

常见的类：
1. java.util.Map
2. java.util.Set
3. java.util.List -> AbstractList -> ArrayList -> 
4. java.util.Vector
5. java.util.Stack
6. java.util.Queue


## java.util.Queue 
**队列** ： *先进先出的数据结构*

主要提供的方法为： offer(E), peek(), poll() 此组方法返回如果是空返回null， add（E），element(), remover()此组方法为空返回异常,需要进行异常处理