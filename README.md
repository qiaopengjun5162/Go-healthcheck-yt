# Go-healthcheck-yt

## Explain main.go code

这段代码是一个用于检查网站是否运行或宕机的小工具。代码的主要功能是使用命令行参数来指定要检查的域名和端口号，然后调用Check函数来检查指定的域名和端口的状态，并将结果打印出来。

具体代码步骤如下：

1. 导入必要的包：main包导入了"fmt"、"log"、"os"和"github.com/urfave/cli/v2"这些包。
2. 定义main函数：main函数是程序的入口函数。
3. 创建一个cli.App实例：创建一个名为"Healthchecker"的cli.App实例，并设置其用途为"检查网站是否运行或宕机的小工具"。
4. 定义命令行参数：定义了两个命令行参数，一个是"domain"，用于指定要检查的域名；另一个是"port"，用于指定要检查的端口号。其中"port"参数是可选的，默认值为"80"。
5. 定义Action函数：定义了一个匿名函数作为Action函数，该函数会在命令行参数解析完毕后被调用。该函数会获取"port"参数的值，并根据需要设置默认值。然后调用Check函数来检查指定的域名和端口的状态，并将结果打印出来。
6. 运行应用程序：调用app.Run()方法来运行应用程序，并传入命令行参数os.Args。如果运行过程中出现错误，则使用log.Fatal()方法打印错误信息并退出程序。

总结：这段代码是一个使用命令行参数来检查网站状态的小工具。它通过解析命令行参数来获取要检查的域名和端口号，并调用Check函数来检查指定的域名和端口的状态。最后，将结果打印出来。

## Explain check.go code

这段代码是一个用于检查网络连接状态的函数。它接收两个参数：目标地址(destination)和端口(port)。函数首先将目标地址和端口拼接成一个完整的地址字符串，然后设置一个超时时间为5秒。接下来，使用net包中的DialTimeout函数创建一个TCP连接，并指定连接的地址和超时时间。如果连接成功建立，则返回一个表示连接状态的字符串，包括目标地址、本地地址和远程地址。如果连接失败，则返回一个表示连接不可达的字符串，包括目标地址和错误信息。

具体步骤如下：

1. 导入必要的包：main、fmt、net和time。
2. 定义一个名为Check的函数，接收两个参数：目标地址和端口。
3. 将目标地址和端口拼接成一个完整的地址字符串，并赋值给变量address。
4. 设置一个超时时间为5秒，并赋值给变量timeout。
5. 使用net包中的DialTimeout函数，传入参数"tcp"、address和timeout，创建一个TCP连接，并将连接和错误信息赋值给变量conn和err。
6. 定义一个空字符串变量status。
7. 如果err不为空，则表示连接失败，将连接不可达的字符串赋值给status，包括目标地址和错误信息。
8. 否则，表示连接成功建立，将连接可达的字符串赋值给status，包括目标地址、本地地址和远程地址。
9. 返回status。

## Usage

```shell
Code/go/go-healthcheck-yt via 🐹 v1.20.7 via 🅒 base 
➜ go run . --domain pexels.com
[UP] pexels.com is reachable, 
 From: 192.168.0.102:56033
 To: 104.16.234.10:80

Code/go/go-healthcheck-yt via 🐹 v1.20.7 via 🅒 base took 2.7s 
➜ go run . --domain google.com
[DOWN] google.com is unreachable, 
 Error: dial tcp 59.24.3.174:80: i/o timeout

Code/go/go-healthcheck-yt via 🐹 v1.20.7 via 🅒 base took 5.4s 
➜ go run . --domain baidu.com 
[UP] baidu.com is reachable, 
 From: 192.168.0.102:56105
 To: 39.156.66.10:80
```
