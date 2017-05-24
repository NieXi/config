# README

本仓库包含个人使用的一些配置文件

## 1. Git 相关配置

### 1.1 随机生成 git commit 信息

```shell
git commit -m"`curl -s http://whatthecommit.com/index.txt`"
```

### 1.2 设置 git commit 模板

1. 在用户目录下新建自己的模板文件：比如 .gitmessage

    ```config
    What:

    Why:

    How:

    ```
2. 在配置文件 .gitconifg 中添加：

    ```config
    [commit]
    template = ~/.gitmessage
    ```
3. 设置默认编辑 commit 信息编辑器为 Gvim：

    ```shell
    git config --global core.editor gvim
    ```
