---
title: Go入门 
tags: Go
grammar_cjkRuby: true
---

# 安装
- 去官网下载安装包，按照步骤进行安装
- 配置GOPATH环境变量，这将是你以后的工作目录
- 在GOPATH创建三个文件夹：bin、pkg和src，其中bin是编译之后的可执行文件存放目录，pkg为库文件编译之后的存放目录，src为所有的源代码。
- 配置GOBIN环境变量，为了之后运行编译结果更方便，可以把$GOPATH/bin加入到环境变量path中
- 在src下建立自己的命名空间，例如github.com/username
- 接下来，自己的包都会放在此命名空间内，例如在github.com/username 下建立文件夹：Hello，并在Hello文件夹创建Hello.go

# Hello World
按照安装的教程，我们已经配置好了go的开发环境，接下来就是进行简单的go语法学习
编辑自己的Hello.go文件，输入测试代码：
```golang
package main

import (
	"fmt"
	"github.com/JeffreyWxj/my_utils"
)

func main() {
	fmt.Println("HHH");
	my_utils.Print_abc();
}
```
以上代码还包含了其他package的引入方法，此处不再赘述