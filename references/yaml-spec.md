# 接口 YAML 定义规范

新增接口时，在 `apis/` 目录创建 `{资源}-{动作}.yaml`（kebab-case），放入后自动注册。

## 字段说明

```yaml
# 元信息
name: courier-track          # 必填，唯一标识，与文件名一致
description: 查询快递轨迹    # 必填，Claude 靠它匹配用户意图
tags: [快递, 查询]           # 可选

# 请求
method: POST                 # GET | POST | PUT | DELETE | PATCH
path: /skill/courier/track   # 拼接 _env.yaml base_url

headers:                     # 可选，额外或覆盖公共 header
  X-Custom: value

params:                      # GET 查询参数
  page:
    type: int
    default: 1
    description: 页码

body:                        # POST/PUT 请求体
  content_type: application/json
  fields:
    trackingNumber:
      type: string
      required: true
      description: 快递单号

# 响应
response:
  data_path: data            # JSON 提取路径，点号嵌套，如 data.list
  total_path: data.total     # 可选，总数路径
  columns:
    - field: status
      label: 状态
```

## 路径参数

在 `path` 中使用 `{param}` 占位，并在 `body.fields` 或 `params` 中添加同名字段，`run.sh` 会自动替换。

```yaml
path: /api/v1/users/{id}
body:
  fields:
    id:
      type: int
      required: true
      description: 用户 ID
```

## 复杂接口

分页遍历、多步骤等复杂逻辑使用 `.sh` 脚本，文件头注释格式：

```bash
#!/usr/bin/env bash
# name: users-export
# description: 全量导出（自动分页）
# tags: 用户,导出
```

## _env.yaml 公共配置

```yaml
base_url: ${FENXIANG_API_BASE_URL}
headers:
  X-Api-Key: "${FENXIANG_API_KEY}"
  Content-Type: application/json
timeout: 30
```

`${VAR}` 运行时从环境变量替换。
