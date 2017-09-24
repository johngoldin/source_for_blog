---
title: How I Set Up This Site
author: John Goldin
date: '2017-02-11'
menu: "main"
categories: []
tags: []
Categories:
  - blogdown
  - GitHub
Description: ''
Tags:
  - blogdown
  - GitHub
---
I attended the **blogdown** session at the RStudio conference in Florida. I am enjoying the enthusiasm and energy around R and RStudio.
It reminds me of the early days of personal computers at the end of the 70's and the beginning of the 80's. Perhaps I am experiencing a second
childhood. Anyway, all the Cool Kids are doing web pages on GitHub so I want to do it too.

I have done some simple blog posts with Blogger and WordPress. One of my goals is to create a portfolio of the my R projects.
RMarkdown is the obvious way to go and WordPress doesn't directly support
that. So that's a motivation to use **blogdown**. But a big  part of the
motivation is that these days I am "all in" with the RStudio set of
tools so it's natural to put my faith in Yihui Xie and jump in. Because **blogdown** is still developing,
I know I am going to suffer through rough edges. As a retiree, I am
doing this for fun so the rough edges just add to the adventure.

### GitHub Pages
I had a little trouble to start because I didn't understand the basics of
what was going on with GitHub and web pages. Here I am focused on what GitHub refers to as a "user site" (as opposed to an organization site or a project site). See their [general description of GitHub Pages](https://pages.github.com/) and [What is GitHub Pages?](https://help.github.com/articles/what-is-github-pages). The key
fact is that if you have a repository called `username.github.io` (with your
GitHub username), whatever is in that repository will be served
as a web site accessed as `https://username.github.io`. What
we are going to do here is describe how to use **markdown**, RStudio,
and GitHub to place the content of a static web site into
your `username.github.io` repository.

### GitHub
The site relies on **blogdown** and GitHub. You have to have at least a beginner's familiarity with GitHub, and believe me, I am merely a
GitHub beginner. I got my start with GitHub mostly based on information
from Jenny Bryan (see [Happy Git and GitHub for the useR](http://happygitwithr.com/)) and from [RStudio](https://support.rstudio.com/hc/en-us/articles/200532077-Version-Control-with-Git-and-SVN). There's also an [introduction](https://guides.github.com/activities/hello-world/) on the GitHub site.

You need to be able to create a repository on GitHub and then
clone that to a project in RStudio. See especially [section 16](http://happygitwithr.com/new-github-first.html) on Happy Git.

In general I try to operate in a way that allows me to rely on RStudio to do most of the work and to avoid doing git commands in the Terminal on OSX.
That's why I create a minimal repository first on GitHub and then create
a new project in RStudio that clones the repository from GitHub. Rely on
Jenny's directions on how to do that.

### Creating a website
To get started with blogdown, I relied on a post by [Amber Thomas](https://proquestionasker.github.io/blog/Making_Site/),
especially the comments on the post by Yihui Xie, the creator of
**blogdown**. Amber's instructions involve more work with Git than I wanted
to attempt. In particular, she uses multiple branches. Instead,
I followed the suggestion in the comments by Yihui Xie and created two repositories.
One was for the site itself (`johngoldin.github.io`) and the other (which I called `pages-source`) contains the **blogdown** and **Hugo** material
that actually produces the site. 

1. Create a repository for username.github.io on your github.
2. Clone that to a RStudio project with the same name.
3. Create a repository on your github, any name you desire, but here we will call it `hugo-source`.
4. Clone that second project to an RStudio project.

You are going to use **blogdown** to create a **Hugo** site created by files in the RStudio project
`hugo-source`. And you are going to configure that site
so that whenever it builds a website, it will place that
website into the RStudio project username.github.io.
When you push username.github.io to GitHub you will in effect
publish your website.

(It doesn't matter whether or not you maintain
a GitHub repository for `hugo-source`. It depends on whether
you want to use version control for convenience or backup, just
as would be true for any other RStudio project.)

[Kevin Wong](http://kevinfw.com/post/blogging-with-r-markdown/) does a nice
job of describing the steps needed to get started with **blogdown**. Too bad
I didn't discover this page until after I started writing this description. But I will follow his text closely here.

Here are the steps in the RStudio project that contains the source for Hugo. If you don't already have `devtools` installed as a pckage, use the Packages tab in RStudio to add that package.

```
library(devtools)
devtools::install_github("rstudio/blogdown")
```

In the RStudio project hugo-source (or whatever you have called it), have
**blogdown** install hugo.

```
library(blogdown)
blogdown::install_hugo()
```

Next we wil have Hugo create a new site:

```
blogdown::new_site()
```

The hugo-source site has to be **totally** empty. Otherwise you will get an error. Of course as created it will not be totally empty.
You will have an RProj file and probably `.gitignore`.  Move those
out of the project folder and keep them somewhere safe. Run
`new_site` again and them move them back into the project folder.

Next you need to install a **Hugo** theme. Go to the [themes page](http://themes.gohugo.io/) to find one you like. 
It's hard to know what to pick when you are just starting out.
I'm a novice as well so I can't offer good advice. You can
avoid a choice for now and just stick with the default theme
that is installed as part of the new_site() call.

If you have chosen a different theme, use the install_theme call:

```
install_theme("spf13/hyde")
```

The above commands  will be needed only once when you first
setup the project.

To try out your site, 
```
blogdown::serve_site()
```

With luck, the web site should appear in your RStudio View pane.

If you make changes in a post, they will automatically update
in the site if it is running, You press the **stop** button to halt the site. To restart it in the RStudio Viewer pane, you
can again use `blogdown::serve_site()`.

How to you get this site running in **GitHub**? There's a neat trick.
Edit the `config.toml` file in the `hugo-pages` project folder and
add this magic line:

```
publishDir = "../username.github.io"   # where username is your GitHub name
```

Whenever you run blogdown::serve_site(), the constructed site will be
created in the `username.github.io` directory rather than in `hugo-pages`.
To get the site working on **GitHub**, switch to the `username.github.io` project in RStudio,
go to the Git pane in RStudio, select all the changed files, `Commit`, 
and then `Push` the changes to **GitHub**. Magic! The same code
that is creating the trial web site on your local computer will
now be reproduced exactly in the `username.github.io`
repository on **GitHub** and can be accessed as http://username.github.io.

You can work on your web site on your local RStudio project. When you think it is ready to publish changes
for all the world to see, go to the `username.github.io` project and
push the changes to **GitHub** and you have published your changes on the web.

In summary, here are the steps to maintain the site:  
1. edit the site in the hugo-source project  
2. run blogdown::serve_site() to refresh the site  
3. switch to the username.github.io project on your local machine  
4. commit all changes  
5. push those changes to username.github.io on GitHub.  

### Now What?
I now have a working web site on **GitHub**. But I have a ways to go to learn
how to take advantage of **Hugo** on an ongoing basis. So far I have added
one and only one post. I have looked at the [Hugo documentation](http://gohugo.io/overview/usage/) a bit to try to figure out how to do some basis things.
For example, [this page](https://gohugo.io/extras/shortcodes#ref-relref) tells
me how to add a cross-reference to a post on my site.

It is not yet clear to me how I will take advantage of my **Hugo** **GitHub** site on an ongoing basis.
One of the features of **blogdown** is that I can use RMarkdown.
How will I do that in practice?
I'll have an RMarkdown file in a project I am working on that
documents or demonstrates that project. Will I `knit` the file
and then move the html to my **blogdown** project? Will
I move the Rmd file to the **blogdown** project and include a `setwd` function
call to point to the project that it comes from? I haven't
tried any of this in practice yet. I need to look at the existing **blogdown**
examples more closely. When I know more, I'll add to this introduction.

I have switched to the Hyde-x theme rather than just Hyde.
Configuration has involved a lot of trial and error.
I setup Disqus and briefly saw the ability to do comments on my blog. But after and I made some unrelated changes, 
I no longer saw any sign of Disqus.
Eventually I realized that I was confused (and ignorant) about the
syntax of `config.toml`. I had had a square-brackets author line above
the line that set `disqusShortname` and as a result `disqusShortname`
wasn't getting set. I moved things around and comments reappeared.

This is typical of the blundering around I am doing with Hugo and themes.
I guess it's a learning experience.

### Things I Have Learned Since I First Posted This

#### Directory Structure
If you follow my steps exactly as described here or the instructions at the [RStudio blogdown readme](https://github.com/rstudio/blogdown), you
are likely to end up with a two-tiered directory structure. You create an
RStudio project for your site (the top level) and then when you run `blogdown::new_site()` you create a new directory within that project
directory. That didn't seem right to me, so behind the scenes I "fixed" that
and flattened things so that my hugo site directory was the same as my RStudio project.
Since then, I've decided there is probably some advantage in keeping
the hugo site as a separate directory inside the project directory. It's not
a big deal, but having two levels gives you a place to put additional related
material that is not directly related to your web site. As of now I have "flat" one-directory structure for my blogdown site. But if you
follow the description in this post and end up with a two-level structure,
keep it.

#### How To Manage an RMarkdown Post
I finally did my first RMarkdown post. As is likely to be the case,
it is derived from a separate RStudio project. How should I deal with the
working directory? The RMarkdown file is in my Hugo blogdown project. But
the data file I need for my work is in the original project directory.
At first I thought I should change the working directory with `setwd()`,
but I wondered about what side effects that might produce.
A [post on Stack Overflow](http://stackoverflow.com/questions/20060518/in-rstudio-rmarkdown-how-to-setwd) steered me away from `setwd()`. 
I now know I should use something like `knitr::opts_knit$set(root.dir = '../myproject')`. I have been having some trouble with that,
presumably because of the `..` notation to go up a directory, but
I haven't taken the time yet to case that out. Being impatient I cut
corners and sort of hardcoded the file reference in my Rmd file. I'll go back
and fix that once I figure out the `root.dir` parameter.



