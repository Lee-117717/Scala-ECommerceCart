# Scala 电商购物车系统

基于 Scala + Slick + MySQL 的命令行电商购物车管理系统。

## 项目简介

本项目实现了一个功能完整的电商购物车系统，支持商品管理、购物车操作、订单结算和支付等核心业务流程。系统采用分层架构设计，包含实体层（entity）、数据访问层（dao）、数据库映射层（schema）、业务逻辑层（service）和用户界面层（ui）。

## 技术栈

- **语言**: Scala 2.11.10
- **构建工具**: SBT
- **数据库**: MySQL 5.x
- **ORM 框架**: Slick 3.2.3
- **数据库驱动**: MySQL Connector/J 5.1.47

## 功能模块

### 1. 商品管理
- 商品上架（新增商品到库存）
- 查看所有商品库存信息
- 库存预警（充足/紧张/售罄）

### 2. 购物车管理
- 添加商品到购物车
- 修改购物车商品数量
- 删除购物车商品
- 查看购物车列表（含小计与总计）

### 3. 订单管理
- 购物车结算生成订单
- 事务内扣减库存
- 查看所有订单列表
- 查看订单详情（含订单项明细）

### 4. 支付模拟
- 订单支付状态更新（待支付 → 已支付）

## 项目结构

```
Scala-ECommerceCart/
├── build.sbt                          # SBT 构建配置
├── docs/
│   └── 实验报告.docx                   # 项目实践报告
├── sql/
│   └── ecommerce_cart.sql              # 数据库初始化脚本
├── src/main/
│   ├── resources/
│   │   └── application.conf           # Slick 数据库配置
│   └── scala/com/ecommerce/
│       ├── App.scala                   # 程序入口
│       ├── entity/                     # 实体类
│       │   ├── Product.scala           # 商品实体
│       │   ├── CartItem.scala          # 购物车项实体
│       │   ├── Order.scala             # 订单实体
│       │   └── OrderItem.scala         # 订单项实体
│       ├── schema/                     # 数据库表映射
│       │   ├── ProductTable.scala
│       │   ├── CartTable.scala
│       │   ├── OrderTable.scala
│       │   └── OrderItemTable.scala
│       ├── dao/                        # 数据访问层
│       │   ├── ProductDAO.scala
│       │   ├── CartDAO.scala
│       │   ├── OrderDAO.scala
│       │   └── OrderItemDAO.scala
│       ├── service/                    # 业务逻辑层
│       │   ├── ProductService.scala
│       │   ├── CartService.scala
│       │   └── OrderService.scala
│       ├── db/
│       │   └── DBUtil.scala            # 数据库连接工具
│       └── ui/
│           └── Menu.scala              # 命令行交互菜单
└── project/
    └── build.properties                # SBT 版本配置
```

## 环境要求

- JDK 1.8+
- Scala 2.11.x
- SBT 1.x
- MySQL 5.7+

## 快速开始

### 1. 初始化数据库

执行项目根目录下的 SQL 脚本创建数据库和表结构：

```bash
mysql -u root -p < sql/ecommerce_cart.sql
```

### 2. 配置数据库连接

修改 `src/main/resources/application.conf` 和 `src/main/scala/com/ecommerce/db/DBUtil.scala` 中的数据库连接信息（用户名、密码等）。

### 3. 编译运行

```bash
cd SimpleECommerceCart
sbt run
```

### 4. 使用系统

启动后根据命令行菜单提示进行操作：
- 输入数字 1-8 选择对应功能
- 按提示输入商品信息、数量等参数
- 系统会自动校验数据合法性

## 数据库表结构

| 表名 | 说明 |
|------|------|
| products | 商品库存表 |
| cart_items | 购物车表 |
| orders | 订单主表 |
| order_items | 订单项明细表 |

## 设计特点

- **分层架构**: 清晰的 entity → dao → service → ui 分层，职责明确
- **事务安全**: 结算操作使用数据库事务，保证库存、订单、购物车数据一致性
- **输入校验**: 多层校验机制（UI 层 + Service 层），防止非法数据
- **友好交互**: 命令行菜单引导式操作，支持自动填充和快捷跳转

## 作者

GitHub: @Lee-117717

## 许可证

本项目仅用于学习目的。
