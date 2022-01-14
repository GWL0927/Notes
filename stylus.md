# 缩进

Stylus 语法是 “python 式”的 （即，基于缩进）。空格很重要，所以我们使用_缩进_和_突出_来代替 `{` 和 `}`，如下所示：

```stylus
body
  color white
```

如果喜欢也可以使用冒号来分割属性和值

```stylus
body
  color: white
```

# 规则集

和 CSS 一样，Stylus 允许通过逗号分隔，一次为多个选择器定义属性。

```stylus
textarea, input
  border 1px solid #eee
```

也可以通过换行书写来实现：

```stylus
textarea
input
  border 1px solid #eee
```

最终都会编译为：

```stylus
textarea,
input {
  border: 1px solid #eee;
}
```

# 父级引用

`&` 符号代表父级选择器。下面的例子中，（`textarea`和`input`）两个选择器的伪类`:hover`都会改变 `color` 属性。

```stylus
textarea
input
  color #A7A7A7
  &:hover
    color #000
```

编译为：

```stylus
textarea,
input {
  color: #a7a7a7;
}
textarea:hover,
input:hover {
  color: #000;
}
```

# 属性查找

```stylus
#logo
   position: absolute
   top: 50%
   left: 50%
   width: w = 150px
   height: h = 80px
   margin-left: -(w / 2)
   margin-top: -(h / 2)
```

无需定义变量 `w` 和 `h`，**我们可以仅仅通过前置 `@` 字符在属性名前来访问该属性名对应的值**：

```stylus
 #logo
   position: absolute
   top: 50%
   left: 50%
   width: 150px
   height: 80px
   margin-left: -(@width / 2)
   margin-top: -(@height / 2)
```