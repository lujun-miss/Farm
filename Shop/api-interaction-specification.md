# 前后端数据交互规范

## 一、通用规范

### 1. 数据格式
- **请求/响应格式**：JSON
- **字符编码**：UTF-8
- **日期时间格式**：ISO 8601（YYYY-MM-DDTHH:mm:ssZ）
- **数字格式**：使用浮点型或整型，避免使用字符串
- **布尔值**：使用true/false，不使用0/1

### 2. 命名约定
- **API路径**：使用小写字母和连字符（kebab-case），如 `/api/agent-regions`
- **查询参数**：使用小写字母和下划线（snake_case），如 `page_size=10`
- **请求体字段**：使用驼峰命名法（camelCase），如 `agentName`
- **响应体字段**：使用驼峰命名法（camelCase）

### 3. 错误处理

#### 错误响应格式
```json
{
  "code": "ERR_001",
  "message": "请求参数错误",
  "details": {
    "field": "regionId",
    "reason": "区域ID不能为空"
  },
  "timestamp": "2026-01-16T10:30:00Z"
}
```

#### 错误码定义
| 错误码 | 错误类型 | 说明 |
|--------|----------|------|
| ERR_001 | 请求参数错误 | 缺少必填参数或参数格式不正确 |
| ERR_002 | 认证错误 | 认证失败或令牌过期 |
| ERR_003 | 授权错误 | 没有操作权限 |
| ERR_004 | 资源不存在 | 请求的资源不存在 |
| ERR_005 | 业务逻辑错误 | 违反业务规则 |
| ERR_006 | 系统错误 | 服务器内部错误 |

### 4. 分页规范

#### 请求参数
- `page`: 当前页码（从1开始）
- `page_size`: 每页记录数（默认20，最大100）

#### 响应格式
```json
{
  "data": [
    // 数据列表
  ],
  "pagination": {
    "page": 1,
    "page_size": 20,
    "total": 100,
    "total_pages": 5
  },
  "timestamp": "2026-01-16T10:30:00Z"
}
```

## 二、认证与授权

### 1. 认证机制
- 使用JWT（JSON Web Token）进行身份认证
- Token有效期：24小时
- 支持令牌刷新机制

### 2. 授权机制
- 基于RBAC（角色基础访问控制）
- 支持细粒度权限控制（API级、数据级）

### 3. 认证流程
1. 客户端使用用户名密码获取Token
2. 客户端在请求头中携带Token：`Authorization: Bearer <token>`
3. 服务器验证Token的有效性
4. 服务器根据Token中的用户信息进行授权判断

## 三、代理商后端API规范

### 1. 区域管理API

#### 获取区域列表
```
GET /api/agent-regions?page=1&page_size=20
```

**响应**：
```json
{
  "data": [
    {
      "id": "reg_001",
      "name": "曹县区域",
      "level": "county",
      "parentId": "city_001",
      "coordinates": {},
      "status": "active",
      "createdAt": "2026-01-16T08:00:00Z",
      "updatedAt": "2026-01-16T08:30:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "page_size": 20,
    "total": 5,
    "total_pages": 1
  }
}
```

#### 创建区域
```
POST /api/agent-regions
```

**请求体**：
```json
{
  "name": "新区域",
  "level": "county",
  "parentId": "city_001",
  "coordinates": {},
  "status": "active"
}
```

### 2. 区域保护规则API

#### 获取规则列表
```
GET /api/protection-rules?page=1&page_size=20
```

#### 创建规则
```
POST /api/protection-rules
```

**请求体**：
```json
{
  "regionId": "reg_001",
  "productCategoryId": "cat_001",
  "minPrice": 100,
  "maxPrice": 200,
  "priority": 1,
  "startTime": "2026-01-16T00:00:00Z",
  "endTime": "2026-12-31T23:59:59Z",
  "status": "active"
}
```

### 3. 订单分配API

#### 获取分配的订单
```
GET /api/assigned-orders?page=1&page_size=20&status=pending
```

#### 接受订单
```
POST /api/orders/:id/accept
```

## 四、厂家后端API规范

### 1. 全局规则管理API

#### 获取全局规则列表
```
GET /api/global-rules?page=1&page_size=20
```

#### 创建全局规则
```
POST /api/global-rules
```

