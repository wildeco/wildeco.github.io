---
title: "Include Rmarkdown/HTML file in Jekyll posts"
date: 2023-04-15T15:34:30-04:00
categories:
  - blog
tags:
  - R markdown
---

![](https://team-coder.com/images/posts/2020-06-14-github-pages-and-jekyll/title-image.jpg)

Jekyll + GitHub pages is excellent for blogging. My usual workflow is writing posts in markdown (.md), codes in blocks, copying the results, and linking images. This is convenient as it's highly flexible and simple to use, as GitHub pages renders the .md files nicely. And I can edit the files directly in GitHub as well. Sometimes, it is just easier to render the R workflow as .html file and link to the Jekyll website. However, including the .html in Jekyll is not straightforward. I am going to show a simple way to do that, and it's also for my own record :). 

***Step 1: Render to .html file***

Once you are done with your Rmarkdown, you can render it as .html file. Usually, the .html file will have a lot of files in the same folder. But you can also embed all the files in a single .html file, to do that you will need to insert the following code in the YAML header of your R markdown file:

```
---
format:
  html:
    embed-resources: true
---   
```

Btw I no longer use R markdown in Rstudio but use [Quarto](https://quarto.org/docs/computations/r.html) for rending Rmarkdowns to html, within the VSCode editor. Because I also program in Python and Quarto is multi-language, it's super convenient. If you haven't then you should check it out. 

***Step 2: Edit the .html file and add to `_posts` folder in Jekyll***

Let's say your output file is rendered as `output.html`, then open the file using any text editor and then add this to the front matter

```
---
layout: post
title: Posting Rmarkdowns to your Jekyll website
---
```

Copy the output.html file to the `_posts` folder. Remember to rename the file in the [Jekyll convention](https://jekyllrb.com/docs/posts/)

```
YEAR-MONTH-DAY-title.MARKUP

e.g., 2023-04-17-output.html
```
Finally, execute the build command in your terminal and check if it's working

```
bundle exec jekyll build
```

Push to your GitHub repo

```
git commit -am "add html file"
git push
```

Voila !! You will have your html blog within the posts section in your website. 