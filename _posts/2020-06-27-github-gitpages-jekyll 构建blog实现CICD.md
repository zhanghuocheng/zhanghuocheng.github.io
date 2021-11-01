---
layout: page
---
*  目录
{:toc}

## github-gitpages-jekyll 构建blog实现CICD



## 1 目标

完成一个自己的博客，写完后只需提交，即可触发自动编译部署。(简单-完全免费)



###### 博客的搭建过程

| 组件                    | 网址                       | 提供的功能       |
| ----------------------- | -------------------------- | ---------------- |
| github （仓库+action）  | https://github.com/        | action：持续集成 |
| gitpages（域名+服务器） | https://pages.github.com/  |                  |
| jekyll（网站模版）      | https://jekyllrb.com/docs/ |                  |
| 七牛云                  |                            | 辅助，存储图片   |



## 2 写完blog-->更新网站的过程中的动作分析（3456自动完成）

![20200627085617](/images/1596353930081.jpg)





## 3 过程详情

```
 1 创建一个gitpages 静态站点，配置免费域名
 https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site
 
 2 创建一个jekyll项目
 https://jekyllrb.com/ 
 
 3 提交到github
 
 4 配置action
 https://jekyllrb.com/docs/continuous-integration/buddyworks/
 
 5 在mk中添加图片的格式
 ![20200627073705](http://qck2j2ro3.bkt.clouddn.com/test/20200627073705.png?imagelim)
 
 
 以上过程，都要有官方文档，配置简单
```

