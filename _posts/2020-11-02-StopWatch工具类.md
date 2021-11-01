---
layout: page
---

*  目录
{:toc}

StopWatch-spring框架中一个简单的工具类



### 1  StopWatch-一个简单的工具类-统计线程/方法的执行时间

### 2 demo



```
 public static void main(String[] args) {
        StopWatch stopWatch = new StopWatch("stopWatch test");

        stopWatch.start("task 1 ");
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }).start();
        stopWatch.stop();

        stopWatch.start("task 2 ");
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }).start();
        stopWatch.stop();

        stopWatch.start("task 3 ");
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    Thread.sleep(2500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }).start();
        stopWatch.stop();

        System.out.println(stopWatch.shortSummary());

        System.out.println("---------------我是分割线---------------");
        System.out.println(stopWatch.prettyPrint());
    }
```

```
StopWatch 'stopWatch test': running time (millis) = 5
---------------我是分割线---------------
StopWatch 'stopWatch test': running time (millis) = 5
-----------------------------------------
ms     %     Task name
-----------------------------------------
00002  040%  task 1 
00002  040%  task 2 
00001  020%  task 3 
```

