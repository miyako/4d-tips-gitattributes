# 4d-tips-gitattribute
.gitattributesの検証

## Draft

When you create a Git repository for a 4D project, you may add a [.gitattributes](https://git-scm.com/docs/gitattributes) file.

c.f. see [vdelachaux/4DPop-Git](https://github.com/vdelachaux/4DPop-Git/) for a [basic example](https://github.com/4d-depot/EA_Recipes/blob/master/.gitattributes).

this file helps Git parse and display source code using the most appropriate syntax highlighter and the correct encoding.

---

the compiler has an option to generate a [symbol file](https://doc.4d.com/4Dv19/4D/19/Compiler-page.300-5416922.en.html) that explains which data type has been selected for each symbol, the amount of memory requires to manage process and interprocess variables (same amount of memory is needed for each process, whether you use the variable or not; the reason why developers today limit the number of process variables in production). another useful piece of information is the thread-safety of each project method and each member function of each class.

**Note**: you can also use [Compile project](https://doc.4d.com/4Dv19/4D/19.6/Compile-project.301-6269659.en.html)

what you may not appreciate is that in 4D you can use extended characters (within reasonable bounds, please don't go wild and use emoji...😣)  as tokens.

Japanese 4D developers have been using such characters for their tables, fields and variables. in the symbols file, such characters are represented in UTF-8 encoding. this is relatively recent change made in v18.5 Hotfix 1 and v19 (ACI0102014).

for historic reasons, this file has no byte-order-mark and the the file extension is .txt. as such, it may not display well on Git.

you may think you can easily fix this annoyance with the following line in .gitattributes:

```
+*_symbols.txt    text working-tree-encoding=UTF-8 eol=CR
```

unfortunately there does not seem any ways to handle `CR` (without the `LF`) in Git

c.f. https://docs.github.com/en/get-started/getting-started-with-git/configuring-git-to-handle-line-endings
