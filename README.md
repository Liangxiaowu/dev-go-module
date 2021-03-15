### Go 发布Go Module 依赖管理 (同步到github)

从Go1.11开始加入了对Go Module的支持，Go1.13开始Go Module成为了Go默认切推荐的包依赖管理方式。至今已有非常多的开源项目包支持Go Module，对Go Module感兴趣的可以移步到:https://golang.google.cn/ref/mod

#### 创建项目

先在[github](https://github.com/)创建一个项目，然后将项目拉到本地。

```git
git clone git@github.com:Liangxiaowu/dev-go-module.git

cd ./dev-go-module
```

#### 环境变量和代理

在初始化项目之前，需要设置一下环境变量和下载代理。

GO111MODULE环境变量有三个状态值:`off`(不支持module), `on`(支持module) 和 `auto`(当目录有`go.md`文件会支持module)。

我们需要设置`GO111MODULE=no`

```linux
set `GO111MODULE=no`
```

设置国内下载代理

```linux
linux:
	export GOPROXY=https://goproxy.cn

win:
	set GOPROXY=https://goproxy.cn
```

设置完成后可运行`go env`查看。

#### 初始化项目

需要运行`go mod init`命令来初始化项目

```go
go mod init dev-go-module
go: creating new go.mod: module dev-go-module // 成功后的结果
```

成功后目录下面会出现`go.mod`文件

#### 编写运行脚本

直接上代码

```go
hello.go

package pkg

import "fmt"

func World()  {
	fmt.Println("Hello world !!!")
}
```

#### 提交代码

提交代码到github，然后打包`tag`标签。

```git
git  tag -a v1.0.0 -m "hello world"
git push origin v1.0.0
```

#### 拉取模块包

```go
go get -u github.com/Liangxiaowu/dev-go-module

go: github.com/Liangxiaowu/dev-go-module upgrade => v1.0.0 // 结果
```

#### 使用包函数

```go
import (
	_ "github.com/Liangxiaowu/dev-go-module"
)

func mod() {
	World()
}

```

