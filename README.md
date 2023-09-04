# GPT-TG
1.项目代码克隆：

git clone https://github.com/techxiaofei/bot-on-anything
cd bot-on-anything/

2.配置说明
核心配置文件为 config.json，在项目中提供了模板文件 config-template.json ，可以从模板复制生成最终生效的 config.json 文件：

cp config-template.json config.json

3.获取token

4.config配置
我已经在json文件里面删除了其他平台的配置，只保留telegram的配置即可：

{
  "model": {
    "type" : "chatgpt",
    "openai": {
      "api_key": "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",
      "model": "gpt-3.5-turbo",
      "conversation_max_tokens": 1000,
      "character_desc": "你是ChatGPT, 一个由OpenAI训练的大型语言模型, 你旨在回答并解决人们的任何问题，并且可以使用多种语言与人交流。"
    }
  },

  "channel": {
    "type": "telegram",

    "telegram": {
      "bot_token": "6274785511:AAHmverVxH9NUAexWGndPhtwjwcxxtudjPU",
      "single_chat_users": ["ALL_USERS"],
      "group_chat_list": ["ALL_GROUP"],
      "group_chat_prefix": ["@techxiaofei","@botxiaofei"],
      "group_chat_keyword": ["大神", "群主"]
    }

  }
}

4.安装依赖
升级pip包管理工具和openai

pip3 install --upgrade pip
pip3 install --upgrade openai
安装电报机器人依赖

pip install pyTelegramBotAPI
4.运行程序
配置修改完成，依赖也安装好了，我们就可以运行程序了。

在项目目录下运行 python3 app.py，终端显示如下则表示已成功运行：

[INFO][2023-02-16 01:39:53][app.py:12] - [INIT] load config: ...
[INFO][2023-02-16 01:39:53][wechat_mp_channel.py:25] - [WX_Public] Wechat Public account service start!
Bottle v0.12.23 server starting up (using AutoServer())...
Listening on http://0.0.0.0:80/
Hit Ctrl-C to quit.

最后一步
之前我们python3 app.py只有在你开启窗口的时候才会运行，关闭窗口之后就会停掉。我们需要程序在后台自动运行，这样即使我们关掉云服务器窗口也能继续运行。

那么我们需要开启后台运行的命令：

touch nohup.out
nohup python3 app.py & tail -f nohup.out
此时可通过 ctrl+c 关闭日志，不会影响后台程序的运行。使用 ps -ef | grep app.py | grep -v grep 命令可查看运行于后台的进程，如果想要重新启动程序可以先 kill 掉对应的进程。日志关闭后如果想要再次打开只需输入 tail -f nohup.out。

如何杀进程
第一行先查出来PID，然后第二行kill你查到的PID就可以。

每次重启之前先kill掉进程

ps -ef | grep app.py | grep -v grep
kill -9 PID
