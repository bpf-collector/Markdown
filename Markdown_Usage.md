<!--
 * @Author       : bpf
 * @Date         : 2020-09-08 12:17:09
 * @Description  : 学习使用markdown
 * @LastEditTime : 2020-09-08 16:26:21
-->

# 学习使用Markdown

## 1. 标题

> 1. ATX形式
>       + 使用 "#" 定义1-6级标题，个数表示标题级别。
> 2. SeText形式
>       + 一级标题可以使用 "==="，二级标题可以使用 "---"。

<kbd>Example:</kbd>

```markdown
一级标题
===
二级标题
---
### 三级标题
```

> 一级标题
> ===
> 二级标题
> ---
> ### 三级标题

## 2. 段落

> 1. 段为使用两个以上空格加回车
> 2. 直接使用空行

## 3. 字体

<kbd>Example:</kbd>

```markdown
*斜体*          前后1个"*"|"_"
**粗体**        前后2个"*"|"_"
***粗斜体***    前后3个"*"|"_"
```

> *斜体*
> **粗体**
> ***粗斜体***

## 4. 分割线

> 一行中使用3个会以上的星号|减号|下划线来建立一个分割线，其间只许存在空格。

```markdown
***
_ _ _
-----------------------
```

> ***
> _ _ _
> -----------------------

## 5. 删除线

<kbd>Example:</kbd>

```markdown
~~删除线~~    前后加上"~~"
```

> ~~删除线~~

## 6. 下划线

<kbd>Example:</kbd>

```markdown
<u>下划线</u> 使用HTML语法\<u\>\<\/u\>
```

> <u>下划线</u>

## 7. 脚注

<kbd>Example:</kbd>

```markdown
脚注：我们一起学习[^markdown]吧
[^markdown]: markdown文件以.md结尾。
```

>脚注：我们一起学习[^markdown]吧

## 8. 列表

> 1. 无序列表可以使用星号|加号|减号进行定义，标记之后需添加一个空格。
> 2. 有序列表直接使用123，在标记之后添加.和一个空格。

<kbd>Example:</kbd>

```markdown
1. 第一项
    * 1.1
    * 1.2
2. 第二项
    + 2.1
    + 2.2
3. 第三项
    - 3.1
    - 3.2
```

> 1. 第一项
>     * 1.1
>     * 1.2
> 2. 第二项
>     + 2.1
>     + 2.2
> 3. 第三项
>     - 3.1
>     - 3.2

## 9. 区块

> 这是一个区块，使用">"和一个空格进行定义，对应与HTML的`<blockquote>`

<kbd>Example:</kbd>

```markdown
> 最外层
>> 第一层
>>> 第二层
```

> 最外层
>> 第一层
>>> 第二层

## 10. 代码

> 1. 单行代码
>       + 使用<kbd>``</kbd>
> 2. 代码块
>       + 使用4个空格或<kbd>Tab</kbd>键
>       + 开头和结尾都使用<kbd>```</kbd>，在开头处可加上语言类型。

<kbd>Example:</kbd>

`prinf()函数`

```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```

> `prinf()`函数
>
> ```javascript
> $(document).ready(function () {
>     alert('RUNOOB');
> });
> ```

## 11. 链接

> 1. 普通链接
>       + `[链接名称](链接地址 "可选标题")`
>       + `<链接地址>`
> 2. 高级链接
>       + 使用链接变量，变量赋值在文档末尾进行

<kbd>Example:</kbd>

```markdown
1. 普通: 点击链接[Markdown教程](https://www.runoob.com/markdown/md-tutorial.html)
2. 普通: 点击链接直接跳转到Markdown官方文档：<http://xianbai.me/learn-md/article/about/readme.html>
3. 高级: 这个链接使用 translate 作为网址变量[Youdao][translate]

[translate]: http://fanyi.youdao.com
```

> 1. 普通: 点击链接[Markdown教程](https://www.runoob.com/markdown/md-tutorial.html)
> 2. 普通: 点击链接直接跳转到Markdown官方文档：<http://xianbai.me/learn-md/article/about/readme.html>
> 3. 高级: 这个链接使用 translate 作为网址变量[Youdao][translate]

## 12. 图片

> 1. 普通方法
>       + `![alt 属性文本](图片地址 "可选标题")`，其中<kbd>alt 属性文本</kbd>为图片无法显示时的提示性文本
> 2. 高级方法
>       + 使用链接变量，变量赋值在文档末尾进行
> 3. HTML方法
>       + `<img src="xxx" width="xx%">`

<kbd>Example:</kbd>

```markdown
1. 普通: ![alt Runoob图标](http://static.runoob.com/images/runoob-logo.png "RUNOOB")
2. 高级: 这个图片使用runoob作为链接变量[RUNOOB][runoob]
3. HTML: <img src="http://static.runoob.com/images/runoob-logo.png" width="40%">

[runoob]: http://static.runoob.com/images/runoob-logo.png
```

> 1. 普通: ![Runoob图标](http://static.runoob.com/images/runoob-logo.png "RUNOOB")
> 2. 高级: 这个图片使用runoob作为链接变量[RUNOOB][runoob]
> 3. HTML: <img src="http://static.runoob.com/images/runoob-logo.png" width="40%">

## 13. 表格

<kbd>Example:</kbd>

```markdown
| 左对齐  |  右对齐 | 居中对齐 |
| :------ | ------: | :------: |
| 单元格1 | 单元格2 | 单元格3  |
| 单元格4 | 单元格5 | 单元格6  |
```

> | 左对齐  | 右对齐 | 居中对齐 |
> | :----- | ----:  | :----:  |
> | 单元格1 | 单元格2 | 单元格3 |
> | 单元格4 | 单元格5 | 单元格6 |

## 14. 转义

| 符号  |  含义  | 符号  |  含义  | 符号  |   含义   |
| :---: | :----: | :---: | :----: | :---: | :------: |
|   \   | 反斜线 |  {}   | 花括号 |   +   |   加号   |
|   `   | 反引号 |  []   | 方括号 |   -   |   减号   |
|   *   |  星号  |  ()   | 小括号 |   .   | 英文句点 |
|   _   | 下划线 |   #   | 井字号 |   !   |  感叹号  |

## 15. 公式

> 当你需要在编辑器中插入数学公式时，可以使用两个美元符 $$ 包裹 TeX 或 LaTeX 格式的数学公式来实现.

<kbd>Example:</kbd>

```LaTeX
$$
\mathbf{V}_1 \times \mathbf{V}_2 =
\begin{vmatrix}  
    \mathbf{i} & \mathbf{j} & \mathbf{k} \\
    \frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
    \frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$
```

$$
\mathbf{V}_1 \times \mathbf{V}_2 =
\begin{vmatrix}  
    \mathbf{i} & \mathbf{j} & \mathbf{k} \\
    \frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
    \frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$

## 16. HTML元素

> 目前支持的 HTML 元素有：`<kbd> <b> <i> <em> <sup> <sub> <br>`

## 17. Task List

> + [ ] 1
> + [x] 2
>   + [x] 2.1
> + [x] 3

<!-- 脚注 -->
[^markdown]: markdown文件以.md结尾。

<!-- 链接：高级链接的网址变量赋值 -->
[translate]: http://fanyi.youdao.com

<!-- 图片：高级链接的网址变量赋值 -->
[runoob]: http://static.runoob.com/images/runoob-logo.png
