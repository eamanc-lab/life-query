---
name: life-query
description: Track parcels and check courier shipment status for Chinese carriers (SF Express, YTO, JD, ZTO, etc.) via natural language. Use when user asks to "查快递", "track package", "tracking number", "物流查询", "快递单号", "where is my parcel", "shipment status", "包裹到哪了".
---

# Life Query — 日常生活查询助手

查快递物流轨迹，支持国内主流快递公司（顺丰、圆通、京东、中通等），输入单号即可查询。

## 使用场景

- 用户发来一个快递单号，想知道包裹到哪了
- 用户说"帮我查一下 SF1234567890 的物流"
- 用户问"我的快递到了吗"、"这个单号是什么状态"

## 可用接口

| 接口 | 方法 | 说明 |
|------|------|------|
| courier-track | POST | 查询快递物流轨迹 |

## 使用方式

```bash
# 查快递（自动识别快递公司）
bash scripts/run.sh call courier-track --trackingNumber SF1234567890

# 指定快递公司
bash scripts/run.sh call courier-track --trackingNumber SF1234567890 --carrierCode shunfeng

# 用自己的快递100凭证（可选）
bash scripts/run.sh call courier-track --trackingNumber SF1234567890 \
  --kuaidi100Key YOUR_KEY --kuaidi100Customer YOUR_CUSTOMER

# 列出所有接口
bash scripts/run.sh list

# 表格格式输出
bash scripts/run.sh call courier-track --trackingNumber SF1234567890 --format table
```

## 自然语言映射

| 用户说 | 接口 | 关键参数 |
|--------|------|---------|
| "帮我查一下 SF1234567890" | courier-track | trackingNumber=SF1234567890 |
| "这个单号的物流在哪里：75555555555" | courier-track | trackingNumber=75555555555 |
| "用我自己的快递100 key 查单号" | courier-track | +kuaidi100Key/Customer |
