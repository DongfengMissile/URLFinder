# URLFinder
URLFinder是一款用于快速提取检测页面中JS与URL的工具  

通常用于快速查找隐藏在页面或js中的敏感或未授权api接口  

功能类似于JSFinder，开发由来就是使用它的时候经常返回空或链接不全，作者还不更新修bug，那就自己来咯  

URLFinder更专注于提取页面中的JS与URL链接，提取的数据更完善且可查看状态码与内容大小  

基于golang的多线程特性，几千个链接也能几秒内出状态检测结果

有什么需求或bug欢迎各位师傅提交lssues  

## 功能说明
1.提取页面的URL链接（页面URL最多深入一层，防止抓偏）  
2.提取页面的JS链接  
3.提取JS中的URL链接  
4.提取到的链接会显示状态码、响应大小、标题（带cookie操作时，可能会触发一些敏感功能，后台慎用）  
5.支持配置Headers请求头  
6.支持提取批量URL  
7.支持结果导出到csv文件


结果会优先显示输入的url顶级域名，其他域名不做区分显示在 other  
结果会优先显示200，按从小到大排序（输入的域名最优先，就算是404也会排序在其他子域名的200前面）

## 使用截图
单url截图  
[![jagnp9.png](https://s1.ax1x.com/2022/08/19/vr0G1P.png)](https://s1.ax1x.com/2022/08/19/vr0G1P.png)  
批量url截图  
[![vRqHrd.png](https://s1.ax1x.com/2022/08/27/vRqHrd.png)](https://s1.ax1x.com/2022/08/27/vRqHrd.png)  
[![vRqbqA.png](https://s1.ax1x.com/2022/08/27/vRqbqA.png)](https://s1.ax1x.com/2022/08/27/vRqbqA.png)  

## 使用教程
单url时使用  
```
URLFinder.exe -u http://www.baidu.com -s all -m 2

URLFinder.exe -u http://www.baidu.com -s 200,403 -m 2
```
批量url时使用  
```
URLFinder.exe -s all -m 2 -f url.txt -o d:/
```
参数：  
```
-h  帮助信息
-u  目标URL  
-a  自定义user-agent请求头  
-s  显示指定状态码，all为显示全部  
-m  模式：  1  正常抓取（默认），  2  深入抓取  
-c  添加cookie  
-i  加载yaml配置文件（不存在时，会在当前目录创建一个默认yaml配置文件）  
-f  批量url抓取，需指定url文本路径  
-o  结果导出到csv文件，需指定导出文件目录（.代表当前目录）
```
##  编译  
以下是在windows环境下，编译出各平台可执行文件的命令  

```
windows
#64位
SET CGO_ENABLED=0
SET GOOS=windows
SET GOARCH=amd64
go build -ldflags "-s -w" -o URLFinder-windows64.exe main.go

#32位
SET CGO_ENABLED=0
SET GOOS=windows
SET GOARCH=386
go build -ldflags "-s -w"  -o URLFinder-windows32.exe main.go

linux
#64位
SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=amd64
go build -ldflags "-s -w" -o URLFinder-linux64 main.go

#32位
SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=386
go build -ldflags "-s -w" -o URLFinder-linux32 main.go

macos
#64位
SET CGO_ENABLED=0
SET GOOS=darwin
SET GOARCH=amd64
go build -ldflags "-s -w" -o URLFinder-macos64 main.go

#32位
SET CGO_ENABLED=0
SET GOOS=darwin
SET GOARCH=386
go build -ldflags "-s -w" -o URLFinder-macos32 main.go
```
## 更新说明  
2022/9/5  
新增 链接存在标题时，显示标题  
新增 -i 参数，加载yaml配置文件（目前只支持配置请求头headers）  
修改 部分代码逻辑  
修复 当ip存在端口时，导出会去除端口
 

2022/8/29  
新增抓取url数量显示  
优化 部分代码  
新增 提供各平台可执行文件

2022/8/27   
新增 -o 改为自定义文件目录  
新增 导出文件改为csv后缀，表格查看更方便  
修复 已知正则bug


2022/8/19  
优化 加长超时时间避免误判    

2022/8/5  
新增 状态码过滤  
新增 状态码验证显示进度  
修复 域名带端口输出本地错误问题  

2022/7/25   
优化 js规则  
优化 排序  
新增 根据状态码显示彩色字体  

2022/7/6   
完善 规则  

2022/6/27   
优化 规则  
新增 提供linux成品程序  

2022/6/21   
修改 获取状态码从自动改为手动（-s）  
新增 显示响应内容大小  

2022/6/16   
优化 提取规则增强兼容性  
修复 数组越界错误处理  

2022/6/14  
修复 部分网站返回空值的问题  

2022/6/13  
新增 自定义user-agent请求头功能  
新增 批量url抓取功能  
新增 结果导出功能  
优化 过滤规则  
优化 结果排版  

2022/6/8  
修复 忽略ssl证书错误  

