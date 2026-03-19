---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: "00000000000000000000000000000000"
    PropagateID: "00000000000000000000000000000000"
    ReservedCode1: 3046022100acc8cc44c0ae4dbf4a3e450dae85cc250a648932fbc2db2506b0fe1343dd9fea022100856bc99fc2426b326d8d9f0fcbafefb25e356fd8648167fd8c6c7d11afd53b6c
    ReservedCode2: 304502204f23ff0cf914b467ac1581735eb06b8aecd0fc793037593a6750707ac81c7e93022100815be44d78c8f39a31a8e8ae868c0a6ad2ca5eb6f8a627e747c0323bdc428d97
description: 高德地图导航技能。使用高德地图 Web API 提供定位、附近搜索、路径规划等服务。
name: amap-navigator
---

# 高德地图导航技能

> ✅ API Key 已配置：存储于 openclaw.json → gateway.env.AMAP_KEY

## 功能

- 📍 当前位置反地理编码（经纬度 → 地址）
- 🏬 附近 POI 搜索（商场、快餐、门店等）
- 🧭 路径规划（步行/驾车/公交）
- 🍽️ 附近美食/购物/出行搜索

## 环境变量

| 变量 | 值 | 来源 |
|------|-----|------|
| AMAP_KEY | 88378a408d54d46b75f14795f8db053f | openclaw.json gateway.env |

## 常用调用方式

```python
import urllib.request, urllib.parse, json, os

key = os.environ.get('AMAP_KEY')
params = urllib.parse.urlencode({
    "key": key,
    "location": "116.330709,39.994513",
    "keywords": "商场",
    "radius": "3000",
    "types": "购物服务",
    "extensions": "all"
})
url = "https://restapi.amap.com/v3/place/around?" + params
resp = urllib.request.urlopen(urllib.request.Request(url), timeout=10)
data = json.loads(resp.read())
```
