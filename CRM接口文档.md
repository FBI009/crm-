## CRM接口文档

### 系统基础模块

#### 1. 登录接口

​	1. 请求方式： POST

​	2. 请求地址： http://127.0.0.1:8000/api/login/

 3. 请求参数： 

 4. 响应结果：成功{'code': 200,  'data': '登录成功'}；  失败{'code': 401, 'data': '登录失败'}

 5. 用户表设计（User)

    |    字段     | 字段名称 |    类型     |     约束     |       备注       |
    | :---------: | :------: | :---------: | :----------: | :--------------: |
    |  username   |  用户名  |   TINYINT   |   not null   |       唯一       |
    |  password   |   密码   |   TINYINT   |   not null   |                  |
    |    phone    | 手机号码 |   TINYINT   |   not null   |                  |
    |   mailbox   |   邮箱   |   TINYINT   |   not null   |                  |
    |    state    |   状态   | Varchar(32) |   not null   | 1. 启用  2. 禁用 |
    | department  |   部门   | Varchar(32) |   Dept_ID    |                  |
| username_ID | 用户_ID  |     int     | pk  not null |                  |
    

#### 2. 部门管理

 1. 请求方式：GET

 2. 请求地址： http://127.0.0.1:8000/api/dept/

 3. 请求参数：

 4. 响应结果：成功{'code': 1000,  'data': '获取成功'}；  失败{'code': 2000, 'data': '获取失败'}

 5. 部门表（Dept）

    |         字段          |         字段名称         |    类型     |     约束     | 备注 |
    | :-------------------: | :----------------------: | :---------: | :----------: | :--: |
    |    general_manager    |          总经理          | Varchar(32) |   not null   |      |
    | accounting_department |          财务部          | Varchar(32) |   not null   |      |
    |    administration     | 行政部（办公室、后勤等） | Varchar(32) |   not null   |      |
    |    human_resources    |        人力资源部        | Varchar(32) |   not null   |      |
    |      technology       |          技术部          | Varchar(32) |   not null   |      |
    |      department       |          仓储部          | Varchar(32) |   not null   |      |
    |      department       |          计划部          | Varchar(32) |   not null   |      |
    |        client         |          客户部          | Varchar(32) |   not null   |      |
    |        Dept_ID        |            ID            |     int     | pk  not null |      |

#### 3. 角色权限管理

 1. 请求方式：POST， GET， PUT， DELETE

 2. 请求地址：http://127.0.0.1:8000/api/role/

 3. 请求参数：

 4. 响应结果：JSON

 5. 角色表（Role)

    |   字段   | 字段名称 |    类型     |     约束     | 备注 |
    | :------: | :------: | :---------: | :----------: | :--: |
    |    ID    |  角色ID  |     int     | PK  not null |      |
    | RoleName |  角色名  | Varchar(32) |   not null   |      |

6. 用户与角色关联表（User_Role)

   |  字段   | 字段名称 | 类型 |    约束     | 备注 |
   | :-----: | :------: | :--: | :---------: | :--: |
   |   ID    |    ID    | int  | PK not null |      |
   | User_Id |  用户ID  | int  | FK not null |      |
   | Role_Id |  角色ID  | int  | FK not null |      |

   7. 权限表(Power)

      |   字段    | 字段名称 |     类型      |    约束     | 备注 |
      | :-------: | :------: | :-----------: | :---------: | :--: |
      |    ID     |    ID    |      int      | PK not null |      |
      | PowerType | 权限类型 | Varchar（50） |  not null   |      |
      |           |          |               |             |      |

   8. 角色与权限关联表(Role_Power)

      |   字段   | 字段名称 | 类型 |    约束     | 备注 |
      | :------: | :------: | :--: | :---------: | :--: |
      |    ID    |    ID    | int  | PK not null |      |
      | Role_Id  |  角色ID  | int  | FK not null |      |
      | Power_Id |  权限ID  | int  | FK not null |      |



