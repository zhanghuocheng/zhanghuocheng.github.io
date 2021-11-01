---
layout: page
---
*  目录
{:toc}
### Terraform学习笔记

### 1 背景知识

1 了解terraform 官网&&架构师视频(推荐)   https://www.terraform.io/  && https://www.youtube.com/channel/UCneBEzatq8l08DhfB0fM64w

 1 了解k8s  官网. https://kubernetes.io/zh/docs/home/



###  2  1  调试流程&&环境

#### 2.1 方便的调试流程 方便高效的反馈环


![image](/images/1606267288220.jpg)


#### 2.2 环境

```
1 在本级安装secureCrt vscode(vscode 安装terraform插件)
2 在qa安装terrafom&&lrzsz
3 使用使用mac别名和ssh免密登陆 

alias ti='terraform init '
alias tp='terraform plan '
alias ta='terraform apply -auto-approve'
alias td='terraform destroy -auto-approve'
```



### 3 成果

1 使用terraform实现nginx安装

```
/app/terraform/terraform-docker-demo
```







### 4 附件资料

##### 1 kubectl的基本操作

```
kubectl get pod/all 获取pod/获取全部信息
kubectl delete svc wordpress-mysql 删除service
kubectl logs -f  wordpress-8g7d2  查看pod的日志
kubectl get services
port-foward --可以pod的端口映射到机器
```



##### 2 Linux install lrzsz

```
首先通过sftp工具把安 装文件上传到tmp目录下.

# cd tmp
# wget http://www.ohse.de/uwe/releases/lrzsz-0.12.20.tar.gz
# tar zxvf lrzsz-0.12.20.tar.gz && cd lrzsz-0.12.20
# ./configure && make && make install

上面安装过程默认把lsz和lrz安装到了/usr/local/bin/目录下, 下面创建软链接, 并命名为rz/sz:
# cd /usr/bin
# ln -s /usr/local/bin/lrz rz
# ln -s /usr/local/bin/lsz sz
```











