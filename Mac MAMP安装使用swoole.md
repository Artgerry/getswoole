# Mac MAMP安装使用swoole
系统版本10.14.3 
Swoole：面向生产环境的 PHP 异步网络通信引擎
- - - -


## 安装步骤：
在使用EasySwoole之前我们要安装Swoole，Swoole是PHP扩展，我们可以通过
`pecl install swoole`
如果系统提示不存在pecl这个命令 
`-bash:pecl: command not found`

1. 安装pecl 
 `curl -O https://pear.php.net/go-pear.phar`
若是提示权限不足，使用`sudo`，安装成功可查看版本：`pear version`

再次通过 `pecl install swoole` 
提示`fatal error: ‘php.h’ file not found`
![](Mac%20MAMP%E5%AE%89%E8%A3%85%E4%BD%BF%E7%94%A8swoole/C9526D1E-E68F-47E7-8303-3A7979A26A33.png)

2. 建立软连接
解决办法是：`sudo ln -s /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.10.sdk/usr/include /usr/include`
**注意MacOSX10.10.sdk修改为自己系统的版本号**

但是又会提示：`/usr/include Operation not permitted`
**要关闭它必须进入recover 模式（重启之后按住command+r），在工具中找到terminal执行csrutil disable命令，回车，然后重启，SIP保护就被关闭了。如果要重新打开SIP保护，操作是一样的，命令中的disable换成enable就可以了**
才是网上得知：mac反对usr_include与sdk不同，编译器已经知道如何在SDK中找到它们的include，所以不再需要_usr/include目录。可以找到SDK的包含文件的安装目录通过命令，

3. 对_usr_include/的处理
所以直接使用命令：
`sudo installer -pkg /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg -target /`
就出现了_usr_include/

再把php.h文件copy到这个目录里面：
`sudo cp /Applications/MAMP/bin/php/php7.1.1/include/php/main/php.h /usr/include/`

4. 安装pcre
再次通过 `pecl install swoole` 提示 pcre不存在，直接用：`brew install pcre`

5. 成功安装swoole
最后  `pecl install swoole` 成功安装swoole，呃呃呃 安装成功的忘记截图了。