### 商品管理

#### 	1.采购管理

​		1. 请求方式：POST， GET， PUT， DELETE

​		2. 请求路径：http://127.0.0.1:8000/api/purchase/

​		3. 请求参数：

​		4. 响应结果：JSON

  5. 采购表(Purchase)

     |    字段     | 字段名称 |      类型      |    约束     |         备注          |
     | :---------: | :------: | :------------: | :---------: | :-------------------: |
     |     ID      |  采购ID  |      int       | PK not null |                       |
     |    name     | 商品名称 | Varchar（100） |  not null   |                       |
     |     num     |   数量   |      int       |  not null   |                       |
     |  in_price   |   价格   | decimal(10,2)  |  not null   |                       |
     |  buyer_id   | 采购员ID |      int       |  not null   |                       |
     |   status    |   状态   |    tinyint     |  not null   | 1. 未完成， 2. 已完成 |
     | create_time |   时间   |   timestamp    |  not null   |                       |

#### 2. 库存管理

 1. 请求方式：POST、GET、PUT、DELETE

 2. 请求路径：http://127.0.0.1:8000/api/repertory/

 3. 请求参数：

 4. 响应结果：JSON

 5. 库存表（Repertory）

    |     字段      | 字段名称 |      类型      |    约束     | 备注 |
    | :-----------: | :------: | :------------: | :---------: | :--: |
    |      ID       |  库存ID  |      int       | PK not null |      |
    |     name      | 商品名称 | Varchar（100） |  not null   |      |
    | repertory_num |   数量   |      int       |  not null   |      |
    |               |          |                |             |      |

    

### 订单模块

#### 	1. 订单管理

  1. 请求方式：POST、GET、PUT、DELETE

  2. 请求路径：http://127.0.0.1:8000/api/order/

  3. 请求参数：

  4. 响应结果：JSON

  5. 订单表(Order)

     | 字段 | 字段名称 | 类型 |    约束     | 备注 |
     | :--: | :------: | :--: | :---------: | :--: |
     |  ID  |  订单ID  | int  | PK not null |      |
     |      |          |      |             |      |
     |      |          |      |             |      |

     #### 2. 订单统计

      1. 请求方式：POST、GET、PUT、DELETE

      2. 请求路径：http://127.0.0.1:8000/api/ordersreceived/

      3. 请求参数：

      4. 响应结果： JSON

      5. 订单统计表（OrdersReceived)

         | 字段 |  字段名称  | 类型 |    约束     | 备注 |
         | :--: | :--------: | :--: | :---------: | :--: |
         |  ID  | 订单统计ID | INT  | PK not null |      |
         |      |            |      |             |      |
         |      |            |      |             |      |

         

#### 2. 退单统计

 1. 请求方式：POST、GET、PUT、DELETE

 2. 请求路径：http://127.0.0.1:8000/api/chargeback/

 3. 请求参数：

 4. 响应结果：JSON

 5. 退单表（Chargeback）

    | 字段 | 字段名称 | 类型 |    约束    | 备注 |
    | :--: | :------: | :--: | :--------: | :--: |
    |  ID  |  退单ID  | INT  | PK notnull |      |
    |      |          |      |            |      |
    |      |          |      |            |      |

### 客户模块

#### 	1. 客户管理

  1. 请求方式：POST、GET、PUT、DELETE

  2. 请求路径：http://127.0.0.1:8000/api/client/

  3. 请求参数：

  4. 响应结果：JSON

  5. 客户表（Client）

     |     字段     | 字段名称 |     类型      |    约束     | 备注 |
     | :----------: | :------: | :-----------: | :---------: | :--: |
     |      ID      |  客户ID  |      INT      | PK not null |      |
     | client_name  | 客户名称 | varchar（32） |  not null   |      |
     | client_phone | 手机号码 |      INT      |  not null   |      |

     

