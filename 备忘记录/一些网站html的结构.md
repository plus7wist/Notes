// 一些网站html的结构

## 博客园

### 主页

```
|-------------- body
  |------------ 用户自定义的 html
  |------------ div id=home
    |---------- div id=header
    |---------- div id=main
      |-------- div id=mainContent
        |------ div class=forFlow
          |---- div class=day  : 最近一天
            |-- div class=dayTitle      // 日期
            |-- div class=postTitle     // 第一篇文章的标题
            |-- div class=postCon       // 第一篇文章的摘要
            |-- div class=postDesc      // 第一篇文章的发布信息
            |-- div class=postSeparator // 文章之间的分隔
            |-- div class=postTitle     // 第二篇文章的标题
            |-- ...
          |---- div class= day  : 第二天
          |---- div class= day  : 第三天
          |---- ...
          |---- div class= topicListFooter
    |---------- div id=footer
  |------------ 用户自定义的 html
```

### 文章页面

```
|------------------------ body
  |---------------------- 用户自定义的 html
  |---------------------- div id=home
    |-------------------- div id=header
    |-------------------- div id=main
      |------------------ div id=mainContent
        |---------------- div class=forFlow
          |-------------- div id=post_detail
            |------------ div id=topics
              |---------- div class=post
                |-------- h1 class=postTitle
                |-------- div class=postBody
                  |------ div id=cnblogs_post_body // 文章内容
                  |------ div id=blog_post_info_block
                    |---- div id=blog_post_info
                      |-- div id=green_channel
                      |-- div id=author_profile
                      |-- div id=div_digg
                    |---- div id=post_next_prev // 上一篇和下一篇
                |-------- div class=postDesc
    |-------------------- div id=footer
  |---------------------- 用户自定义的 html
```

## Github Page【某个】

### 主页

```
|---------- body
  |-------- header
    |------ div class=container
  |-------- div class=container
    |------ section id=main_content
      |---- ul class post-list
        |-- 文章链接
        |-- 日期
    |------ section id=comments
  |-------- footer
```

### 文章页面

```
|------ body
  |---- header
    |-- div class=container
  |---- div class=container
    |-- section id=main_content // 文章内容
    |-- section id=comments
  |---- footer
```