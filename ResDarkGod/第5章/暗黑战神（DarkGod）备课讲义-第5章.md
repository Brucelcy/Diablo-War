## 暗黑战神（DarkGod）（课程ID:1801）
>作者：Plane\
邮箱：1785275942@qq.com\
时间：  2018/12/11 01:34
### 第5章：主城UI逻辑与人物控制
#### 主城场景制作
- 导入资源
- 导入灯光，并设置Lighting

#### 制作主城界面UI

#### 跳转主城逻辑

#### 增加角色属性
- 更改数据库account表
- 修改PlayerData类
```
    public int hp;
    public int ad;
    public int ap;
    public int addef;
    public int apdef;
    public int dodge;//闪避概率
    public int pierce;//穿透比率
    public int critical;//暴击概率
```
- 修改DBMgr.cs
```
    // QueryPlayerData()
    hp = reader.GetInt32("hp"),
    ad = reader.GetInt32("ad"),
    ap = reader.GetInt32("ap"),
    addef = reader.GetInt32("addef"),
    apdef = reader.GetInt32("apdef"),
    dodge = reader.GetInt32("dodge"),
    pierce = reader.GetInt32("pierce"),
    critical = reader.GetInt32("critical")
    
    //默认账号数据
    hp = 2000,
    ad = 275,
    ap = 265,
    addef = 67,
    apdef = 43,
    dodge = 7,
    pierce = 5,
    critical = 2,
    
    //InsertNewAcctData()sql增加：
    "hp=@hp,ad=@ad,ap=@ap,addef=@addef,apdef=@apdef,dodge=@dodge,pierce=@pierce,critical=@critical"
    
    //InsertNewAcctData()参数增加：
    cmd.Parameters.AddWithValue("hp", pd.hp);
    cmd.Parameters.AddWithValue("ad", pd.ad);
    cmd.Parameters.AddWithValue("ap", pd.ap);
    cmd.Parameters.AddWithValue("addef", pd.addef);
    cmd.Parameters.AddWithValue("apdef", pd.apdef);
    cmd.Parameters.AddWithValue("dodge", pd.dodge);
    cmd.Parameters.AddWithValue("pierce", pd.pierce);
    cmd.Parameters.AddWithValue("critical", pd.critical);
    
    //UpdatPlayerData()sql增加：
    "hp=@hp,ad=@ad,ap=@ap,addef=@addef,apdef=@apdef,dodge=@dodge,pierce=@pierce,critical=@critical"
    
    //UpdatPlayerData()参数增加：
    
    cmd.Parameters.AddWithValue("apdef", playerData.apdef);
    cmd.Parameters.AddWithValue("dodge", playerData.dodge);
    cmd.Parameters.AddWithValue("pierce", playerData.pierce);
    cmd.Parameters.AddWithValue("critical", playerData.critical);
```

#### 主城UI显示控制
- 通用战力计算函数
- 通用体力限制计算函数
- 通用升级经验计算函数

#### 分段经验条屏幕适配
- 动态计算指定

#### 摇杆插件制作
- 制作目标与思路分析
- 封装UI触控工具脚本PEListener
- 调用脚本完成一个示例
- 封装到WindowRoot，成为通用工具
- 完成逻辑开发，输出测试数据
- 
#### 角色相关
- 角色资源整理导入
- 运动控制器的使用（动画显示控制）
- 添加角色控制器（位置移动控制）
- 创建单独的测试场景实现运动控制
- 添加PlayerController控制运动
- 动作混合控制

#### 主城场景角色初始化
- 主城配置文件生成与解析
- 控制器初始化
- 对接方向传递代码