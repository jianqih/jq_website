---
title: 如何在blogdown中实现新建和上传
date: 2022-10-27
author: JianqiHuang
---

### 存储静态文件

所有的文件都会放在 `static/` 中，之后再Hugo传送到网站的时候复制到 `public/` 文件中。

这些文件通常用于存储静态文件如图片、pdf、CSS等。 比如一张照片 `static/figure/bar.png`  在`.md`文件中，引用的方式就是`![](/figure/bar.png)`.

也就是说即使将内容放在`\root\content`中，最终也会可以访问到。

在`static`中生成一个文件夹，进一步将需要上传的文件复制进生成的文件夹。这样当Hugo上传到网站的时候，自然会将生成的文件夹以及包含的文件传入`public`，同时对于该文件来说，其生成的网站名是`your_website_name/your_folder/file_name`其中文件名包含了文件的后缀`html`、`css`、`pdf`等。`your_folder`可以是多个文件夹的嵌套，之间的网站名生成逻辑同样是`/your_folder1/your_folder2/.../`



### 新建网页

为了在网站建立新的的页面，可以从新建文件夹开始。

1. 比如，在新建一个页面，比如`content/`中新建一个叫`tutorials/`的文件夹；
2. 新建一个`_index.md` 在这个文件夹之下，同时再将其重命名为`index.md`。在`index`中可以添加YAML文件，其中有关于这个文件的[导向](https://sourcethemes.com/academic/docs/managing-content/#create-a-widget-page)。
3. 添加模块
4. 链接这些模块到你的菜单，指向`config/_default`文件夹和打开`menus`TOML 文件夹



### reference

- https://bookdown.org/yihui/blogdown/static-files.html
- https://vickimzhang.rbind.io/post/hugo-blogdown/#run-locally-to-see-how-your-website-looks

