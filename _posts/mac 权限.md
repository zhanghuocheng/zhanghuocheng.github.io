## 1 mac 权限 

```
1 ls -l 查看文件权限 
```

使用普通用户 使用普通用户去开发

问题1 

![image-20210610141439604](/Users/zhanghuocheng/Library/Application Support/typora-user-images/image-20210610141439604.png)



解决办法 

```

```







### 2 解决mac 高版本 根目录为只读问题

```
先在home目录下创建一个可以读写的目录，例如/Users/zc/datasudo vim /etc/synthetic.conf在synthetic.conf文件中添加一行（注意：/Users/zc/data是你自己创建的可读写的目录，可以自定义。用来做为/data实际存储的目录。重启后会创建一个/data的软链接，指向/Users/zc/data)data    /Users/zc/data中间的分隔符一定要是tab3. 重启mac即可


```



### 3 开权限问题

```
chmod -R 775 文件夹或者文件(可以递归开通权限)）
```

