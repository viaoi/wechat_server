This code is no longer being maintained.

开源的目的更多是给新手一个参考 Demo

# gxgk-wechat-server
客户服务公众号后端，为在用户提供一系列信息查询与售后服务。


**主要功能**：

- [x] 产品购买记录查询
    - [x] 手动查询
    - [x] 微信分享购买记录
- [x] 提交售后
    - [x] 保修查询
    - [x] 提交售后
- [x] 产品使用技巧
    - [x] 新奇方案
    - [x] 新品推荐

**其他**：

- [x] 电池电量提醒
- [x] 合作信息

补充说明：

- 依赖外部 API 的操作使用客服接口异步回复，需要通过微信认证
- 字典、正则匹配关键词，避免过多的条件语句嵌套
- 场景状态，支持上下文回复
- 全局保存、刷新微信 access_token
- 关键词兼容繁体、全角空格
- 长文本的回复使用图文信息进行排版
- 前端 UI 使用 WeUI 统一风格

## 快速开始

安装 MySQL、Redis
```
略
```

安装依赖

```
pip install -r requirements.txt
```

创建配置文件
```
cp instance/config.example instance/config.py
vi instance/config.py
```

初始化数据库

```
# into Python shell
>>> from main.models import db
>>> db.create_all()
```

运行

```
python run.py
```

运行队列任务

```
celery -A main.celery worker --beat -l info
```

测试

```
这个开发者很懒，暂时没写下什么测试……
```

部署

```
# using gunicorn
pip install gunicorn

# run
gunicorn -w 3 run:app -p wechat.pid -b 127.0.0.1:8000 -D --log-level warning --error-logfile gunicorn-error.log

# reload
kill -HUP `cat wechat.pid`
```

## License
[MIT](LICENSE)
