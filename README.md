# taobao_bra_crawler
a taobao web crawler just for fun.

## 说明
淘宝文胸商品评论内容爬取与简单分析。

## 部署环境
测试环境：腾讯云主机一台<br>
操作系统：ubuntu-14.04<br>
数据库： mongodb<br>
效果展示：[http://nladuo.github.io/bra](http://nladuo.github.io/bra)

## 商品评论数据
### 下载地址
链接: [https://pan.baidu.com/s/1bpbuZLX](https://pan.baidu.com/s/1bpbuZLX) 密码: kvyp

### 导入数据
``` shell
mongoimport -d taobao -c rates  --file ./rates.dat
```

## 爬虫部署
### 修改配置文件
``` python
# -*- coding:utf-8 -*-
config = {
    'timeout' : 3,
    'db_user': '',       # 无密码
    'db_pass': '',
    'db_host': 'localhost',
    'db_port': 27017,
    'db_name': 'taobao',
    'use_tor_proxy': False,
    'tor_proxy_port': 9050
}
```
如果有被禁IP的情况可以使用tor代理，将config['use_tor_proxy']设置为True，具体方法见[python中使用tor代理](http://nladuo.github.io/2016/07/17/python%E4%B8%AD%E4%BD%BF%E7%94%A8tor%E4%BB%A3%E7%90%86/)
### 运行爬虫
``` shell
python crawler/item_crawler.py      #爬文胸的商品信息
python crawler/rate_crawler.py      #爬文胸的评论信息
python crawler/simple_analyzer.py   #统计数据
```
### 运行网页显示
``` shell
cd data_visualization
npm install
npm run dev		# 进行调试
node run build 	# 生成dist
```
