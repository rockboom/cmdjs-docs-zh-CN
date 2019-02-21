# 公共模块定义 / 草案

------

为了在**基于浏览器**的环境中保持模块的互相引用，这篇规范说明了应该如何编写模块。要想支持互相操作的模块，这篇规范定义了模块系统必须提供的最少的功能。

- 模块就是一个单文件
- 不应该引入模块范围作用域内新的自由变量
- 必须是懒执行。

## 模块定义

用`define`关键字定义模块，`define`是一个函数。

```js
define(factory);
```

1. `define`函数接受一个参数，也就是模块工厂。
1. `factory`可能是一个函数或其他的有效值。
1. 如果`factory`是一个函数，如果指定了函数的前三个参数，那么必须按照指定的顺序"require", "exports", 和 "module"传入。
1. 如果`factory`不是一个函数，那么模块的exports会被设置成对相关。

## 模块的上下文

在一个模块内有三个自由变量：`require`, `exports` 和 `module`。

```js
define(function(require, exports, module) {

  // 模块的代码

});
```

### `require`函数

1. `require`是一个函数

    1. `require`接受一个模块标识符。
    1. `require`返回外部模块导出的API。
    1. 如果请求的模块不能返回，`require`应该返回null。

1. `require.async`是一个函数
    
    1. `require.async`接受一个模块标识符列表和一个可选的回调函数。
    1. 回调函数接受模块导出为函数参数，并按照与第一个参数相同的顺序列出。
    1. 如果请求的模块不能返回，回调函数相应的也会接受null。

### `exports`对象

在模块内有一个自由变量叫做`exports`，`exports`是一个对象，模块执行时会把它的API加到对象上。

### `module`d对象

1. `module.uri`

    完全解析的模块路径

1. `module.dependencies`

    模块所需的模块标识符列表。

1. `module.exports`

    模块导出的API，和`exports`y相同。

## 模块标识符

1. 一个模块标识符必须是一个**字面量**字符串。
2. 模块标识符可能没有像`.js`这样的文件扩展名。
3. 模块标识符应该是一个短划线连接的字符串，比如`foo-bar`。
4. 模块标识可能是一条相对路径，比如`./foo` 和 `../bar`。

## 示例代码

math.js
```js
define(function(require, exports, module) {
  exports.add = function() {
    var sum = 0, i = 0, args = arguments, l = args.length;
    while (i < l) {
      sum += args[i++];
    }
    return sum;
  };
});
```
increment.js
```js
define(function(require, exports, module) {
  var add = require('math').add;
  exports.increment = function(val) {
    return add(val, 1);
  };
});
```

program.js
```js
define(function(require, exports, module) {
  var inc = require('increment').increment;
  var a = 1;
  inc(a); // 2

  module.id == "program";
});
```


**Wrapped modules with non-function factory**

object-data.js
```js
define({
    foo: "bar"
});
```

array-data.js
```js
define([
    'foo',
    'bar'
]);
```

string-data.js
```
define('foo bar');
```

