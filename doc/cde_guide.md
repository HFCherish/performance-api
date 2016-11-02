### 准备cde环境
1. 下载安装[docker](https://www.docker.com/products/docker#mac)
1. 下载最新版本(0.1.5) [cde](https://github.com/tw-cde/cde-client-binary/releases)
2. 将下载下来的可执行文件（eg. cde\_darwin\_amd64）重命名为cde，并移动到/usr/local/bin
3. 运行docker，打开terminal，输入`cde -h`，出现cde帮助信息，安装成功。

### 使用cde
1. 帮助命令：`cde [command] -h`
1. 注册：打开terminal，输入`cde register http://controller.tw-cde.com `。按提示要求输入个人邮箱帐号，回车即注册成功。
2. 显示所有技术栈：`cde stacks`
3. 创建一个新的程序：terminal中进入项目目录，输入`cde apps:create <projectName> jersey-mysql-redis`在cde中创建一个新程序。其中`jersey-mysql-redis`是技术栈，sanxing采用的是该技术栈，所以这里写的是这个。
4. 添加git remote：`cde git:remote <projectname> [-r <remoteName>]`，remoteName默认是cde
4. 起环境：`cde dev:up`。这根据项目的配置文件要求，搭建起所要求的环境，例如mysql。后续测试运行时，要保证环境起起来了。（初次起环境可能比较慢）
5. 测试：环境起起来之后，当前目录是`/usr/local # `，进入`/codebase`执行测试`gradle clean test`。也可以在本地IDE环境中跑测试
6. 编写代码并提交：本地IDE编写代码，进入代码目录，用git命令add、commit，并提交`git push <remoteName> master`。（cde使用git管理代码）
7. 本地运行：代码提交后就已经自动部署，进入`/codebase`，输入`gradle run`，起来之后，即可在浏览器中通过`localhost:8088`访问后端。（初次起服务器可能比较慢）

### 其他命令
1. cde set环境变量的方法：cde config:set ORIGINS=http://pre-lead-feedback.herokuapp.com
2. 创建新的域名（即为访问你的应用程序自定义一个域名）：cde domains:create sanxing-api.tw-cde.com
3. 设置路由（在创建域名之后，设置该域名的根访问路径）：cde routes:create sanxing-api.tw-cde.com /
4. 绑定路由（在设置路由之后，将该路由于应用程序绑定起来）：cde routes:bind sanxing-api.tw-cde.com/ san-xing

### 其他
1. 添加认证. 往cde中push或pull等时,可能提示没有权限. 需要加ssh认证，方法是：eval \`ssh-agent -s\`（用于添加身份认证），然后执行`ssh-add ~/.ssh/***`, ***是本地密钥