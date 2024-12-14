---
title: 基于 Chronocat + liteloader 的 RedProtocal 迁移
pubDate: 2024-1-21
tags:
  - 记录
  - qqbot
categories:
  - tech
description: Happy to see you again
slug: chronocat-redprotocal
image: https://images.weserv.nl/?url=s2.loli.net/2024/02/15/Byul1j9FKXCNJob.webp
---

%%

url%3Dhttps%3A%2F%2Fmusic.163.com%2Fsong%2Fmedia%2Fouter%2Furl%3Fid%3D2083848734.mp3%26name%3D%E6%88%91%E6%83%B3%E4%BD%A0%E4%BA%86%EF%BC%8C%E7%89%A2%E5%92%95%26artist%3D%E4%BC%A0%E5%A5%87AI%E7%99%BD%E5%92%95%E5%92%95%26cover%3Dhttps%3A%2F%2Fs2.loli.net%2F2024%2F02%2F15%2FCqeM1GuH9rc4sK3.webp%26theme%3D%2352B4EC

%%

## 是的，孩子们，我回来了

自上篇写完后，我又找了其他方案，然后试了下Chronocat + Liteloader，折腾成功了，但是要做代码修改。

如何迁移到上述框架看这篇：[目前可用的QQ机器人hook框架-Chronocat教程](https://blog.bingyue.top/page/2/#board)

当你成功启动Bot，然后把onebot那边的插件拉过来用时，就会发现**发不出消息**，细看则是**规则匹配上了但send后无反应**。

本篇针对上述问题示例如何做代码修改，以适配从onebot v11迁移到RedProtocol。

> 笔者对源码并不熟悉，囫囵吞枣之处，恳请指教

> helper：如果你未成功启动Bot，报错在.env配置文件里，请尝试去掉#注释（特指JSON里的，如果不知道建议了解下[JSON长什么样]()，.env其他地方用#是没问题的），查看报错最后的行数（如lineno 284）是否变化。如果变化，说明配置文件里的#注释没有被正确解析，去掉所有#则可正常启动



## 哪些插件需要迁移

没有做协议适配或没有使用的协议适配插件（如saa）编写的插件。症状是不报错，代码走下去了，但是**消息发了没反应**。

换言之，如果插件一装上去就报错，或者发送前就已经出现了报错，**首要考虑的就不是迁移**，而是先把这些报错解决。

## 迁移点

### adapter

找到需要发送消息的代码，如`bot.send`、`message.finish`这些方法，观察上面是否有引入`nonebot.adapters.onebot.v11`，有则换成形如以下：

```python
from nonebot.adapters.red.bot import Bot
from nonebot.adapters.red import MessageSegment
from nonebot.adapters.red.event import Event
```

### 换方法、换类

`nonebot.adapters.onebot.v11`后导入的方法、类，统一换成red下的，确认请Ctrl点击` nonebot.adapters.red`查看，比对名称语义。

### 去除CQ码

RedProtocol不支持CQ码，需要去掉。当然，这意味着Bot不能@人了，但显然不应该因为CQ码影响了咱Bot的主要功能。

### 处理图片数据

> [red只能用本地文件路径或者二进制数据发图片 你应该先拉取url的数据，再用image(data)发送](https://github.com/nonebot/adapter-red/issues/33#issuecomment-1807102175)

#### API返回URL需多请求一次

因为RedProtocol不像go-cqhttp会自动请求https://开头的图片url，你需要自行对url请求，拿回图片数据，再做发送.

```python
async def suijitu():
    async with AsyncClient() as client:
        url = "https://api.2xb.cn/zaob"  # 备用网址
        resp = requests.get(url)
        resp = resp.text
        resp = remove_upprintable_chars(resp)
        retdata = json.loads(resp)
        imageUrl = retdata['imageUrl']
        img = await client.get(imageUrl, timeout=8000)
        return [MessageSegment.text(f"今日60S读世界已送达\n"), MessageSegment.image(img.content)]
```

#### 图片格式

本地上传给TX的OSS图片如果是webp的，可能获取不到宽高，导致下载到”损坏图像“，因为OSS返回的还是一个JSON，里面带了width、height这些数据，在你下载图片到缓存时，要么中途报错，要么图片格式有问题发不出去。

#### 转二进制

支持发二进制数据

```python
...
	buf = BytesIO()
    img.save(buf, format='png') # buf存为png编码
    return True, MessageSegment.image(buf.getvalue()), msg # 获取二进制数据
...
```

#### 图片路径

[gocq迁移过来需多包一层pathlib.Path](https://github.com/nonebot/adapter-red/issues/16#issuecomment-1754629097)

