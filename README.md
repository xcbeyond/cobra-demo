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

## 实战

这里以一个简单的 `time` 命令为例，实战讲解如何cobra开发一个命令。
功能如下：
* `show`：查看当前时间
* `parse`：指定时间格式 --format，parse为show的子命令

### 实现show命令

1. 添加show命令
通过命令 `cobra add`添加show命令：
```
E:\github\cobra-demo>..\bin\cobra.exe add show
show created at E:\github\cobra-demo
```

此时，项目cmd目录下会创建一个 `show.go` 文件，在该文件中可完成命令的具体操作逻辑。

下面是 `show.go` 文件的初始代码：
```go
// showCmd represents the show command
var showCmd = &cobra.Command{
	Use:   "show",
	Short: "A brief description of your command",
	Long: `A longer description that spans multiple lines and likely contains examples
and usage of using your command. For example:

Cobra is a CLI library for Go that empowers applications.
This application is a tool to generate the needed files
to quickly create a Cobra application.`,
	Run: func(cmd *cobra.Command, args []string) {
		fmt.Println("show called")
	},
}

func init() {
	rootCmd.AddCommand(showCmd)

	// Here you will define your flags and configuration settings.

	// Cobra supports Persistent Flags which will work for this command
	// and all subcommands, e.g.:
	// showCmd.PersistentFlags().String("foo", "", "A help for foo")

	// Cobra supports local flags which will only run when this command
	// is called directly, e.g.:
	// showCmd.Flags().BoolP("toggle", "t", false, "Help message for toggle")
}
```

2. 实现显示当前时间逻辑
在&cobra.Command.Run中添加获取当前时间逻辑 `time.Now()`：
```go
var showCmd = &cobra.Command{
	Use:   "show",
	Short: "A brief description of your command",
	Long: `A longer description that spans multiple lines and likely contains examples
and usage of using your command. For example:

Cobra is a CLI library for Go that empowers applications.
This application is a tool to generate the needed files
to quickly create a Cobra application.`,
	Run: func(cmd *cobra.Command, args []string) {
		// show current time
		fmt.Println(time.Now())
	},
}
```

3. 修改help命令
help命令有两个，一个是short，一个是lang，很明显short命令用来定义简短的说明，lang命令用来定义详细说明，下面我们修改show命令的help:
```go
var showCmd = &cobra.Command{
	Use:   "show",
	Short: "Displays the current time",
	Long: `You can use the time show command to view the current time. For example:

$ ./cobra-demo show
2021-03-19 14:34:20.9320241 +0800 CST m=+0.378845301`,
	Run: func(cmd *cobra.Command, args []string) {
		// show current time
		fmt.Println(time.Now())
	},
}
```

4. 运行
执行show命令：
```
E:\github\cobra-demo>go run main.go show
2021-03-19 14:49:27.3582836 +0800 CST m=+0.176660901
```

执行show --help命令：
```
E:\github\cobra-demo>go run main.go show --help
You can use the time show command to view the current time. For example:

$ ./cobra-demo show
2021-03-19 14:34:20.9320241 +0800 CST m=+0.378845301

Usage:
  cobra-demo show [flags]

Flags:
  -h, --help   help for show

Global Flags:
      --config string   config file (default is $HOME/.cobra-demo.yaml)
```

