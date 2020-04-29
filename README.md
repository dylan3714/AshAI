# AshAI_Toy
该项目旨在设计一款借助于 Flask + 人工智能实现的语音互动亲子玩具, 
面向 3-5 岁幼年儿童, 在为幼年儿童提供优质音频内容的基础上构建幼儿社交圈, 
通过音频交友, 进行交流分享与学习. 同时支持 APP 远程内容管理, 消息推送, 内容推送, 
好友管理等基本功能

### 下载安装

- 下载源码:

```
https://github.com/dylan3714/AshAI.git
```

- 安装依赖

```
pip install -r requirements.txt
```

- 软件依赖
  - MongoDB
  - Redis
  - HBuildxerX
  - FFmpeg

- 配置:

```
# config.py 为项目配置文件
# 配置 DB
DB = client_mongodb["AiToy"]
RDB = Redis("127.0.0.1", 6379, db=4)

# url 路径配置(资源爬取)
URL = "https://www.ximalaya.com/revision/play/album?albumId=245037&pageNum=1&sort=1&pageSize=30"

# Begin --> 目录配置
COVER_PATH = "Cover"
MUSIC_PATH = "Music"
QRCODE_PATH = "Qrcode"
RECOFILE_PATH = "RecoFile"
# <-- End

# 联图二维码接口API(将 %s 内容生成二维码图片, 返回数据流)
LT_URL = "http://qr.topscan.com/api.php?text=%s"

# 需填入百度AI个人项目的相关信息
APP_ID = ""
API_KEY = ""
SECRET_KEY = ""

# 需填入图灵机器人TL_API_KEY
TL_API_KEY = ""

# get_source.py
start_mongodb_cmd 命令需要修改, 开启 MongoDB, 若 MongoDB 处于开启状态可注释该行

# gen_nlp.py
start_mongodb_cmd 命令需要修改, 开启 MongoDB, 若 MongoDB 处于开启状态可注释该行

# create_qrcode.py
start_mongodb_cmd 命令需要修改, 开启 MongoDB, 若 MongoDB 处于开启状态可注释该行


```

- 启动

```
# 如果你的依赖已经安装完成并且具备运行条件
1.启动 MongoDB, Redis
2.PyCharm 打开项目目录
3.运行 utils 目录下的 get_source.py 获取音频资源并将信息入库
4.运行 utils 目录下的 create_qrcode.py 生成二维码并将信息入库
5.运行 app.py 启动 APP 后台服务器
6.运行 ws_app.py 启动模拟硬件后台服务器
7.HBuilderX 结合模拟器或真机即可测试所有功能
```

### 项目应用技术以及技术实现功能

- Flask (项目框架)
  - 登录注册相关
    - reg  注册
    - login  登录
    - auto_log  自动登录
  - 内容相关
    - content_list  获取内容信息
    - get_cover  获取封面
    - get_music  获取资源
  - 语音消息及音频上传相关
    - app_uploader  App 向 Toy 发送语音消息
    - toy_uploader  Toy 向 App 发送语音消息
    - ai_uploader  Toy 向 AI 发送语音指令
  - 硬件设备及二维码相关
    - scan_qr  扫描二维码
    - bind_toy  绑定玩具
    - toy_list  展示玩具列表
    - get_qr  获取二维码图片
  - 好友通讯录相关
    - friend_list  好友列表展示
    - add_req  处理好友添加请求
    - req_list  展示好友请求列表
    - acc_req  同意好友请求
    - ref_req  拒绝好友请求
- WebSocket
  - APP 通讯
  - Toy 通讯
- NLP
  - 语音内容 (转文字) 相似度匹配

### 功能简述

- app
  - 推送语音消息给 Toy
  - 推送音乐等语音内容给 Toy
  - 与 Toy 进行相互之间的语音交流
  - 管理好友
  - 管理 Toy
- toy
  - 主动请求音乐等语音内容
  - 与 APP 进行相互之间的语音交流
  - 与 AI 进行交互
  - Toy 之间进行相互之间的语音交流
