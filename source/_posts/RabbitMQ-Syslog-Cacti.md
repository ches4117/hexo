---
title: RabbitMQ-Syslog-Cacti
date: 2020-06-23 20:51:47
tags: RabbitMQ
---
  有個需求是將外面設備的 syslog 經由 RabbitMQ，傳送到另外一台伺服器上，透過 Cacti syslog 的插件查看狀況。
<!--more-->

## 難題
  1. 如何操作 RabbitMQ 收送訊息
  2. 如何用 Python 傳送 syslog 
  3. 如何轉換 syslog 時區與格式

## 解決
  用了兩天的時間看了 Python syslog 以及 RabbitMQ。
  
  一開始先下載 RabbitMQ docker container，並找了一個 RabbmitMQ 簡單的收發訊息的程式測試成功。（難題一)<br/><br/>

  接下來花蠻多時間在研究 Python syslog，我這階段也是找了一個範例程式研究。
  ```
  handler = logging.handlers.SysLogHandler(address=('127.0.0.1', 514), facility='local1')
  ```
  上面這段程式就是設置要傳送到本機端的 514 port，以及隨意設定的 facility。
  然後還有其他基本設定就不贅述，設定成功後就能在 Cacti 上看到所傳送的訊息了(難題二)<br/><br/>

  但是發現 Cacti 上的 log 時間格式錯誤，
  於是我就參考[該連結](https://stackoverflow.com/questions/32402502/how-to-change-the-time-zone-in-python-logging)，
  ```
  class Formatter(logging.Formatter):
    """override logging.Formatter to use an aware datetime object"""

    def converter(self, timestamp):
        dt = datetime.datetime.fromtimestamp(timestamp)
        tzinfo = pytz.timezone('Asia/Taipei')
        return tzinfo.localize(dt)

    def formatTime(self, record, datefmt=None):
        dt = self.converter(record.created)
        if datefmt:
            s = dt.strftime(datefmt)
        else:
            try:
                s = dt.isoformat(timespec='milliseconds')
            except TypeError:
                s = dt.isoformat()
        return s
  ```
  成功設置好時區就可以了。(難題三)

