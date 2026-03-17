---
name: life-query
description: Daily life query assistant. Declarative YAML API registry with natural language intent matching. Trigger when the user needs to track a parcel, check shipment status, or mentions "package tracking", "courier tracking", "tracking number", "where is my parcel", etc. More life query capabilities will be added over time.
---

# Life Query

日常生活查询助手。`apis/` 目录即接口注册表，放入 `.yaml` 自动发现，开箱即用。

## 可用接口

| 接口 | 方法 | 路径 | 说明 |
|------|------|------|------|
| courier-track | POST | /skill/courier/track | 查询快递物流轨迹 |

## 使用方式

```bash
# 查快递
bash scripts/run.sh call courier-track --trackingNumber SF1234567890
bash scripts/run.sh call courier-track --trackingNumber SF1234567890 --carrierCode shunfeng

# 用自己的快递100凭证（可选）
bash scripts/run.sh call courier-track --trackingNumber SF1234567890 \
  --kuaidi100Key YOUR_KEY --kuaidi100Customer YOUR_CUSTOMER

# 列出所有接口
bash scripts/run.sh list

# 输出格式（json 默认，table 可读）
bash scripts/run.sh call courier-track --trackingNumber SF1234567890 --format table
```

## 自然语言映射

| 用户说 | 接口 | 关键参数 |
|--------|------|---------|
| "帮我查一下 SF1234567890" | courier-track | trackingNumber=SF1234567890 |
| "这个单号的物流在哪里：75555555555" | courier-track | trackingNumber=75555555555 |
| "用我自己的快递100 key 查单号" | courier-track | +kuaidi100Key/Customer |

