## 暗黑战神（DarkGod）（课程ID:1801）
>作者：Plane\
邮箱：1785275942@qq.com\
时间：  2018/12/09 05:34
### 第4章：数据库与服务器缓存层
#### 数据库环境配置
- 安装Wamp（拓展介绍Lamp）
- 安装Navicat for Mysql，并破解
- 讲解各个部分之间的关系

#### Navicat使用示例
- 讲解理念：简单直接，直达目的
- 数据库的概念及创建（字符集排序规则）
- 表的概念及创建
- 表的字段、类型、长度
- 主键概念，ID无符号自增

#### 数据库增删改查
- 引用C#的MySql.Data.dll
- 增：获取主键
- 删：指定id，用于转服等
- 改：cmd.Parameters.AddWithValue("name","Plane最帅")
    - 修改使用更方便
    - 更安全，可防止Sql注入
- 查：
    - 解析查找到的数据，while(true)遍历集合

#### 增加数据库管理器
- 创建darkgod数据库、account表
- 增加缓存层DBMgr.cs
- 在ServerRoot中调用
- 初始化连接

#### 查询玩家数据
- 使用try...catch...捕获异常
- 解析数据部分代码
```
    MySqlCommand cmd = new MySqlCommand("select * from account where acct = @acct", conn);
    cmd.Parameters.AddWithValue("acct", acct);
    reader = cmd.ExecuteReader();
            
    id = reader.GetInt32("id"),
    name = reader.GetString("name"),
    lv = reader.GetInt32("level"),
    exp = reader.GetInt32("exp"),
    power = reader.GetInt32("power"),
    coin = reader.GetInt32("coin"),
    diamond = reader.GetInt32("diamond")
```
#### 插入默认玩家数据
- 讲解reader关闭，并演示易出错情况
- 创建新账号部分代码
```
"insert into account set acct=@acct,pass =@pass,name=@name,level=@level,exp=@exp,power=@power,coin=@coin,diamond=@diamond"
```
```
    cmd.Parameters.AddWithValue("acct", acct);
    cmd.Parameters.AddWithValue("pass", pass);
    cmd.Parameters.AddWithValue("name", pd.name);
    cmd.Parameters.AddWithValue("level", pd.lv);
    cmd.Parameters.AddWithValue("exp", pd.exp);
    cmd.Parameters.AddWithValue("power", pd.power);
    cmd.Parameters.AddWithValue("coin", pd.coin);
    cmd.Parameters.AddWithValue("diamond", pd.diamond);
```

#### 更新玩家数据
- 定制重命名协议，并发送网络消息
- 服务器转发到LoginSys.cs处理
```
    //名字是否已经存在 
    MySqlCommand cmd = new MySqlCommand("select * from account where name= @name", conn);
    cmd.Parameters.AddWithValue("name", name);
    reader = cmd.ExecuteReader();
    if (reader.Read()) {
        exist = true;
    }
    
    //更新玩家数据
    MySqlCommand cmd = new MySqlCommand(
    "update account set name=@name,level=@level,exp=@exp,power=@power,coin=@coin,diamond=@diamond where id =@id", conn);
    cmd.Parameters.AddWithValue("id", id);
    cmd.Parameters.AddWithValue("name", playerData.name);
    cmd.Parameters.AddWithValue("level", playerData.lv);
    cmd.Parameters.AddWithValue("exp", playerData.exp);
    cmd.Parameters.AddWithValue("power", playerData.power);
    cmd.Parameters.AddWithValue("coin", playerData.coin);
    cmd.Parameters.AddWithValue("diamond", playerData.diamond);

    //TOADD Others
    cmd.ExecuteNonQuery();
```
- 客户端更新数据
- 客户端错误码处理技巧（考滤非技术因素）
#### 总结梳理
- 讲解代码完整的运行过程
