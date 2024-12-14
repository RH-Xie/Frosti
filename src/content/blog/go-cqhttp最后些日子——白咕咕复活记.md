---
title: go-cqhttp最后些日子 ~ 白咕咕复活记
pubDate: 2023-11-11 23:40:17
tags:
  - 记录
  - go-cqhttp
  - qqbot
  - nonebot
categories:
  - tech
description: 那时候我们都相信，日子会一直这样过下去...
image: https://images.weserv.nl/?url=s2.loli.net/2023/11/12/xXmRz2WiPVN9Y4S.webp
---

> 本篇为第二稿，后续根据情况补充内容
> 

# go-cqhttp最后些日子

经常玩qq机器人的同学一定听说过go-cqhttp。

它仍是现今bot开发者最热爱的协议逆向框架，在Github上开源，与许多机器人协议相互支持。

简单理解，go-cqhttp用于收发信息，提供qq登录、设备虚拟服务。而Nonebot、Koishi.js用于对消息进行处理、定义返回信息，提供各种钩子以在合适的时间触发消息的收发。

自2019年来，go-cqhttp的诞生让聊天bot走上开源之路，社区、相关协议的生态逐渐形成，文档逐日完善，插件的开发门槛已经放低到有基础编程学习的同学都可以献一份力，鼓捣出属于自己的插件。Nonebot甚至参与了的开源之夏，供高校的同学参与开源。

那时候我们都相信，日子会一直这样过下去。

直至2022年夏左右，零星的“风控”“账号冻结”进入开发者们的视野。

2023年四月起，大规模的Code 40、Code 45和Code 235、Code 237停留在终端的最下方。多位Bot作者在此前已经领到腾讯警告、律师函，社区的脚步也逐渐放缓。

随后有大佬逆向出了设备协议，增设签名服务器，许多“贵重”的机器人得以延续。

2023年九到十月，go-cqhttp作者发布声明，建议放弃go-cqhttp，转移阵地。

而在今天的2023年十一月，经过一个月短暂倒腾后，于5月沉眠的机器人“白咕咕”重新上线。并且这次部署更为体系化，本篇也将以技术的角度解析现今可行的机器人方案。

在协议库的最后这些日子，如果想要短暂唤醒你的睡美人，请接下阅读吧。

## 白咕咕复活记

>
> 注0：先看文章顶部的更新，确认是否有必要阅读本文
> 注：本篇是可行方案复盘，并不是原理解析，我们目的只有一个：复活机器人
> 注2：不建议对内容全部招收或是深入批判，本篇文章的价值有限，并且时效性极强
> 注3：图示均出于个人理解，作者仅是一个使用者，没有参与协议框架的开发，因此图示**极有可能**出错。对于有误之处，作者愿意接受建议，并择时更改
> 注4：使用go-cqhttp的任何一个步骤都可能导致你的账号被冻结、被封禁，不要使用大号、高价值号操作

- 操作系统：缺少WSL的Windows 10 家庭版 / Ubuntu 20.04 / Docker下的Debian环境
- 软件环境：Python 3.10 slim / ZuluSDK（Java的分支）
- 部署环境：群晖NAS Synology 7.2

截止2023/11/10，QQBot最核心的部分如下图所示：

