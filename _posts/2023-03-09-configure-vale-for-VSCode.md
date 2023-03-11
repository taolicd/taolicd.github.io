---
layout: post
title: "Install and Configure the Vale linter to work with Visual Studio Code"
date: 2023-03-09
---

---
# #Background

The [Vale CLI](https://vale.sh/) is an excellent open source grammar and style linter widely used by technical writers and software developers. This instruction explains how to install and configure Vale to work in Visual Studio Code.

## Prerequisites

* Visual Studio Code latest version

The steps below focus on MacOS and assume you have admin right to install software.

## Steps

1. On your terminal, type `brew install vale`. 

2. To confirm your Vale is properly installed, type `vale -v` to check the Vale CLI version. As of March 9, 2023, the latest version is 2.24.0.
    
3. Launch Visual Studio Code, click the **Extensions** icon on the vertical bar and type `Vale` in the Search box. Install the Vale extension. 

4. Before you configure the Vale extension, you need to get some Vale style packages. For explanations about Vale styles, see the official [Vale docs](https://vale.sh/docs/topics/styles/). On your terminal, run the following command to get some example Vale styles:
   ```
   git clone https://github.com/errata-ai/vale-boilerplate.git
   ```
   
5. In your VS Code, click the Manage button at the bottom left corner and then choose **Settings**, 
locate Vale setting and configure the **Vale CLI** to point to the absolute path of the Vale config file `.vale.ini` you get in step 5.0. For example, I cloned the repo in step 4 to `/Users/taoli/` so I configured mine as `/Users/taoli/vale-boilerplate/.vale.ini`

6. Exit VS Code and start it again. Open a Markdown file and you should see the Vale linter working.

