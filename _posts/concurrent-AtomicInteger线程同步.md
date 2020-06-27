---
layout: default
---



concurrent-AtomicInteger线程同步

```mermaid
sequenceDiagram
participant 我（软件工程师）
participant AtomicInteger
participant unsafe
participant jvm
我（软件工程师）-->>AtomicInteger:创建对象，并发调用getAndIncrement
AtomicInteger-->>unsafe: 传入当前对象，原始值，更改值
unsafe-->>jvm:do while 循环调用指令compareAndSwapInt

```

![image-20191214154455677](/Users/huochengzhang/Library/Application Support/typora-user-images/image-20191214154455677.png)

#### compareAndSwapInt 这个原子操作的指令实现

```
c/c++ 加上硬件支持的
```



```
public class AtomicTest {
    AtomicInteger atomicInteger = new AtomicInteger(0);
    static ExecutorService executorService = Executors.newFixedThreadPool(10);

    public static void main(String[] args) {
        AtomicTest atomicTest = new AtomicTest();
        for (int i = 0; i < 1000; i++) {
            executorService.submit(new Runnable() {
                @Override
                public void run() {

                    //getAndIncrement() 这个函数怎么实现线程同步的
                    atomicTest.atomicInteger.getAndIncrement();
                    System.out.println(atomicTest.atomicInteger.get());
                }
            });

        }
    }

}
```



### getAndIncrement

```
   public final int getAndIncrement() {
        return unsafe.getAndAddInt(this, valueOffset, 1);
    }
```

#### this 当前AtomicInteger对象

#### valueOffset 是获取AtomicInteger对象的value通过反射

```
 private static final long valueOffset;

    static {
        try {
            valueOffset = unsafe.objectFieldOffset
                (AtomicInteger.class.getDeclaredField("value"));
        } catch (Exception ex) { throw new Error(ex); }
    }

    private volatile int value;
```



### unsafe class

#### 通过native 方法compareAndSwapInt 比较并交换 do while

```
   public final int getAndAddInt(Object var1, long var2, int var4) {
        int var5;
        do {
            var5 = this.getIntVolatile(var1, var2);
        } while(!this.compareAndSwapInt(var1, var2, var5, var5 + var4));

        return var5;
    }
```



```
休息态-->运动态:起床小技巧，让起床动作在意识之前发生
休息态-->运动态:6:00起床/喝温水
运动态-->运动态:半小时
运动态-->吃饭态:吃早餐(8点之前)
吃饭态-->工作态:工作
工作态-->休息态:换维度放松，休息脑&体 11:50
休息态-->工作态:下午2:00-10:00工作-休息-运动循环
休息态-->休息态:睡觉：11:00-6:00
```

```
自我压力/工作压力/社会压力/家庭压力-->工作/学习:驱动 40%
篮球（训练）-->工作/学习:兴趣驱动 60%（给我激情）喜欢挑战，不放弃
篮球（训练）-->篮球（训练）:信仰库里 库里的坚持，热爱，三观
篮球（训练）-->篮球（训练）:长期的篮球训练
```

