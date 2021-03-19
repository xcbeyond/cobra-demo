# cobra-demo

Cobra demo。

## Cobra介绍

`Cobra` 既是一个用来创建强大的现代CLI命令行的golang库，也是一个生成程序应用和命令行文件的程序。

## 快速入门
### 前提条件&环境

* 操作系统：Window10
* Go环境：go 1.16
* Go开发IDE：VSCode

### 安装

使用 `go get` 命令获取最新版本的 `cobra` 库。下面命令将会安装 `cobra` 及其相关依赖包：

```
go get -u github.com/spf13/cobra/cobra
```

安装完 `cobra` 后，打开 `GOPATH` 目录，`bin` 目录下会下载好 `cobra.exe` 程序。

### 程序初始化

假设现需要开发一个基于 `cobra` 的 `CLI` 的命令行程序，命名为 `cobra-demo`。`cobra` 提供了初始化命令 `cobra init` 进行快速初始化创建，将会自动创建程序工程。

切换到 `GOPATH` 目录（如，`E:\github`），执行命令 `cobra init <name> --pkg-name <pkgname>`,如下：
```
E:\github>.\bin\cobra init cobra-demo --pkg-name github.com/xcbeyond/cobra-demo
Your Cobra application is ready at
E:\github\cobra-demo
```

初始化成功后，cobra-demo程序目录结构如下：
```
cobra-demo
    | --- cmd
    |      | --- root.go
    | --- main.go
    | --- LICENSE 
```

### 运行

执行命令 `go run`运行：
```
E:\github\cobra-demo>go run main.go
A longer description that spans multiple lines and likely contains
examples and usage of using your application. For example:

Cobra is a CLI library for Go that empowers applications.
This application is a tool to generate the needed files
to quickly create a Cobra application.
```