![](https://s2.loli.net/2023/11/12/HDriK1vsu5mhoyP.webp)

因此，你需要：

- 启动一个Nonebot机器人后端
  - 可以使用Matcha进行联调，这是一个测试工具，模拟go-cqhttp与nonebot通信。
- 启动一个qsign签名服务器
  - 下载unidbg-fetch-qsign，1.2.0版本，与下方的go-cqhttp版本要一致
  - 下载协议库（2023/11/10 最新为8.9.88）（一般包含在上面，但协议库可能不是最新的）
- 下载go-cqhttp（2023/11/10 1.2.0版本可用）
- 初始化一个反向socket通信的go-cqhttp
- 将unidbg-fetch-qsign/txlib/{最新版本号} 内的 `android_pad.json` 复制到go-cqhttp初始化目录下的data/version（或是versions），并且命名为`6.json` （数字是协议号，打开.json可见protocol就是6）
- 配置go-cqhttp（config.yml）
  - 填入账号密码
  - 如有协议，协议号改为6
  - 确认服务器地址可连接
  - 反向端口和nonebot一致
  - 签名服务器地址端口和qsign一致

- 启动完毕，进行登录
  - 登录会提示扫码、拉条或是手机验证，可以一一尝试。个人起初是自动提交的拉条验证，失效后手动提交，现在是手机短信验证码，而手表协议只能扫码、平板协议只能帐号登录。所以建议直接发手机验证码。
  - 登录完毕，正篇结束

而目录如下：

```
├── address.txt # 手动更改服务器地址
├── go-cqhttp # ./go-cqhttp，首次执行初始化，建议最后启动
├── bot.sh # 启动bot的命令，可以自行nb run
├── data
│   ├── versions（放置你的协议）
├── qsign.sh # 启动qsign的命令，较长，所以此处写入.sh
├── config.yml # go-cqhttp的配置文件
├── device.json # 虚拟出的设备信息
├── ptilopsis # nonebot根目录，我这里命名为ptilopsis
│   ├── README.md
│   ├── data
│   ├── .venv
│   ├── pic_search_cache
│   ├── pyproject.toml
│   └── src
├── qsign # qsign根目录
│   ├── bin
│   ├── lib
│   └── txlib
├── requirements.txt
├── session.token # go-cqhttp获取的session
```



## 面向开发

以上展示的流程适用于任何操作系统，而这里以我的环境为例子，建立一个较为可靠、易于迁移的环境。

这其中的关键当然是Docker，服务器介质则随意，支持Docker即可。

因为特化为：

- 开发环境虚拟机套Docker
- 生产环境群晖NAS Docker

自然也遇到了一些迁移的问题。

下面是一些常用操作，适用于群晖（确保群晖可以以ssh登录并且拥有root权限）

### Docker

由于是ubuntu的docker迁移到群晖的docker，不要使用群晖Docker的GUI导入导出，因为群晖Docker导出镜像格式不是`.tar`。需要ssh进入然后docker export导出为`.tar`。

#### 导出镜像

⚠ 不要使用`sudo`操作（除非权限不够），否则可能会导致无法打开、上传这个文件

```bash
docker export -o 20231111.tar 080b994a0df0
```

#### 导入镜像

```bash
sudo docker import 20231111.tar ptilopsis:20231111
```

#### 以镜像创建容器

```bash
sudo docker run -it --name=ptilopsis -w /qqbot ptilopsis:20231111 /bin/bash
```

参数：

`-it`：是`-i`和`-t`的合并缩写，效果是创建后以`bash`进入容器，`-i`使容器可交互（Keep STDIN open even if not attached），`-t`为分配“终端”（其实是`TTY`，TeleTYpewriter或者TeleTypeWriter）

`-w /qqbot`：指定工作目录，即新建终端的初始目录

`ptilopsis:20231111`：镜像ptilopsis（REPOSITORY）的20231111版本（TAG），类似的有centos:latest、python:3等等

注意：各类参数应按顺序：`docker run [带"-"的参数[=值]] {镜像名称} [启动命令]`

（更完整的：输入`docker run --help`可以得到`docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`）

#### 查看

通过`docker ps -a`查看你的容器

通过`docker image ls`查看你的镜像

![](https://s2.loli.net/2023/11/12/8g4NdtIFwb7auUB.png)



#### 复制文件

以下是主机到容器，可以反过来，源在前，目标在后。容器的格式是：`容器ID:路径`

```bash
sudo docker cp Desktop/data.zip 080b994a0df0:/qqbot
```

## 持久化

qsign时不时会崩溃，所以可以设置一下自重启。

```shell
#!/bin/bash
# 下面命令请自行替换路径
COMMAND="bash path/to/qsign/bin/unidbg-fetch-qsign --basePath=path/to/qsign/txlib/8.9.88"

while true; do
    echo "Starting the command: $COMMAND"
    $COMMAND

    # 获取命令的退出状态码
    exit_status=$?

    echo "Command exited with status $exit_status"

    # 如果退出状态码不为0，说明命令崩溃了，等待一段时间后重新启动命令
    if [ $exit_status -ne 0 ]; then
        echo "Command crashed. Restarting in 5 seconds..."
        sleep 5
    else
        echo "Command exited normally. Exiting the script."
        break
    fi
done
```

其次，整个体系也可以自动化重启：先启动nonebot、qsign和代理，定时在三分钟后启动go-cqhttp。

## 插件开发

等我PR被merge了再写

## QA常见问题

### 连不上去腾讯服务器的地址，如何获得address.txt

两个问题，前一个不由我回答。后一个问题，你可以参照下方文档，也可以使用nonebot-plugin-gocqhttp启动，随后便可以看到一个有效地址，将它带端口复制下来到go-cqhttp的根目录address.txt（没有自行创建），如有多个可以换行写。

具体见：[go-cqhttp文档：自定义服务器ip](https://docs.go-cqhttp.org/guide/config.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E6%9C%8D%E5%8A%A1%E5%99%A8ip)

### 在哪获取txlib里的文件？

https://github.com/MrXiaoM/qsign/tree/mirai/txlib/8.9.88

或者使用自行逆向
