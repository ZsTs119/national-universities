# 全国学校数据库 (NationalUniversitiesJson)

## 项目简介

这是一个收集和整理全国各省份学校（主要是大学和中小学）数据的工具集。项目基于百度地图 API，能够检索并保存全国各地区的学校数据，支持按省份进行数据筛选和整理。

## 功能特点

- 基于百度地图 API 自动收集全国各地区学校信息
- 支持数据过滤，剔除无关信息
- 提供按省份分类的学校数据
- 数据格式为 JSON，方便开发者使用和集成
- 包含学校名称、省份、城市、区域、地理位置和详细地址等信息

## 项目结构

```
NationalUniversitiesJson/
├── public/                      # 整理后的数据文件
│   ├── areas.json               # 中国行政区划数据
│   ├── 大学.json                # 全国大学数据
│   └── 中小学.json              # 全国中小学数据
└── universityCollecter/         # 数据采集工具
    ├── spiders/                 # 爬虫模块
    │   └── spider.py            # 主爬虫程序，基于百度地图API收集数据
    ├── dataHandle.py            # 数据处理模块，用于筛选和整理数据
    ├── areas.json               # 行政区划数据（爬虫使用）
    ├── settings.py              # 爬虫配置文件
    ├── items.py                 # 数据项定义
    ├── middlewares.py           # 中间件配置
    ├── pipelines.py             # 数据处理管道
    └── scrapy.cfg               # Scrapy配置文件
```

## 数据格式

学校数据 JSON 格式示例：

```json
[
  {
    "name": "清华大学", // 学校名称
    "province": "北京市", // 所在省份
    "city": "北京市", // 所在城市
    "area": "海淀区", // 所在区域
    "location": {
      // 地理坐标
      "lat": 40.00359,
      "lng": 116.32142
    },
    "address": "北京市海淀区清华园" // 详细地址
  }
  // 更多学校数据...
]
```

## 使用说明

### 数据采集

1. 安装依赖：

   ```bash
   pip install scrapy requests
   ```

2. 配置百度地图 API：

   - 在 [百度地图开放平台](http://lbsyun.baidu.com/apiconsole/key/create) 申请开发者密钥(AK)
   - 将获取的 AK 替换到 `universityCollecter/spiders/spider.py` 文件中的 `ak` 参数

3. 运行爬虫收集数据：

   ```bash
   cd universityCollecter
   scrapy runspider universityCollecter/spiders/spider.py
   ```

   爬虫参数说明：

   - `ak`: 百度地图开发者密钥
   - `file_name`: 保存的文件名
   - API 参数可参考[百度地图开发文档](https://lbsyun.baidu.com/faq/api?title=webapi/guide/webservice-placeapi/district)

### 数据处理

运行数据处理脚本，按省份筛选和整理数据：

```bash
python universityCollecter/dataHandle.py
```

数据处理参数说明：

- `search`: 筛选的字段名，可根据需要修改
- 处理后的数据将按省份保存为独立的 JSON 文件

## 开发计划

- [ ] 增加更多过滤条件和数据字段
- [ ] 提供 Web 界面进行数据可视化
- [ ] 支持更多数据源和 API 集成
- [ ] 完善数据分类和标签系统

## 问题反馈

在使用中有任何问题，欢迎反馈：

- 邮件：zsts@foxmail.com
- GitHub Issues

## 捐助支持

在兴趣的驱动下，我创建了这个免费的工具。如果您觉得它对您有所帮助，欢迎给予支持和鼓励！

## 关于作者

```javascript
var ihubo = {
  nickName: "ZsTs119",
  site: "https://github.com/ZsTs119",
};
```

## 许可证

MIT
