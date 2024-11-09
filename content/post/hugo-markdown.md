---
title:       "Hugo对Markdown支持情况测试"
subtitle:    ""
description: ""
date:        2018-06-04
author:      "Pig Logic Park Studio"
image:       ""
tags:        ["Hugo", "tag2"]
categories:  ["Hugo" ]
---
本文主要内容是测试Hugo对Markdown的支持情况，方便后续写作时查阅。

标题
在行首以井号#加空格指定，几个井号就代表几级标题。

# 1级标题
## 2级标题
...
###### 6级标题
段落
段落之间以至少一行空行为分隔，也可以通过在行尾加 2个空格 强制段落内换行。

段落一的第一行
段落一的第二行
…
段落一的第N行

段落二的第一行

文本样式
字体样式常用的有粗体、斜体、删除线等。
*斜体字* 对应 斜体字
**粗体字** 对应 粗体字
~~删除线~~ 对应 删除线
`行内代码` 对应 行内代码

还有一些样式原生不支持，但是可以通过html间接支持。
<u>下划线</u> 对应 下划线
H<sub>2</sub>O 对应 H2O
爆米<sup>TM</sup> 对应 爆米TM
<span style="color: orange">前景色</span>对应 前景色
<span style="background: orange">背景色</span>对应 背景色

列表
列表分为有序列表和无序列表。
以数字+ . 表示有序列表项：

有序子项目1
以 - 或 + 表示无序列表项：

无序子项目
可以混合使用，注意同级列表以空格对齐。

有序子项目一
无序子项目 1
无序子项目 2
有序子项目二
无序子项目 a
无序子项目 b
图片
一般格式是 ![文字描述](链接) ：
org-mode-logo

这种格式显示图片不能控制对齐和大小，需要的话可以采取raw html的方法：

1
2
3
<p align="center">
    <img src="https://i.loli.net/2021/01/31/4ZHoWduI59fiqJY.png" width="100" />
</p>


tip

需要注意的是，Hugo 0.60以上版本需要设置markup.goldmark.renderer的unsafe值为true才支持

链接可以是网络URL，也可以是相对路径。
相对路径的话需要注意本地路径和(网站)部署路径可能不一致的问题。
一般还是通过工具 (如 PicGo) 上传到图床更方便。

链接
链接分为外部链接和内部链接，格式都是 [文字描述](链接) 。
外部链接就是我们常用的URL，这里不赘述。
内部链接，也叫anchor，用来引用当前文档的某个位置。
可以通过以下方式标记位置：

1
{#target}
其中 target 需要取一个有意义的、文档内唯一的名字。
然后通过以下方式引用，与html的锚类似：

1
[文字描述](#target)
跳转回本章节起始位置☞ back 。

引用与代码
引用名人名言：

1
> Stay Hungry. Stay Foolish -- Steve Jobs
Stay Hungry. Stay Foolish – Steve Jobs

引用代码：

1
2
3
```语言(可以不填，但是没有语法高亮)
代码内容
```
C代码：

1
2
3
4
5
6
```c
int sayHello()
{
    printf("Hello!\n"); // hello everyone
}
```
1
2
3
4
int sayHello()
{
    printf("Hello!\n"); // hello everyone
}
表格
创建表格十分简便，基本上组合使用 | - 即可。
对齐不是硬性要求，第一列 | 也可以省略。

1
2
3
4
5
6
7
8
9
简写版本：
key | value
--- | ---
long key | long测试中文

美观版本：
| key      | value       |
|----------|-------------|
| long key | long测试中文 |
key	value
long key	long测试中文
另外在 spacemacs 中使用 Tab 和 Shift Tab 可以自动对齐表格和在单元格内跳转，谁用谁知道！ 😄


分隔线
3个以上横杠 - 单独为一行可以显示分隔线：

emoji表情
支持Github的emoji表情，格式为 :emoji代码: ，具体可以查阅 👉 这里 。

公式
比较考验排版能力的数学公式，通过LaTex表示毫无压力、逼格满满。
正文显示公式： $LaTex公式$ 

单独显示公式： $$LaTex公式$$

另外根据mathjax的说明，公式中的换行\\需要写成\\\\：

1
2
3
4
5
6
7
8
\begin{equation}
 \begin{split}
 (a + b)^3
    &= (a + b)(a + b)^2            \\\\
    &= (a + b)(a^2 + 2ab + b^2)    \\\\
    &= a^3 + 3a^2b + 3ab^2 + b^3
 \end{split}
\end{equation}
 

tip

支持显示公式需要设置mathjax选项为true，支持单个$还需要设置mathjaxEnableSingleDollar为true。

脚注Footnote
脚注主要有数字脚注1和命名脚注2。
在文章末尾行首以下面的方式可以定义脚注：
[^数字]: 数字脚注内容
[^名字]: 命名脚注内容
在文中通过 [^数字] 或者 [^名字] 引用即可。
不过命名脚注显示在页面上还是数字脚注的形式。。。

任务列表
任务列表是在无序列表的基础上扩展的，属于GFM标准。

1
2
- [ ] 待测试
- [x] 已测试
 待测试
 已测试