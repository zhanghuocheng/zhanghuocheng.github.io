## github-gitpages-jekyll 构建blog实战

[TOC]

## 1 目标-完全免费

完成一个自己的博客，写完后只需提交，即可触发自动编译部署。



博客的搭建过程

| 组件                    | 网址                       | 提供的功能       |
| ----------------------- | -------------------------- | ---------------- |
| github （仓库+action）  | https://github.com/        | action：持续集成 |
| gitpages（域名+服务器） | https://pages.github.com/  |                  |
| jekyll（网站模版）      | https://jekyllrb.com/docs/ |                  |
| 七牛云                  |                            | 辅助，存储图片   |
|                         |                            |                  |



## 2 提交blog的过程

```sequence
张火成-->git:写博客/commit
git-->Action:自动构建并推送
Action-->gitpages服务器:更新静态页面
gitpages服务器-->张火成:看到了刚提交的博客
```

## 3 过程详情

```
 1 创建一个gitpages 静态站点，配置免费域名
 https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site
 
 2 创建一个jekyll项目
 https://jekyllrb.com/ 
 
 3 提交到github
 
 4 配置action
 https://jekyllrb.com/docs/continuous-integration/buddyworks/
 
 
 以上过程，都要有官方文档，配置简单
```