​		

### 报表模块

#### 	1. 订货相关

  1. 请求方式：POST、GET、PUT、DELETE

  2. 请求路径：http://127.0.0.1:8000/api/goods/

  3. 请求参数：

  4. 响应结果：JSON

  5. 订货相关表（Goods）

     | 字段 |  字段名称  | 类型 |    约束     | 备注 |
     | :--: | :--------: | :--: | :---------: | :--: |
     |  ID  | 订货相关ID | INT  | PK NOT NULL |      |
     |      |            |      |             |      |
     |      |            |      |             |      |

     

#### 2. 利润损耗

 1. 请求方式：POST、GET、PUT、DELETE

 2. 请求路径：http://127.0.0.1:8000/api/profit/

 3. 请求参数：

 4. 响应结果：JSON

 5. 利润损耗表（Profit）

    | 字段 | 字段名称 | 类型 |    约束     | 备注 |
    | :--: | :------: | :--: | :---------: | :--: |
    |  ID  | 利润损耗 | INT  | PK NOT NULL |      |
    |      |          |      |             |      |
    |      |          |      |             |      |

    

#### 3. 资金收款

 1. 请求方式：POST、GET、PUT、DELETE

 2. 请求路径：http://127.0.0.1:8000/api/capital/

 3. 请求参数：

 4. 响应结果：JSON

 5. 资金收款表（Capital）

    | 字段 |  字段名称  | 类型 |    约束     | 备注 |
    | :--: | :--------: | :--: | :---------: | :--: |
    |  ID  | 资金收款ID | INT  | PK NOT NULL |      |
    |      |            |      |             |      |
    |      |            |      |             |      |
    |      |            |      |             |      |

    

#### 4. 业绩核算

1. 请求方式：POST、GET、PUT、DELETE

2. 请求路径：http://127.0.0.1:8000/api/performance/

3. 请求参数：

4. 响应结果：JSON

5. 资金收款表（Performance）

   | 字段 |  字段名称  | 类型 |    约束     | 备注 |
   | :--: | :--------: | :--: | :---------: | :--: |
   |  ID  | 业绩核算ID | INT  | PK NOT NULL |      |
   |      |            |      |             |      |
   |      |            |      |             |      |

### 资金模块

#### 	1. 资金管理

1. 请求方式：POST、GET、PUT、DELETE

2. 请求路径：http://127.0.0.1:8000/api/funds/

3. 请求参数：

4. 响应结果：JSON

5. 资金收款表（FundsManagement）

   | 字段 |  字段名称  | 类型 |    约束     | 备注 |
   | :--: | :--------: | :--: | :---------: | :--: |
   |  ID  | 资金管理ID | INT  | PK NOT NULL |      |
   |      |            |      |             |      |
   |      |            |      |             |      |

   

#### 	2. 对账管理

  1. 请求方式：POST、GET、PUT、DELETE

  2. 请求路径：http://127.0.0.1:8000/api/checking/

  3. 请求参数：

  4. 响应结果：JSON

  5. 资金收款表（AccountChecking）

     | 字段 |  字段名称  | 类型 |    约束     | 备注 |
     | :--: | :--------: | :--: | :---------: | :--: |
     |  ID  | 对账管理ID | INT  | PK NOT NULL |      |
     |      |            |      |             |      |
     |      |            |      |             |      |

     

#### 	3. 资金统计

1. 请求方式：POST、GET、PUT、DELETE

2. 请求路径：http://127.0.0.1:8000/api/statistics/

3. 请求参数：

4. 响应结果：JSON

5. 资金收款表（FundsStatistics）

   | 字段 | 字段名称 | 类型 |    约束     | 备注 |
   | :--: | :------: | :--: | :---------: | :--: |
   |  ID  | 资金统计 | INT  | PK NOT NULL |      |
   |      |          |      |             |      |
   |      |          |      |             |      |

   













