**请求体**：
```json
{
  "productId": "prod_001",
  "channelId": "chan_001",
  "priority": 1,
  "minPrice": 100,
  "maxPrice": 200,
  "validRegions": ["reg_001", "reg_002"],
  "invalidRegions": ["reg_003"],
  "startTime": "2026-01-16T00:00:00Z",
  "endTime": "2026-12-31T23:59:59Z",
  "status": "active"
}
```

### 2. 代理商管理API

#### 获取代理商列表
```
GET /api/agents?page=1&page_size=20&status=approved
```

#### 创建代理商
```
POST /api/agents
```

**请求体**：
```json
{
  "name": "新代理商",
  "contactPerson": "张三",
  "phone": "13800138000",
  "email": "agent@example.com",
  "address": "山东省菏泽市曹县",
  "level": "primary",
  "status": "pending",
  "regions": ["reg_001"],
  "creditRating": 90
}
```

### 3. 区域规划API

#### 获取区域规划建议
```
GET /api/region-planning/suggestions?agentId=agent_001&productCategoryId=cat_001
```

#### 优化区域划分
```
POST /api/region-planning/optimize
```

**请求体**：
```json
{
  "regionIds": ["reg_001", "reg_002"],
  "agentId": "agent_001"
}
```

## 五、前端与后端交互流程

### 1. 地址选择与区域保护流程

```
前端                             后端
│                                │
│ 1. 显示订单商品列表             │
│                                │
│ 2. 点击"选择地址"按钮           │
│                                │
│ 3. 获取可选地址列表 ──────────→ │
│                                │
│ 4. 显示地址选择弹窗             │
│                                │
│ 5. 用户选择地址                │
│                                │
│ 6. 检查区域保护规则 ──────────→ │
│                                │
│ 7. 返回区域保护结果 ←───────── │
│                                │
│ 8. 显示区域保护弹窗             │
│                                │
│ 9. 用户确认                    │
│                                │
│10. 更新订单信息    ──────────→ │
│                                │
│11. 返回更新结果 ←───────── │
│                                │
│12. 更新页面显示                │
│                                │
```

### 2. 订单分配流程

```
前端                             后端
│                                │
│ 1. 请求分配的订单列表 ─────────→ │
│                                │
│ 2. 返回订单列表 ←──────────── │
│                                │
│ 3. 显示订单列表                │
│                                │
│ 4. 点击"接受订单"按钮          │
│                                │
│ 5. 接受订单请求    ──────────→ │
│                                │
│ 6. 处理订单分配                │
│                                │
│ 7. 返回处理结果 ←──────────── │
│                                │
│ 8. 更新订单状态                │
│                                │
```

## 六、数据同步机制

### 1. 实时数据同步
- **技术方案**：WebSocket
- **适用场景**：订单分配通知、区域规则更新、库存变化等
- **连接地址**：`wss://api.example.com/ws`

### 2. 定时数据同步
- **技术方案**：REST API + 定时任务
- **同步周期**：
  - 基础数据：每日同步一次
  - 销售数据：每小时同步一次
  - 库存数据：实时同步

### 3. 数据一致性保障
- 使用乐观锁机制防止并发冲突
- 实现数据版本控制
- 提供数据同步状态查询接口

## 七、安全策略

### 1. 传输安全
- 使用HTTPS加密传输
- 禁用不安全的TLS版本
- 使用强加密算法

### 2. 输入验证
- 所有输入参数都进行验证
- 使用参数绑定和类型检查
- 防止SQL注入、XSS攻击等

### 3. 输出编码
- 对所有输出数据进行编码
- 防止XSS攻击

### 4. 限流策略
- 实现API限流机制
- 防止DDoS攻击
- 保护系统资源

## 八、性能优化

### 1. 缓存策略
- 对频繁访问的数据进行缓存
- 使用Redis等缓存技术
- 实现缓存失效机制

### 2. API响应时间
- 普通API响应时间应小于500ms
- 复杂查询API响应时间应小于2s
- 超过2s的操作应提供异步处理机制

### 3. 批量操作
- 提供批量创建、更新、删除API
- 减少网络请求次数

## 九、版本管理

### API版本控制
- 使用URL路径版本控制，如 `/api/v1/agent-regions`
- 支持多版本并存
- 提供版本迁移指南

### 文档版本控制
- 文档应包含版本号
- 记录版本变更历史
- 提供版本对比功能

---

版本：1.0
日期：2026-01-16
作者：技术团队