# 安装包 / 草案

----


## 安装包描述文件

每一个安装包必须提供根目录下的安装包描述器："package.json"。

### 必须字段

- family
- name
- version

### 可选字段

- description
- keywords
- author
- repository
- bugs
- license
- scripts

## 扩展代码

**基本示例**

```
{
    "family": "arale",
    "name": "overlay",
    "version": "1.0.0",
    "description": "Overlay is a mask covering.",
    "keywords": ["mask", "dom"],
    "author": "Hsiaoming Yang <lepture@me.com>",
    "repository": {
        "type": "git",
        "url": "https://github.com/arale/overlay.git"
    },
    "bugs": {
        "url": "https://github.com/arale/overlay/issues"
    },
    "license": {
        "type": "BSD",
        "url": "http://opensource.org/licenses/BSD-2-Clause"
    },
    "scripts": {
        "prebuild": "prebuild.js",
        "test": "make test"
    }
}
```

**最简代码示例**

```
{
    "family": "arale",
    "name": "overlay",
    "version": "1.0.0"
}
```