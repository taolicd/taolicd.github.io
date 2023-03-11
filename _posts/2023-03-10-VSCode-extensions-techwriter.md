---
layout: post
title: "Visual Studio Code extensions for Tech Writers"
date: 2023-03-10
---

---

This post lists Visual Studio Code extensions that technical writers may find useful. 

### Version control

You can do all Git-related commands within the VS Code terminal. I find the following extensions useful.

* **Git Graph**: Visual and easy to use. I use it for cherry-picking so I do not need to use git log to see the checksum.

* **GitLens**: This is super powerful and popular.

For more Git related extensions, see [The best VS Code extensions to supercharge Git](https://dev.to/jamieswift90/the-best-vs-code-extensions-to-supercharge-git-yes-there-s-more-than-gitlens-4588)

In VS Code, you do not need a separate extension to resolve Git merge conflict.

### Graphing tools

* **PlantUML**: Create and preview UML diagrams in VS Code. Alternatively, you can use Amazon's internal online version.

* **Draw.io**: Draw and preview draw.io style diagrams. Alternatively, you can use Amazon's internal draw.io online version.
* **Mermaid Preview**: Mermaid diagram preview in VS Code.
  
### Style and spell checking

* **Vale**: For configuration steps, see my 2023-03-09 post "Install and Configure the Vale CLI to work with Visual Studio Code".
* **Code Spell Checker**: This tool is helpful for catching spelling errors in code blocks. Vale ignores code blocks as far as I know.

### Other useful extensions

* **Swagger Viewer**: For preview Swagger and OpenAPI yml files in VS Code.
* **Word Count**: For counting the number of words in your file.
* **Office Viewer**: To view MS Word, Excel etc in VS Code.
* **Prettier**: Code formatter.
* **Thunder client**: Lightweight REST API client in VS Code.
* **VSCode-Pandoc**: To render PDF, Word, or HTML in VS Code. You still need to install pandoc separately as the prerequisite.
* **Readability check**: To display the readability score of text in plain text or Markdown files.

### Caveat
Do not install too many extensions. Having too many extensions might slow down the performance drastically. At one point, I had to un-install VS Code including all the extensions and reinstall it to resolve the performance issue.