# 校园二手交易系统 - 完整项目文档



## 项目概述

### 项目简介

**校园二手交易系统**是一个基于Django 5.2框架开发的智能二手交易平台,专为校园场景设计。系统集成了AI协同过滤推荐算法、WebSocket实时通讯、完整的商品审核机制等先进功能,为校园师生提供安全、便捷的二手物品交易服务。

### 项目特点

- 🤖 **AI智能推荐**: 基于协同过滤算法的个性化商品推荐
- 💬 **实时通讯**: WebSocket实时私聊,QQ式聊天界面
- 🔔 **消息推送**: 实时消息和订单通知
- 📊 **数据可视化**: Chart.js图表展示交易分析
- 🎨 **现代化UI**: 玻璃拟态设计,渐变动画效果
- 🖼️ **高质量图片**: Unsplash专业商品图片
- 🔒 **安全审核**: 完整的商品审核机制
- 📱 **响应式设计**: 支持PC和移动端

### 技术栈

#### 后端技术
- **Django 5.2**: Python Web框架
- **Django Channels 4.0**: WebSocket支持
- **Daphne 4.1.0**: ASGI服务器
- **SQLite**: 数据库(可以无缝切换成mysql)
- **Python 3.12**: 编程语言

---

## 项目预览

### 部分前台页面
前台首页：
![首页](https://github.com/user-attachments/assets/926bd2cb-05da-4c92-82bf-f7eaa80f893a)
我的商品：
![我的商品](https://github.com/user-attachments/assets/b023f210-c1ef-4d6a-845b-946ddb48a6fc)
我的订单：
![我的订单](https://github.com/user-attachments/assets/4418ca72-caf8-444e-9e1e-2cf2917ea421)
通知中心：
![通知中心](https://github.com/user-attachments/assets/fc3776a4-606e-4f5f-887a-ff994f7b03b8)
聊天界面：
![聊天界面](https://github.com/user-attachments/assets/41ebdded-95fd-4d08-8c19-e83b19d5abb8)

### 部分后台页面：
后台管理_商品管理
![后台管理_商品管理](https://github.com/user-attachments/assets/f7786eb1-9779-45a1-aa69-99f122dc87fc)
商品审核：
![商品审核](https://github.com/user-attachments/assets/7ce88ca9-0a0f-4fcb-9a54-a5b6637384ef)
后台管理_交易分析：
![后台管理_交易分析](https://github.com/user-attachments/assets/48ea5062-0f01-4aea-94c7-c57319bf685f)

## 技术架构

### 系统架构图

```
┌─────────────────────────────────────────────┐
│              用户浏览器                      │
│  (Chrome/Edge/Firefox/Safari)               │
└─────────────────┬───────────────────────────┘
                  │
                  ├─── HTTP/HTTPS (页面请求)
                  ├─── WebSocket (实时通讯)
                  └─── Ajax (动态加载)
                  │
┌─────────────────▼───────────────────────────┐
│           Daphne ASGI服务器                  │
│         (127.0.0.1:8000)                    │
└─────────────────┬───────────────────────────┘
                  │
    ┌─────────────┼─────────────┐
    │             │             │
    ▼             ▼             ▼
┌────────┐  ┌──────────┐  ┌──────────┐
│  HTTP  │  │WebSocket │  │  静态   │
│  请求  │  │  通道    │  │  文件   │
└───┬────┘  └────┬─────┘  └────┬─────┘
    │            │             │
    ▼            ▼             ▼
┌─────────────────────────────────────┐
│         Django 应用层                │
│  ┌──────────┐  ┌──────────┐        │
│  │ 视图层   │  │ 消费者   │        │
│  │ (Views)  │  │(Consumer)│        │
│  └────┬─────┘  └────┬─────┘        │
│       │             │               │
│  ┌────▼─────────────▼─────┐        │
│  │    业务逻辑层           │        │
│  │  (Services/Models)     │        │
│  └────┬───────────────────┘        │
│       │                             │
│  ┌────▼───────────────────┐        │
│  │   数据访问层(ORM)      │        │
│  └────┬───────────────────┘        │
└───────┼─────────────────────────────┘
        │
        ▼
┌─────────────────┐
│  SQLite数据库   │
│   (db.sqlite3)  │
└─────────────────┘
```

### 应用模块划分

```
apps/
├── accounts/          # 用户认证模块
├── products/          # 商品管理模块
├── orders/            # 订单交易模块
├── messages_app/      # 消息通讯模块
├── recommendations/   # 推荐算法模块
└── admin_panel/       # 管理后台模块
```

---

## 功能模块

### 前台系统

#### 1. 用户系统
- **用户注册**: 学号、邮箱、密码注册
- **用户登录**: 支持用户名/邮箱登录
- **个人中心**: 查看和编辑个人资料
- **我的商品**: 管理自己发布的商品
- **我的订单**: 查看买家/卖家订单
- **收藏夹**: 管理收藏的商品

#### 2. 商品功能
- **商品发布**: 发布二手商品(需审核)
- **商品浏览**: 瀑布流展示商品列表
- **商品搜索**: 关键词搜索商品
- **分类筛选**: 按分类浏览商品
- **排序功能**: 最新发布、价格最高、价格最低
- **商品详情**: 查看商品详细信息
- **商品收藏**: 收藏感兴趣的商品
- **商品管理**: 上架、下架、删除自己的商品

#### 3. 交易功能
- **下单购买**: 创建订单
- **订单管理**: 查看订单状态
- **订单确认**: 卖家确认订单
- **订单完成**: 买家确认收货
- **订单取消**: 取消未确认订单
- **商品评价**: 交易完成后评价

#### 4. 通讯功能
- **实时私聊**: WebSocket实时聊天
- **会话列表**: QQ式左侧会话列表
- **消息通知**: 实时消息推送
- **未读提示**: 红点角标显示未读数
- **已读状态**: 智能消息已读逻辑

#### 5. 推荐系统
- **个性化推荐**: 基于协同过滤算法
- **浏览历史**: 记录用户浏览行为
- **相似商品**: 推荐相似商品
- **热门商品**: 冷启动推荐

### 管理后台

#### 1. 数据仪表盘
- **核心指标**: 活跃用户、新增商品、交易额、AI转化率
- **增长趋势**: 对比昨日数据
- **交易走势**: 近7日交易趋势图
- **分类占比**: 热门商品分类统计
- **待审核**: 待审核商品列表

#### 2. 用户管理
- **用户列表**: 分页展示所有用户
- **搜索功能**: 按用户名、邮箱、学号搜索
- **状态筛选**: 筛选活跃/禁用用户
- **启用/禁用**: 一键启用或禁用用户账户
- **用户详情**: 查看用户详细信息

#### 3. 商品管理
- **商品列表**: 展示所有已审核商品
- **搜索筛选**: 按标题、分类、状态筛选
- **商品编辑**: 编辑商品信息
- **上下架**: 控制商品展示状态
- **删除商品**: 删除违规商品

#### 4. 商品审核
- **待审核列表**: 展示所有待审核商品
- **审核通过**: 一键通过审核
- **审核驳回**: 填写驳回理由
- **实时推送**: 新商品自动提醒
- **状态筛选**: 待审核/已通过/已驳回

#### 5. 订单管理
- **订单列表**: 展示所有订单
- **订单搜索**: 按订单号、用户名搜索
- **状态筛选**: 按订单状态筛选
- **订单详情**: 查看订单详细信息
- **数据统计**: 订单状态分布统计

#### 6. 交易分析
- **核心指标**: 总订单、总交易额、转化率、活跃用户
- **时间筛选**: 7天/30天/90天数据
- **交易趋势**: 双Y轴折线图(交易额+订单数)
- **分类分析**: 饼图展示分类销售占比
- **状态分布**: 商品状态、订单状态分布
- **TOP10榜单**: 热门商品、活跃卖家排行

---

## 数据库设计

### 核心数据表

#### 1. User (用户表)
```python
字段:
- username: 用户名(唯一)
- email: 邮箱(唯一)
- password: 密码(加密)
- student_id: 学号
- college: 学院
- phone: 手机号
- avatar: 头像
- bio: 个人简介
- campus_location: 校区位置
- credit_score: 信用分数
- is_active: 是否激活
- is_staff: 是否管理员
- created_at: 创建时间
```

#### 2. Category (商品分类表)
```python
字段:
- name: 分类名称
- icon: 图标类名
- description: 描述
- is_active: 是否启用
- order: 排序
```

#### 3. Product (商品表)
```python
字段:
- title: 商品标题
- description: 商品描述
- price: 价格
- seller: 卖家(外键User)
- category: 分类(外键Category)
- condition: 成色
- status: 状态(available/reserved/sold/removed)
- review_status: 审核状态(pending/active/rejected)
- location: 交易地点
- views_count: 浏览次数
- favorites_count: 收藏次数
- is_featured: 是否推荐
- created_at: 发布时间
- updated_at: 更新时间
```


---

## 核心功能详解

### 1. 协同过滤推荐算法

#### 算法原理
基于物品的协同过滤(Item-based Collaborative Filtering):
1. 收集用户行为数据(浏览、收藏)
2. 计算商品间的相似度
3. 根据用户历史行为推荐相似商品

#### 相似度计算
```python
def calculate_similarity(product1, product2):
    score = 0
    
    # 1. 分类相同 +50分
    if product1.category == product2.category:
        score += 50
    
    # 2. 价格相近 +30分
    price_diff = abs(product1.price - product2.price)
    if price_diff < 100:
        score += 30
    elif price_diff < 500:
        score += 15
    
    # 3. 成色相同 +20分
    if product1.condition == product2.condition:
        score += 20
    
    return score
```

#### 推荐流程
```
1. 获取用户浏览历史
   ↓
2. 找出浏览过的商品
   ↓
3. 计算与其他商品的相似度
   ↓
4. 按相似度排序
   ↓
5. 返回Top N推荐结果
```

### 2. WebSocket实时通讯

#### 技术实现
- **Django Channels**: WebSocket支持
- **InMemoryChannelLayer**: 内存通道层(开发环境)
- **异步消费者**: async/await语法

#### 消息流程
```
用户A发送消息
   ↓
WebSocket → ChatConsumer
   ↓
保存到数据库
   ↓
通过Channel Layer广播
   ↓
用户B的WebSocket接收
   ↓
前端渲染消息
```

#### 连接管理
```javascript
// 前端连接
const chatSocket = new WebSocket(
    'ws://' + window.location.host + '/ws/chat/' + conversationId + '/'
);

chatSocket.onmessage = function(e) {
    const data = JSON.parse(e.data);
    // 渲染消息
};
```

### 3. 商品审核机制

#### 审核流程
```
用户发布商品
   ↓
状态: pending (待审核)
   ↓
创建"商品审核中"通知
   ↓
管理员审核
   ├─ 通过 → status: active → 创建"审核通过"通知
   └─ 驳回 → status: rejected → 创建"审核未通过"通知(含理由)
```

#### 审核状态
- **pending**: 待审核(不在首页展示)
- **active**: 已通过(正常展示)
- **rejected**: 已驳回(不展示,用户可修改)

#### 通知推送
```python
# 审核通过
Notification.objects.create(
    recipient=product.seller,
    notification_type='product_approved',
    title='商品审核通过',
    content=f'恭喜!您发布的商品《{product.title}》已通过审核...',
    related_product=product
)

# 发送WebSocket通知
NotificationService.send_realtime_notification(product.seller.id)
```

### 4. Ajax动态加载

#### 实现方式
```javascript
// 前端请求
fetch(`/api/products/?page=${page}&sort=${sort}`)
    .then(response => response.json())
    .then(data => {
        // 渲染商品卡片
        data.products.forEach(product => {
            container.innerHTML += createProductCard(product);
        });
    });
```

#### 后端API
```python
def products_api(request):
    page = int(request.GET.get('page', 1))
    sort = request.GET.get('sort', 'latest')
    
    # 排序逻辑
    if sort == 'price_high':
        queryset = queryset.order_by('-price')
    elif sort == 'price_low':
        queryset = queryset.order_by('price')
    
    # 返回JSON
    return JsonResponse({
        'products': products_data,
        'has_next': has_next,
    })
```

---

## 安装部署


###  访问系统
- 前台: http://127.0.0.1:8000
- 管理后台: http://127.0.0.1:8000/admin-panel/

### 手动安装

#### 1. 创建虚拟环境
```bash
# Windows
python -m venv env
env\Scripts\activate

# Linux/Mac
python3 -m venv env
source env/bin/activate
```

#### 2. 安装依赖
```bash
pip install -r requirements.txt
```

#### 3. 数据库迁移
```bash
python manage.py makemigrations
python manage.py migrate
```

#### 4. 启动服务器
```bash
daphne -b 127.0.0.1 -p 8000 config.asgi:application
```
---

## 使用指南

### 前台用户操作

#### 注册登录
1. 访问首页
2. 点击右上角"登录/注册"
3. 填写注册信息或使用测试账号登录

#### 浏览商品
1. 首页自动加载商品列表
2. 点击分类标签筛选商品
3. 使用搜索框搜索商品
4. 切换排序方式(最新/价格高/价格低)
5. 点击"加载更多"查看更多商品

#### 发布商品
1. 登录后点击"发布商品"
2. 填写商品信息(标题、价格、分类等)
3. 上传商品图片(支持多图)
4. 点击"发布"提交审核
5. 等待管理员审核
6. 收到审核通知

#### 购买商品
1. 浏览商品,点击进入详情页
2. 点击"立即购买"按钮
3. 填写联系方式和交易地点
4. 确认订单信息
5. 等待卖家确认
6. 线下交易
7. 确认收货
8. 评价交易

#### 私聊卖家
1. 在商品详情页点击"联系卖家"
2. 进入聊天界面
3. 发送消息(支持Enter快速发送)
4. 实时接收回复
5. 查看消息已读状态

### 管理员操作

#### 登录后台
1. 使用管理员账号登录(admin/admin)
2. 访问 http://127.0.0.1:8000/admin-panel/
3. 进入管理后台

#### 审核商品
1. 点击"商品审核"菜单
2. 查看待审核商品列表
3. 点击"通过"直接通过审核
4. 点击"驳回"填写驳回理由
5. 用户会收到审核通知

#### 管理用户
1. 点击"用户管理"菜单
2. 搜索或筛选用户
3. 点击"启用/禁用"切换用户状态
4. 查看用户详细信息

#### 查看数据分析
1. 点击"交易分析"菜单
2. 选择时间范围(7/30/90天)
3. 查看交易趋势图表
4. 查看分类销售占比
5. 查看TOP10榜单

---

## API接口

### 商品API

#### 获取商品列表
```
GET /api/products/
参数:
  - page: 页码(默认1)
  - sort: 排序(latest/price_high/price_low)
  
响应:
{
  "products": [
    {
      "id": 1,
      "title": "iPhone 13",
      "price": "3999.00",
      "status": "available",
      "main_image": "/media/products/product_1.jpg",
      "seller_name": "user001",
      "seller_college": "计算机学院",
      "location": "东区宿舍"
    }
  ],
  "has_next": true,
  "current_page": 1
}
```

### 消息API

#### 获取未读消息数
```
GET /messages/api/unread-count/
响应:
{
  "count": 5
}
```

### 管理后台API

#### 获取待审核商品数
```
GET /admin-panel/review/pending-count/
响应:
{
  "count": 3
}
```

---


## 项目亮点

### 技术亮点
1. **Django 5.2最新框架**: 使用最新稳定版本
2. **WebSocket实时通讯**: 真正的实时聊天体验
3. **协同过滤算法**: AI个性化推荐
4. **Ajax无刷新**: 流畅的用户体验
5. **Chart.js可视化**: 专业的数据展示
6. **完整审核机制**: 规范的内容管理

### 业务亮点
1. **完整闭环**: 从发布到交易的完整流程
2. **双端系统**: 前台+管理后台
3. **实时通知**: 消息和订单实时推送
4. **智能推荐**: 提升交易转化率
5. **审核机制**: 保证商品质量
6. **数据分析**: 运营决策支持

### 设计亮点
1. **现代化UI**: 玻璃拟态、渐变动画
2. **响应式布局**: 适配各种屏幕
3. **高质量图片**: Unsplash专业图片
4. **交互动画**: 流畅的过渡效果
5. **用户体验**: 简洁直观的操作

---



## 技术支持

### 文档资源
- **运行说明**: 详细的安装运行步骤
- **使用指南**: 功能使用说明
- **快速开始**: 快速入门指南
- **API文档**: 接口说明
- **更新日志**: 版本更新记录

### 支持服务
- **代码问题**: 代码本身运行问题可协助解决
- **功能咨询**: 功能使用疑问解答
- **远程部署**: 80元远程部署服务(单独购买)
- **定制开发**: 功能定制需求单独沟通

### 联系方式
- 有疑问请及时联系：alex522622
- 消息会及时回复
- 提供技术支持

---

## 版权声明

### 知识产权
- ✅ 源码为个人知识产权
- ✅ 严禁倒卖、侵权必究
- ✅ 仅供学习和商业使用
- ✅ 不得用于违法用途

### 使用许可
- ✅ 可用于个人学习
- ✅ 可用于毕业设计
- ✅ 可用于商业项目
- ✅ 可进行二次开发

---


## 总结

### 项目优势
1. **功能完整**: 20+核心功能模块
2. **技术先进**: Django 5.2 + WebSocket + AI推荐
3. **开箱即用**: 一键启动,自动化测试数据
4. **文档齐全**: 10+详细文档
5. **易于扩展**: 清晰的架构,标准的规范
6. **高性价比**: 节省4-6周开发时间

### 适用场景
- ✅ 校园二手交易平台
- ✅ 毕业设计项目
- ✅ Django学习案例
- ✅ WebSocket实战项目
- ✅ 推荐算法实践
- ✅ 电商系统参考

### 学习价值
- 🎓 完整的Django项目实战
- 🎓 WebSocket实时通讯实现
- 🎓 协同过滤推荐算法
- 🎓 前后端分离开发
- 🎓 数据可视化实践
- 🎓 项目部署经验

---
