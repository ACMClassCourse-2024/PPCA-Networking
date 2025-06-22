# 环境配置

## 使用语言

- 除C/C++以外的任何语言
- 不建议使用python与java，因为这两门语言在之后的课程中都会被使用
- PPCA课程希望大家可以学习一门崭新的语言
- 如果你使用了助教不会的语言助教会去学习



## Go 语言配置教程

### IDE

- Goland：Jetbrains家族对于Go语言专门开发的IDE，方便快捷，且学校有对应正版授权，即下即用。
- vscode：需要安装对应扩展与相关组件，配置需要一定时间，但对许多人来说vscode使用起来更熟悉，且以后在写其他文件时，也大多会使用vscode。

### windows

- [官方网站](https://golang.google.cn/)

- [官方安装教程（简略）](https://golang.google.cn/doc/install)

- windows下环境配置较为简单

- 大体流程是你需要在msi文件安装完成后手动添加环境路径，添加完成后在powershell中键入

  ```bash
  go version
  ```

  即可进行测试。

- 也可以使用[scoop](https://scoop.sh/)等包管理器进行安装。

- 具体环境配置流程可以去相关博客或网站搜索`Go install windows`。

### Linux

#### 一

如果你是ubuntu用户，请输入

```bash
sudo apt install golang-go
```

以安装go。并在安装完成后使用

``` bash
go version
```

检查是否安装成功

注意，此指令在ubuntu-24.04下默认安装1.22.2版本，但在ubuntu-22.04下默认安装1.18.1版本。如果你想使用更新版本的语言，请参照 golang 官网教程手动安装。

#### 二

如果你是arch系用户

```
yay -S go
```

#### 三

如果前两者你都不愿意执行或都没效果

删除旧版本 Go：

```bash
sudo rm -rf /usr/local/go
```

下载 Go 安装包：（你可以从 [Go 官网](https://go.dev/dl/) 获取最新版本下载链接）

```bash
curl -LO "https://go.dev/dl/go1.20.5.linux-amd64.tar.gz"
```

解压到 `/usr/local` 目录：

```bash
sudo tar -C /usr/local -xzf go1.20.5.linux-amd64.tar.gz
```

将 `/usr/local/go/bin` 目录添加到 PATH 环境变量中。

如果你使用的是 zsh，执行以下命令：

```bash
echo 'export PATH="$PATH:/usr/local/go/bin"' >> ~/.zshrc
```

如果你使用的是 bash，执行以下命令：

```bash
echo 'export PATH="$PATH:/usr/local/go/bin"' >> ~/.bashrc
```

重启终端使环境变量生效。

之后运行以下命令检查 Go 版本：

```bash
go version
```

配置 [Go 模块代理](https://goproxy.cn/) 加速 Go 模块的下载：

```bash
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
```

## 网络环境搭建

我们建议用 `lxd` 创建两个 `lxc` 容器，分别作为客户端和服务器端。调整配置使两个容器在同一虚拟内网中具有固定的 IP 地址。
如果你不想使用 `lxd`，也可以使用 `docker`、虚拟机或物理机。

[lxd官方教程](https://documentation.ubuntu.com/lxd/stable-5.21/tutorial/first_steps/)

### 快速开始

```bash
sudo snap install lxd
sudo lxd init --minimal
sudo lxc launch ubuntu:24.04 my-container
sudo lxc list
sudo lxc info my-container
sudo lxc exec my-container -- bash
```