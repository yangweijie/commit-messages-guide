# 提交消息指南

[![感谢!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/RomuloOliveira)

理解提交消息的重要性以及如何写好它们的指南。

这可能有助于你了解什么是提交，为什么写好提交消息是很重要的、最佳实践和一些建议来计划和 (重新) 写一篇好的提交历史。

## 可用语言

- [英语](README.md)
- [葡萄牙语](README_pt-BR.md)
- [德语](README_de-DE.md)
- [西班牙语](README_es-AR.md)
- [意大利语](README_it-IT.md)
- [汉语](README_zh-CN.md)

## 什么是 "commit" ?

简而言之，提交是本地文件的_快照_，写在本地存储库中。

与一些人的想法相反， [git 不存储文件间的差异而是全版本](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences)。

对于没有从一个提交更改为另一个提交的文件，git 只存储到之前已经存储的相同文件的链接。

下图显示了 git 如何随着时间的推移存储数据，其中每个 “版本” 都是提交：

![](https://i.stack.imgur.com/AQ5TG.png)

## 为什么提交信息很重要？

- 加快和简化代码审查
- 助理解一个变更
- 解释只能用代码描述的 “为什么”
- 帮助未来的维护人员了解更改的原因和方式，使故障排除和调试变得更容易

为了最大限度地发挥这些成果，我们可以使用下一节中描述的一些好的做法和标准。

## 好的实践

这里有从我的经验、互联网文章和其他指南中收集的一些实践。如果你有其他 (或者不同意部分内容)，请随时提出请求并做出贡献。

### 使用命令式的形式

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

但是为什么要使用命令式形式呢？

提交消息描述了引用的更改实际上**做**了什么，它的效果，而不是做过什么。

[Chris Beams的这篇优秀的文章](https://chris.beams.io/posts/git-commit/)  给我们一个简单的句子，可以帮助我们用命令式的形式写出更好的提交消息:

```
If applied, this commit will <commit message>
```

Examples:

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### 大写首字母

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

首字母大写的原因是遵循句子开头使用大写字母的语法规则。这种做法的使用可能因人而异，因团队而异，甚至因语言而异。

不管是否大写，重要的一点是坚持一个标准并遵循它。

### 尝试交流更改所做的事情，而不必查看源代码

```
# Good
Add `use` method to Credit model

```

```
# Bad
Add `use` method
```

```
# Good
Increase left padding between textbox and layout frame
```

```
# Bad
Adjust css
```

在许多情况下 (例如多次提交、多次更改和重构)，帮助审阅者理解提交者的想法是有用的。

### 使用消息正文解释 “为什么” 、 “如何” 和其他细节
```
# Good
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because the cart was calling the backend implementation
incorrectly.
```

```
# Good
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are pickleable by default
```

```
# Good
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

消息的主题和正文用空行分隔。
额外的空行被认为是消息正文的一部分。

像 `-`, `*` and \` 这样的字符是提高可读性的元素。

### 避免没有任何上下文的通用消息或消息

```
# Bad
Fix this

Fix stuff

It should work now

Change stuff

Adjust css
```

### 限制列的数量

[推荐](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) 为主题使用最多 50 个字符，为正文使用 72 个字符。

### 保持语言的一致性

对于项目所有者: 选择一种语言，并使用该语言编写所有提交消息。理想情况下，它应该与代码注释、默认翻译区域设置 (对于本地化项目) 等相匹配。

对于贡献者: 使用与现有提交历史相同的语言编写提交消息。

```
# Good
ababab Add `use` method to Credit model
efefef Use InventoryBackendPool to retrieve inventory backend
bebebe Fix method name of InventoryBackend child classes
```

```
# Good (Portuguese example)
ababab Adiciona o método `use` ao model Credit
efefef Usa o InventoryBackendPool para recuperar o backend de estoque
bebebe Corrige nome de método na classe InventoryBackend
```

```
# Bad (mixes English and Portuguese)
ababab Usa o InventoryBackendPool para recuperar o backend de estoque
efefef Add `use` method to Credit model
cdcdcd Agora vai
```

### 模板

这有一个模板，[Tim Pope的出稿](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), 出现在 [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).

```
Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

## Rebase vs. Merge

本章节是  Atlassian's 精品教程 ["Merging vs. Rebasing"](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)的**精华**。

![](https://wac-cdn.atlassian.com/dam/jcr:01b0b04e-64f3-4659-af21-c4d86bc7cb0b/01.svg?cdnVersion=hq)

### Rebase

**TL;DR:** 在基分支上逐个应用分支提交，生成新树。

![](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=hq)

### Merge

**TL;DR:** 使用两个分支之间的差异创建一个新的提交，称为 (适当地) 合并提交。

![](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=hq)

### 为什么有些人相对于合并更喜欢变基？

比起合并，我更喜欢变基。原因包括:

* 它生成 “干净” 的历史记录，没有不必要的合并提交
* _你所看到的是你所得到的，也就是说，在代码审查中，所有的更改都来自一个特定的、有标题的提交，避免了隐藏在合并提交中的更改
* 提交者解决了更多的合并，每个合并更改都包含在带有适当消息的提交中
    * 挖掘和审查合并提交并不寻常的，所以避免它们可以确保所有的更改都有属于它们的提交

### 什么时候压缩

"Squashing" 是将一系列提交合并为单个提交的过程。

它在几种情况下都很有用，例如:
- 减少很少或没有上下文的提交 (拼写错误更正、格式、忘记的东西)
- 将单独的更改连接在一起使用时更有意义
- 正在重写正在进行的提交

### 什么时候避免变基或压缩？

避免在公共提交或多人工作的共享分支中进行变基和压缩。
Rebase 和 squash 重写历史记录并覆盖现有提交，在共享分支上的提交上执行 (即推送到远程存储库或来自其他分支的提交) 可能会造成混乱，人们可能会因为不同的树和冲突而失去他们的变化 (无论是在本地还是远程)。

## 有用的 git 命令

### rebase -i

它可以压缩提交、编辑消息、重写/删除/重新排序提交等。

```
pick 002a7cc Improve description and update document title
pick 897f66d Add contributing section
pick e9549cf Add a section of Available languages
pick ec003aa Add "What is a commit" section"
pick bbe5361 Add source referencing as a point of help wanted
pick b71115e Add a section explaining the importance of commit messages
pick 669bf2b Add "Good practices" section
pick d8340d7 Add capitalization of first letter practice
pick 925f42b Add a practice to encourage good descriptions
pick be05171 Add a section showing good uses of message body
pick d115bb8 Add generic messages and column limit sections
pick 1693840 Add a section about language consistency
pick 80c5f47 Add commit message template
pick 8827962 Fix triple "m" typo
pick 9b81c72 Add "Rebase vs Merge" section

# Rebase 9e6dc75..9b81c72 onto 9e6dc75 (15 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into the previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

#### fixup

使用它可以轻松清理提交，而不需要更复杂的 rebase。
[这篇文章](http://fle.github.io/git-tip-keep-your-branch-clean-with-fixup-and-autosquash.html)有非常好的例子来说明如何以及何时去做。

### cherry-pick

应用你在错误的分支上提交的提交非常有用，而不需要再次编码。

示例:

```
$ git cherry-pick 790ab21
[master 094d820] Fix English grammar in Contributing
 Date: Sun Feb 25 23:14:23 2018 -0300
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### add/checkout/reset [--patch | -p]

假设我们有以下差异:

```diff
diff --git a/README.md b/README.md
index 7b45277..6b1993c 100644
--- a/README.md
+++ b/README.md
@@ -186,10 +186,13 @@ bebebe Corrige nome de método na classe InventoryBackend
 ``
 # Bad (mixes English and Portuguese)
 ababab Usa o InventoryBackendPool para recuperar o backend de estoque
-efefef Add `use` method to Credit model
 cdcdcd Agora vai
 ``

+### Template
+
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in the [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contributing

 Any kind of help would be appreciated. Example of topics that you can help me with:
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

我们可以用 `git add -p` 只添加我们想要的补丁，而不需要更改已经编写的代码。
将较大的更改拆分为较小的提交或重置/签出特定更改很有用。

```
Stage this hunk [y,n,q,a,d,/,j,J,g,s,e,?]? s
Split into 2 hunks.
```

#### hunk 1

```diff
@@ -186,7 +186,6 @@
 ``
 # Bad (mixes English and Portuguese)
 ababab Usa o InventoryBackendPool para recuperar o backend de estoque
-efefef Add `use` method to Credit model
 cdcdcd Agora vai
 ``

Stage this hunk [y,n,q,a,d,/,j,J,g,e,?]?
```

#### hunk 2

```diff
@@ -190,6 +189,10 @@
 ``
 cdcdcd Agora vai
 ``

+### Template
+
+This is a template, [written originally by Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), which appears in the [_Pro Git Book_](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project).
+
 ## Contributing

 Any kind of help would be appreciated. Example of topics that you can help me with:
Stage this hunk [y,n,q,a,d,/,K,j,J,g,e,?]?

```

#### hunk 3

```diff
@@ -202,3 +205,4 @@ Any kind of help would be appreciated. Example of topics that you can help me wi

 - [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
 - [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
+- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
```

## 其他有趣的东西

https://whatthecommit.com/

## 喜欢吗？

[Say thanks!](https://saythanks.io/to/RomuloOliveira)

## 贡献

我们将感谢您的任何帮助。 可以帮助我的示列:

- 语法和拼写更正
- 翻译成其他语言
- 源引用的改进
- 信息不正确或不完整

## 启发、来源和进一步阅读

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [Pro Git Book - Commit guidelines](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [Pro Git Book - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
