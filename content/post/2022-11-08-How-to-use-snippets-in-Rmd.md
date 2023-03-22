---
date: 2022-11-08
title: "How to use snippets in Rmd"
author: Jianqi
---

There is a function about complete the mathematic code when typing the imcomplete code in many  complier. In RStudio the `.R` file also has this function. But in the RMarkdown typed in the text it is lack in. So we need to complete the mathematic code with the help of snippets embeded in RStudio. 

The snippets is in the `tools->Global Options->Code `  that we will found at the bottom of the screen called `Edit Snippets`. 

The first columns is R has been written in advance. The basic synatax is like below:

```R
snippet lib
	library(${1:package})
```

the first column is the snippets with the abbreviation of code.

the second column is the effect when typing the abbreviation the code in `${}` is the text will show on the complier or script that are scriptable. the number is the typing order we  writing in the code chunk. We  can  `tab`  to transfer the code module when we finished the code module to next module. But we could not type the code modules circularly. 

So based on the logic of this synatax, we can edit the snippet by ourselves. 

Example: we want to add mathematical formula we usually type `$$`  in pairs. We could edit the abbreviation `dd` to replace `$$ $$`.

```R
snippet dd
	\$\$ ${1:formula} \$\$
```

