---
nav:
  title: 工具
  path: /tool-nav
---

## tool-view

Demo:

```tsx
import React from 'react';
import { Foo } from 'dumi-template';

export default () => <Foo title="tool-view" />;
```

## Change

Demo:

```tsx
import React from 'react';
import { Foo } from 'dumi-template';

export default () => <Foo title="Change" />;
```

## gitHub

### 访问页面超时的问题

[参考](https://blog.csdn.net/oyjl__/article/details/132262919)

### 提交的失败时的端口问题

mac 上使用 git push 命令或者 sourceTree 操作时一直无响应，最后如下错误提示

```sh
ssh: connect to host github.com port 22: Operation timed out
fatal: Could not read from remote repository.

ssh: connect to host github.com port 22: Operation timed out
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

这个错误表明 SSH 连接在尝试通过 22 端口连接到远程服务器时超时。这可能是由于网络环境、防火墙设置或代理配置等原因导致的。为了解决此问题，我们可以尝试将 SSH 连接切换到 443 端口

```sh
cd ~/.ssh
nano config
```

复制以下内容：

```sh
Host github.com
  User 注册github的邮箱
  Hostname ssh.github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa
  Port 443
```

使用 nano 编辑器，按下 Ctrl + X，然后按 Y 确认保存，最后按 Enter 退出。
重新测试，发现可以运行

```sh
ssh -T git@github.com

Hi mywywuqek060! You've successfully authenticated, but GitHub does not provide shell access.
```

重新提交代码，成功

## NVM

### 前提

**如果你的电脑已经安装了 node，那么在安装 nvm 之前要先卸载掉，避免后面产生不必要的冲突**

Window 控制面板程序卸载或者用其他的应用卸载都行
Mac 卸载：

```sh
# 删除全局 node_modules 目录
sudo rm -rf /usr/local/lib/node_modules
# 删除 node
sudo rm /usr/local/bin/node
# 删除全局 node 模块注册的软链
cd /usr/local/bin && ls -l | grep "../lib/node_modules/" | awk '{print $9}'| xargs rm
```

### 安装

#### Mac 安装

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
```

或者

```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
```

#### Windows 安装

[下载地址](https://github.com/coreybutler/nvm-windows/releases)

### 命令

```sh
nvm install <版本号>   // 安装指定 node 版本，版本号如写 14.5.0 或 v14.5.0 效果一样
nvm uninstall <版本号> // 卸载指定 node 版本
nvm install stable    // 安装最新稳定版 node
nvm ls                // 查看已经安装了的所有 node 版本
nvm on                // 开启使用 nvm 管理 node
nvm use <版本号>      // 切换到指定 node 版本，当前窗口生效
nvm alias default <版本号> // 全局默认版本。如果 nvm use xxx 换不了，就用这个换
nvm off               // 关闭 nvm 管理 node
```

### 其他

**安装淘宝镜像设置**

```sh
# npm 用淘宝镜像
npm config set registry http://registry.npm.taobao.org/
# 或安装 cnpm
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm config  set registry https://registry.npm.taobao.org
cnpm config get registry
cnpm -v
```

[更多注意事项](https://juejin.cn/post/7165500644647206948?searchId=202401161111490C24995F8F6D546EAE2D)

[更多技巧](https://d.umijs.org/guide/demo-principle)
