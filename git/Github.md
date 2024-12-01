#  Github

**目录**：

- [标题](#标题)
- [斜体](#斜体)
- [粗体](#粗体)
- [粗斜体](#粗斜体)
- [删除线](#删除线)
- [脚注](#脚注)
- [分割线](#分割线)
- [引用](#引用)
- [下划线](#下划线)
- [换行](#换行)
- [有序列表](#有序列表)
- [无序列表](#无序列表)
- [复选框](#复选框)
- [代码块](#代码块)
- [图片](#图片)
- [超链接](#超链接)
- [锚点](#锚点)
- [表格](#表格)
- [diff](#diff)
- [折叠](#折叠)
- [HTML 标签](#html标签)
- [转义字符](#转义字符)
- [公式](#公式)
- [shields](#徽章)
- [star-history](#star-历史)

# 标题

```markdown
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

# 字体

## 斜体

- `*斜体*`
- `_斜体_`

## 粗体

- `**粗体**`
- `__粗体__`

## 粗斜体

- `***粗斜体***`
- `___粗斜体___`

## 删除线

`~~文本~~`

## 脚注

`[^脚注]`

```markdown
鲁迅[^1]
[^1]: 原名周树人
```

鲁迅[^1]

[^1]: 原名周树人

# 分割线

三个以上的星号 ( `*` )、减号 ( `-` )、底线 ( `_` )

如：`---`

# 引用

`>` + 空格

# 下划线

使用 HTML 的 `u` 标签

# 换行

- `<br>`
- 上一行文本后补两个空格，实现换行

# 列表

## 有序列表

```markdown
1. 第一项
2. 第二项
3. 第三项
```

## 无序列表

```markdown
* 第一项
* 第二项
* 第三项

+ 第一项
+ 第二项
+ 第三项


- 第一项
- 第二项
- 第三项
```

# 复选框

```markdown
- [x] 已选中
- [ ] 未选中
```

- [x] 已选中
- [ ] 未选中

# 代码

- 反引号
- `code` 标签

```markdown
// 使用一对反引号
`socket`
```

## 代码块

````markdown
```javascript
console.log('Hello');
```
````

# 图片

- `![alt](URL title)`
- `img` 标签

```markdown
![baidu](http://www.baidu.com/img/bdlogo.gif "百度logo")
```

`alt` 和 `title` 属性可以省略：

- `alt` ：图片显示失败时替换文本
- `title`：鼠标悬停时显示的文本

仓库中的图片路径：`仓库地址/raw/分支名/图片路径`

# 超链接

- `[链接名称](链接地址)`
- `<链接地址>`

## 锚点

- 大写字母要小写

- 空格使用 `-` 代替

- 多级序号中要去除 `.`

- 特殊字符要省略，如：括号 `()`、<code>`</code>

- 回到顶部 `#`

  ```markdown
  [↑回到顶部](#)
  ```

## 高级链接

通过变量设置链接，实现复用

```markdown
[Google][google]

[google]:whttps://www.google.com/
```

# 表格

用 `|` 来分隔不同的单元格，用 `-` 来分隔表头和其他行

```markdown
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```

对齐方式：

- `:-`：左对齐
- `-:`：右对齐
- `:-:`：居中对齐

# diff

三个反引号 + `diff`

- `+`：新增
- `-`：删除

以及 `!` 和 `#`

```diff
+ 新增内容
- 删除内容
```

# HTML

## 折叠

```html
<details>
    <summary>标题</summary>
    内容
</details>
```

## 居中

```html
<div align="center">
    |  表头   | 表头  |
    |  ----  | ----  |
    | 单元格  | 单元格 |
    | 单元格  | 单元格 |
</div>
```

# 高级

## HTML 标签

- `kbd`：键盘
- `b`：加粗
- `i`：斜体
- `em`：斜体
- `sup`：上标
- `sub`：下标
- `br`：换行

## 转义字符

**转义字符**：`\`

- \\：反斜线

- \`：反引号

- \*：星号
- \_：下划线

## 公式

**公式**：

- `$`：行内公式
- `$$`：块级公式

$y=x^2$

# 徽章

绘制徽章：https://shields.io/

# star 历史

绘制 star-history：https://star-history.com/

```mark
## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=YasakaKanoko/coding_note&type=Date)](https://star-history.com/#YasakaKanoko/coding_note&Date)
```

[![Star History Chart](https://api.star-history.com/svg?repos=YasakaKanoko/coding_note&type=Date)](https://star-history.com/#YasakaKanoko/coding_note&Date)

[↑回到顶部](#)