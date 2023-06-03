---
layout: post
title: Test table sorting with Datatable
date: 2023-06-03
datatable: true
---

This post is for testing how to create a table in Jekyll Markdown that uses [JQuery's DataTables](https://datatables.net/) feature.

## Steps

1. Creat an HTML file in the `_includes` folder that contains the script to use Datatables. For example, I created [this file](https://github.com/taolicd/taolicd.github.io/blob/master/_includes/datatables.html). Here I named my file `datatables.html` and you can name it with any name as you want.
2. Edit the `_layouts/default.html` to include the line that references the file created in step 1. For example, I added line 27 in my [default.html](https://github.com/taolicd/taolicd.github.io/blob/master/_layouts/default.html) to refer to my file from step 1. 
3. Create a blog post as usual and make sure to include `datatable: true` in the frontmatter. 
4. After creating a table as usual, add a line `{: .datatable}`. This is my [current example post in Markdown](https://github.com/taolicd/taolicd.github.io/blob/master/_posts/2023-06-03-table-sorting.md).

For example, the table source code looks like:

```
Food    | Quantity | Time sold         | Cashier
--------|----------|-------------------|--------
Apples  | 15       | 6-25-2023 9:00:01 | A
Bananas | 10       | 6-25-2023 9:03:55 | B
Kiwis   | 3        | 6-25-2023 9:06:37 | C
Oranges | 5        | 6-25-2023 9:07:24 | D
{: .datatable}
```

This is the output you see in HTML:

Food    | Quantity      | Time sold         | Cashier
------- | ------------- | ----------------- | -----------
Apples  |   15          | 6-25-2023 9:00:01 | A
Bananas |   10          | 6-25-2023 9:03:55 | B
Kiwis   |   3           | 6-25-2023 9:06:37 | C
Oranges |   5           | 6-25-2023 9:07:24 | D
{: .datatable}

