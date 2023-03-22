---
title: "How to use Quarto invert  Jupyter to other format"
date: 2022-10-29
author: Jianqi Huang
---

### Install Quarto

Quarto is a good system to convert the 

Running in JupyterLab

jupyter used to run in Jupyter notebook and Jupyterlab which are focusing in 

And JupyterLab has more module and is more like a IDE. So we use the JupyterLab to render.

we open the JupyterLab use the command `jupyter lab`

And we will open the terminal and `.ipynb` 

### Preview 

before translate it into different file formmat we could use to `preview` module to see the details in the file.

```bash
quarto preview notebook.ipynb
```

In my opioion the best formmat for Quarto is html it could use the code folding function and the interface is tidy.

### Preparation

The `.ipynb` is a little different from we used to write. In the front of the file we add the      

 `Yaml` cell in the first cell. We can add some options in there like title,date,author etc. It    just like the format in `.Rmd` 

### supplement

based on `#｜` in the normal compile and the necessity of translating into other format，It will be as an annotation in Jupyter complier, And be considered as a setting in Quarto,which could input some basic infomation and format in chunk about output.

```
#| label: fig-polar
#| fig-cap: "A line plot on a polar axis"
```



### Render

using the `--to` argument to render to a specific format:

```bash
quarto render notebook.ipynb --to docx
```

Besides, quarto can make `.ipynb` and `.qmd` convert each other

```bash
quarto convert jupy_name.ipynb
quarto convert q_name.qmd
```

