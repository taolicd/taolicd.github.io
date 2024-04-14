---
layout: post
title: Creating and hosting a portfolio for free
date: 2024-04-13
---

Building an online portfolio has become essential for professionals such as journalists, technical writers, software developers, and UX designers to showcase their work.
This blog walks you through the process of creating portfolios on Clippings.me, GitHub, GitLab, or Netlify for free. 

## Creating a portfolio on Clippings.me

[clippings.me](https://www.clippings.me/) is a platform for journalists, writers, and freelancers. It requires no coding or app deployment experience. The drawback is the templates are very simple and you cannot customize much.  

To create a free portfolio on clippings.me:

1. Go to the [Clippings website](https://www.clippings.me) and click [**Sign Up**](https://www.clippings.me/users/sign_up).
2. Follow the instructions. Your portfolio will have a URL that resembles `www.clippings.me/<username>`. For example, this is [my short portfolio](https://www.clippings.me/taolicd) on clippings.me. 

If you are not very technical, this is an excellent platform to showcase your work. If you are a technical writer, I don't recommend that you use clippings.me as the only platform for your portfolio. It is just too simple to demonstrate your "tech" skills. As a technical writer, your proficiency in using tech platforms like GitHub, GitLab, or Netlify is a testament to your technical caliber. 

##  Creating a portfolio on GitHub, GitLab, or Netlify

GitHub and GitLab are two popular platforms for hosting and collaborating on Git repositories for source code management. Both have very similar functionality and workflows. GitHub is Microsoft-owned and seems to be more popular. 

Netlify is a platform that automates the build, deployment, and hosting of modern web projects. Netlify can ingest projects with source code stored on GitHub or GitLab. 

For personal projects, you can host them for free on all the three platforms. 

### Step 1 Choose a static site generator 

Before you decide where to host the portfolio, first choose what static site generator (SSG) you want to use for creating your portfolio. SSGs provide templates that allow you to create consistent layouts and designs across your website. These templates can include dynamic elements, such as navigation menus or sidebars, that are generated at build time. [Jekyll](https://jekyllrb.com/) and [Hugo](https://gohugo.io/) are two popular open source SSGs. Jekyll is Ruby-based while Hugo is Go-based. For a comparison of the two, see [Hugo vs. Jekyll](https://opensource.com/article/17/5/hugo-vs-jekyll).

After you have decided on a SSG, follow the official documentation to install the related software. For Jekyll, you can follow the [Jekyll QuickStart Guide](https://jekyllrb.com/docs/). For Hugo, follow the [Hugo QuickStart Guide](https://gohugo.io/getting-started/quick-start/). You should create a dummy site on your machine to get some basic understandings how static site generators work.

### Step 2 Choose a theme

After choosing an SSG, you need to decide a theme. A theme defines the look and feel of a site and provides basic structure and functionalities that you can customize. You can find Jekyll themes on [jekyllthemes.org](http://jekyllthemes.org/). For Hugo themes, go to [themes.gohugo.io](https://themes.gohugo.io/).

### Step 3 Choose where to host your portfolio

Now it is time to decide where to host your portfolio. You don't even have to stick with just one. You can have your source code on GitHub and then use Netlify to manage the deployment. 

#### GitHub

 You can use [GitHub Pages](https://pages.github.com/) to create a website and host it on GitHub for free. Your website on GitHub pages will have a URL that resembles `https://<username>.github.io`, where "`<username>`" is your GitHub username. For example, I have a GitHub pages account on [taolicd.github.io](https://taolicd.github.io). 

To deploy a GitHub Pages site, you need to create a repo on GitHub with the name `<username>.github.io`. On the GitHub login page, locate this repo, click **Settings** tab near the top of the repository page. On the left panel, under Code and automation, click **Pages**. Find to the "**GitHub Pages**" section.

4. Choose a source branch
In the GitHub Pages section, you'll find a dropdown menu labeled "Source." Select the branch you want to use for GitHub Pages. By default, the "main" branch is selected, but you can also choose other branches or the "master" branch.

5. Select a theme (optional)
GitHub Pages allows you to apply a theme to your site to give it a professional look. You can select a theme by clicking on the "Choose a theme" button in the GitHub Pages section. Browse the available themes and click on "Select theme" to apply it to your site.


7. Access your GitHub Pages site
Once you've enabled GitHub Pages and made any desired customizations, scroll back up to the GitHub Pages section in the repository settings. You'll find a message indicating the URL where your site is published (e.g., "Your site is published at https://username.github.io"). Click on the provided URL to access your GitHub Pages site.

8. Publish your content
To publish content on your GitHub Pages site, you can create new files directly in the repository or upload existing files. You can also use Git commands or the GitHub web interface to make changes and updates to your site.

After you've successfully created your GitHub Pages site, you can continue to add, modify, and publish content to your site by making changes to the repository and committing them.

#### GitLab

#### Netlify





