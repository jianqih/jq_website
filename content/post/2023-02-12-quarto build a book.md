---
title: "How to use quarto build a book"
date: "2023-02-12"
---

usually we use rmarkdown to create a book project. It could build in RStudio and publish in netlify. But it’s little tedious that it need to git and push into respority. But when we using the quarto to create could avoid this problem. When we want to publish the book online, we just type the command `quarto publish` to publish the book deployed in Netlify. It will have servel choices when using the command above we choose the netlify and push the `ENTER`.

Of course, if using the Github, GitLab etc. you can point Netlify at your site’s source code and have it deployed whenever your code changes.

The easiest way to publish locally rendered content by netlify is `quarto publish netlify`

And when you haven’t publish before, the publish command will prompt you to authenticate connecting with the account of Netlify.

The final published book will be showed like this.

![netlify-control-panel](../../../static/media/netlify-control-panel.png)

