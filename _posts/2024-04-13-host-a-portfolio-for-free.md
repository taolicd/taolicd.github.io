---
layout: post
title: Creating and hosting a portfolio for free
date: 2024-04-13
---

Building an online portfolio has become essential for professionals across fields — from journalists and technical writers to software developers and UX designers — to effectively showcase their work and skills.

This blog walks you through the process of creating portfolios on Clippings.me, GitHub, GitLab, or Netlify for free. 

## Creating a portfolio on Clippings.me

[clippings.me](https://www.clippings.me/) is a platform for journalists, writers, and freelancers. It requires no coding or app deployment experience. The drawback is the templates are very simple and you cannot customize much.  

To create a free portfolio on clippings.me:

1. Go to the [Clippings website](https://www.clippings.me) and click [**Sign Up**](https://www.clippings.me/users/sign_up).
2. Follow the instructions. Your portfolio will have a URL that resembles `www.clippings.me/<username>`. For example, this is [my short portfolio](https://www.clippings.me/taolicd) on clippings.me. 

If you are not very technical, this is an excellent platform to showcase your work. If you are a technical writer, I don't recommend that you use clippings.me as the only platform for your portfolio. It is just too simple to demonstrate your **tech** skills. As a technical writer, your demonstrated proficiency in leveraging version control systems like GitHub and GitLab and efficiently deploying applications on platforms such as Netlify demonstrates your strong technical skills and quick learning capability.

##  Creating a portfolio on GitHub, GitLab, or Netlify

GitHub and GitLab are two popular platforms for hosting and collaborating on Git repositories for source code management. Both have very similar functionality and workflows. GitHub is owned by Microsoft and seems to be more popular. 

Netlify is a platform that automates the build, deployment, and hosting of web projects. Netlify can ingest projects with source code stored on GitHub or GitLab. 

For personal projects, you can host them for free on all the three platforms. 

To create and host a portfolio, you typically go through the following steps:

1. Choose a static site generator (SSG). An SSG makes it easy for you to create a professional looking website using established mechanisms and templates. See [Step 1 Choose an SSG](#step-1-choose-an-ssg).
2. Choose a theme for your SSG. A theme defines the look and feel of a site and provides basic structure and functionalities that you can customize. See [Step 2 Choose a theme](#step-2-choose-a-theme).
3. Choose where to host your portfolio. See [Step 3 Choose where to host your portfolio](#step-3-choose-where-to-host-your-portfolio).
4. Configure your portfolio and deploy it. See [Step 4 Configure the portfolio and deploy it](#step-4-configure-the-portfolio-and-then-deploy-it).

### Step 1 Choose an SSG

Before you decide where to host the portfolio, first choose what SSG you want to use for creating your portfolio. SSGs provide templates that allow you to create consistent layouts and designs across your website. These templates can include dynamic elements, such as navigation menus or sidebars, that are generated at build time. [Jekyll](https://jekyllrb.com/) and [Hugo](https://gohugo.io/) are two popular open source SSGs. Jekyll is Ruby-based while Hugo is Go-based. For a comparison of the two, see [Hugo vs. Jekyll](https://opensource.com/article/17/5/hugo-vs-jekyll).

After you have decided on an SSG, follow the official documentation to install the related software on your computer. For Jekyll, you can follow the [Jekyll QuickStart Guide](https://jekyllrb.com/docs/). For Hugo, follow the [Hugo QuickStart Guide](https://gohugo.io/getting-started/quick-start/). If you have never used SSGs before, you should create a dummy site following the QuickStart instructions to get some basic understandings how SSGs work.

### Step 2 Choose a theme

After choosing an SSG, you need to pick a theme. You can find Jekyll themes on [jekyllthemes.org](http://jekyllthemes.org/). For Hugo themes, go to [themes.gohugo.io](https://themes.gohugo.io/).

When choosing a theme, consider the following:

* Is the theme responsive? Responsive means the website can respond and adjust to the size of the screen it's being viewed on. Some older themes only look good on desktop or laptop computers. Those themes are not mobile-friendly. You can test whether a site is responsive by looking at the page from a mobile phone. For example, [my portfolio on GitHub](https://taolicd.github.io/) uses an older Jekyll theme and is not mobile friendly. I do intend to replace it soon. 
* If you want to monitor the web traffic, does the theme provide easy integration for web traffic monitoring?
* Do you want to have a form on your website that allows readers to contact you? If so, find a theme that provides such functionality.
* Do you want to allow readers to add comments on your website? If so, find a theme that provide easy integration with such services. Look for keywords, such as "Disqus", "Giscus", or "Utterances Comments", in the theme readme.

### Step 3 Choose where to host your portfolio

Now you need to decide where to host your portfolio. Both GitHub and GitLab can host your source code, provide Continuous Integration/Continuous Deployment (CI/CD) tools to manage your portfolio and deploy the website. 

For Netlify, typically you still need to have your source code hosted on GitHub or GitLab. Instead of using GitHub or GitLab's own deployment and hosting mechanisms, you use Netlify to manage the deployment and provide the hosting service. Personally I find Netlify's deployment and hosting mechanism a bit easier to use compared with the corresponding GitHub or GitLab services. 

### Step 4 Configure the portfolio and then deploy it

The configuration and deployment steps vary depending on the platform you choose. 

* For GitHub, your portfolio URL resembles `https://<username>.github.io`,  where `<username>` is your GitHub username. I have a Jekyll-based GitHub Pages on [taolicd.github.io](https://taolicd.github.io).
* For GitLab, your portfolio URL resembles `https://<username>.gitlab.io/<projectname>`,  where `<username>` is your GitLab username and `<projectname>` is your portfolio project name. I have a Hugo-based GitLab Pages on [tao_li.gitlab.io/hugo](https://tao_li.gitlab.io/hugo/).
* For Netlify, your portfolio URL resembles `https://<your-chosen-name>.netlify.app`, where the `<your-chosen-name>` is from one of the available names you get when creating the project. During your portfolio project creation, Netlify displays a list of suggested names you can choose from. Some are free and some you need to pay and the price is listed next to the name. I deployed a Hugo-based project on Netlify for free on [taoli.netlify.app](https://taoli.netlify.app/).

#### GitHub

To configure and deploy a GitHub Pages site, follow [these steps](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll) described in the official GitHub Pages documentation.

After you've enabled GitHub Pages and made any desired customizations, scroll back up to the GitHub Pages section in the repository settings. You'll find a message indicating the URL where your site is published (for example, "Your site is published at `https:/</>username>.github.io"`). Click on the provided URL to access your GitHub Pages site.

If you prefer to watch a YouTube video, try [How to Make a Data Science Portfolio With GitHub Pages video](https://www.youtube.com/watch?v=D9CLhQdLp8w&t=663s).

#### GitLab

GitLab Pages are very similar to GitHub Pages. Visit the official [GitLab Pages documentation](https://docs.gitlab.com/ee/user/project/pages/index.html) to get started.

To watch a YouTube video, try [How to make a website with Hugo and Gitlab](https://www.youtube.com/watch?v=-q6ZiCroiGM).

#### Netlify

Netlify makes deploying and managing a web project really easy. Hugo provides excellent documentation to explain how to host your site on Netlify with continuous deployment. See [Hugo Host on Netlify official documentation](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/).

#### Future improvements

After you've successfully created your portfolio and deployed to GitHub, GitLab, or Netlify, you can continue to add, modify, and publish content to your site by making changes to the repository and committing them. 

## What if I want to get a custom domain name?

If you don't like the free URL name that GitHub, GitLab, or Netlify provides, you can buy a custom domain name from a domain registry company such as [GoDaddy](https://www.godaddy.com/) or [Amazon Route 53](https://aws.amazon.com/route53/). The cost may range from a few dollars to hundreds of dollars per year depending on the popularity of the domain name you choose.

After you purchase the domain name, you then configure your portfolio to use this new custom domain name. 

* For GitHub Pages, refer to [Managing a custom domain for your GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#about-custom-domain-configuration). 
* For GitLab Pages, refer to [Configure Custom Domains](https://docs.gitlab.com/ee/user/project/pages/custom_domains_ssl_tls_certification/). 
* For Netlify, refer to [Custom Domains](https://docs.netlify.com/domains-https/custom-domains/).



