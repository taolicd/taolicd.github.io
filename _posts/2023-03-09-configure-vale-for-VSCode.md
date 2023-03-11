---
layout: post
title: "Install and Configure the Vale linter to work with Visual Studio Code"
date: 2023-03-09
---

---
## Background

[Vale](https://vale.sh/) is an excellent open source grammar and style linter widely used by technical writers and software developers. This instruction describes how to install and configure Vale to work in Visual Studio Code.

## Prerequisite

* [Visual Studio Code](https://code.visualstudio.com/download) latest version

The steps below focus on MacOS and assume you have admin right to install software on your MacOS.

## Steps

1. On your terminal, type `brew install vale`. 

2. To confirm Vale is properly installed, type `vale -v` to check the Vale version. As of March 9, 2023, the latest version is 2.24.0.
    
3. Launch Visual Studio Code, click the **Extensions** icon on the vertical bar and type `Vale` in the Search box. Install the Vale extension. 

4. Before configuring the Vale extension, you need to get some Vale styles. For explanations about Vale styles, see the official [Vale docs](https://vale.sh/docs/topics/styles/). On your terminal, run the following command to get some example Vale styles:
   
   ```
   git clone https://github.com/errata-ai/vale-boilerplate.git
   ```
   
5. In your Visual Studio Code, click the **Manage** button at the bottom left corner and then choose **Settings**. Locate Vale setting and configure the **Vale CLI** to point to the absolute path of the Vale config file `.vale.ini` you get in step 4. For example, I cloned the repo in step 4 to `/Users/taoli/` so I configured mine as `/Users/taoli/vale-boilerplate/.vale.ini`. You can customize this `.vale.ini` file to specify where the style rules are, which file types you want Vale to lint. Vale supports Markdown, HTML, TXT, and AsciiDoc files. For details about this `.vale.ini` file, see [the official Vale configuration topic](https://vale.sh/docs/topics/config/).
   
6. Exit Visual Studio Code and start it again. Open a Markdown file and you should see the Vale linter working with wiggle lines flagging the sentences. 

