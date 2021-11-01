---
layout: page
---

*  目录
{:toc}

Stream

### 1 初始化一个数组

```
  int[] array = new Random().ints(10, 10, 100).toArray
  Arrays.stream(array).forEach(i-> out.print(i+",")); 
```



### 2  stream 是单线成执行 main 

```
 int[] array = new Random().ints(10000, 10, 100).toArray();                                             
                                                                                                        
 Arrays.stream(array).forEach(i ->                                                                      
 {                                                                                                      
     a++;                                                                                               
     out.println(Thread.currentThread().getName());                                                     
 });                                                                                                    
 out.println("i ====" + a);                                                                             
```



### 3 parallel stream   执行线程 4个 线程个数取决于及其的内核数

```
ForkJoinPool.commonPool-worker-3
ForkJoinPool.commonPool-worker-1
ForkJoinPool.commonPool-worker-2
main
```



```
int[] array = new Random().ints(100000, 10, 100).toArray();                                           
Arrays.stream(array).parallel().forEach(i ->                                                          
{                                                                                                     
    a++;                                                                                              
    out.println(Thread.currentThread().getName());                                                    
});                                                                                                   
out.println("i ====" + a);                                                                            
```

