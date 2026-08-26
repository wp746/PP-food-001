# Dish Semantic Router

本文件负责在高保真主体锁定完成之后，为背景、环境、色彩、道具和摄影气质选择**菜品语义方向**。

核心原则：

> **Preserve the food physically. Design the environment semantically.**
>
> 主体在物理上高保真，环境在语义上与菜品强关联。

## 1. 信息优先级

按以下优先级使用菜品信息：

1. 用户明确提供的菜名 / 菜系 / 风味 / 卖点
2. 用户提供的其他描述性信息
3. 从源图中自动推断的菜品语义
4. 通用食品类别信息
5. 最后才允许使用保守的通用商业摄影方向

用户明确提供的信息永远优先于自动猜测。

如果用户说“这是青花椒酸菜鱼”，不得因为视觉模型更像“藤椒鱼”而覆盖用户提供的菜名。

## 2. 需要内部提取的字段

如果用户提供则直接使用；缺失时才自动推断：

```text
dish_name
dish_alias
dish_name_source = user | inferred
dish_confidence
cuisine_type
flavor_profile
primary_ingredients
secondary_ingredients
cooking_method
temperature_state
dish_mood_keywords
semantic_route
material_stage_direction
background_semantic_direction
prop_semantic_direction
color_semantic_direction
appetite_rendering_direction
lighting_character
photography_mode
```

## 3. 菜名缺失时的推断规则

菜名推断只用于选择更合适的摄影环境，**不得用于重做食物**。

### 高置信度：confidence >= 0.85

可以采用较明确的菜品级语义路线。

例如：

- 明显的青花椒、鱼片、酸菜、清黄热汤 -> 可判断为青花椒酸菜鱼 / 藤椒酸菜鱼方向
- 明显的红油、辣椒、鱼片 -> 可进入川味红油鱼类方向

### 中置信度：0.60 <= confidence < 0.85

只采用“品类级”语义背景，不把猜测当事实。

例如：

- hot fish soup
- Sichuan-style fresh-pepper fish
- Chinese spicy soup dish

### 低置信度：confidence < 0.60

采用保守的品类级商业摄影环境。

不要为了背景创意而硬猜具体菜名、地域或菜系。

## 4. 主要语义路线

以下是基础路由，不是穷举清单。遇到其他菜品时按相同逻辑推导。

### SICHUAN_FRESH_PEPPER

典型：

- 青花椒酸菜鱼
- 藤椒鱼
- 青花椒鸡
- 青花椒牛蛙
- 鲜麻类川味热菜

语义：

- 鲜麻
- 青花椒香
- 酸香 / 清辣
- 开胃
- 热汤
- 川渝
- 精致中带一点江湖气

视觉方向：

- 藤椒绿 / 花椒绿
- 酸菜黄绿
- 汤汁暖金
- 深灰 / 黑石 / 克制深木
- 少量暖铜色环境光

食欲信号：汤面镜面反光、花椒油珠悬浮、鱼片边缘微卷水润、酸菜爽脆。

不要把它简单做成红油川菜。

### SICHUAN_SPICY_RED

典型：

- 水煮鱼
- 毛血旺
- 冒菜
- 红油麻辣类

语义：

- 麻辣
- 红油
- 浓烈
- 热烈
- 高刺激

视觉方向：

- 辣椒红
- 深红油
- 暖黑
- 少量金色高光
- 更强但受控的热气与反差

食欲信号：红油镜面透亮发光、辣椒段油润饱满、肉片油亮挂汁。

### CANTONESE_LIGHT_FRESH

典型：

- 清蒸鱼
- 白切鸡
- 粤式煲汤
- 清鲜海鲜

语义：

- 清鲜
- 细腻
- 克制
- 高级
- 通透

视觉方向：

- 明亮柔和
- 中性白
- 淡绿
- 浅木 / 石材
- 干净高级浅石材质舞台

食欲信号：豉油汁水清亮挂身、鱼肉湿润反光、葱丝挺立、汤体清透。

### NORTHERN_HEARTY_STAPLE

典型：

- 牛肉面
- 汤面
- 饺子
- 烩面
- 传统主食

语义：

- 温暖
- 扎实
- 饱腹
- 烟火气

视觉方向：

- 自然木 / 石面
- 暖环境光
- 真实热气（克制）
- 丰富但不过度戏剧化

食欲信号：面条油润挂汁、汤面浮油光、配菜挺立水灵。

### JIANGHU_HOTPOT

典型：

- 火锅
- 串串
- 干锅
- 江湖菜

语义：

- 热烈
- 聚餐
- 江湖感
- 锅气
- 香辣

视觉方向：

- 深色哑光石材舞台 + 铸铁/粗陶/黄铜材质
- 局部红 / 铜 / 暖金
- 火锅热气
- 暖金 bokeh 纵深

食欲信号：锅底沸点微泡、食材油亮、毛肚黄喉水润挺括、麻酱挂壁。

### STREET_BBQ_SMOKY

典型：

- 烧烤
- 烤串
- 铁板
- 夜市小吃

语义：

- 烟火气
- 夜色
- 炭火
- 街头

视觉方向：

- 炭色铸铁 + 粗粝石板哑光舞台
- 暖灯 bokeh 远景
- 炭火反光
- 受控轻烟
- 更强环境层次

食欲信号：焦糖化边缘油亮、孜然辣椒面微距可见、油滴微滴反光。

### JAPANESE_MINIMAL_FRESH

典型：

- 寿司
- 刺身
- 日式定食

语义：

- 极简
- 清洁
- 冷静
- 精致

视觉方向：

- 原木
- 石材
- 低干扰背景
- 克制留白
- 清晰材质

食欲信号：刺身半透明质感、鱼肉湿润反光、醋米颗粒分明油亮。

### SEAFOOD_CLEAN_REFINED

典型：

- 清鲜鱼类
- 贝类
- 海鲜拼盘

语义：

- 鲜
- 清爽
- 水润
- 高级

视觉方向：

- 干净冷暖平衡
- 湿润石材 / 清透冷调材质舞台
- 清透高光
- 禁止泛滥的"蓝色海洋背景"俗套

食欲信号：表面湿润水光、柠檬水珠、冰镇冷凝水、贝类汁水。

### DESSERT_SOFT_ELEGANT

典型：

- 蛋糕
- 慕斯
- 甜品

语义：

- 柔和
- 精致
- 甜感
- 轻盈

视觉方向：

- 奶白 / 柔粉 / 食材本身颜色
- 柔光
- 奶油白大理石 / 柔和织物高级舞台

食欲信号：奶油缎面光泽、慕斯镜面、水果水珠、切面层次湿润。

### COFFEE_BAKERY_LIFESTYLE

典型：

- 咖啡
- 烘焙
- 面包
- 手持咖啡

语义：

- Lifestyle
- 松弛
- 日常高级感
- 香气

视觉方向：

- 柔和高显色自然光感
- 原木 / 水泥灰 / 现代材质舞台
- 轻编辑感

食欲信号：奶泡缎面光泽、crema 琥珀反光、面包脆壳光泽与内瓤湿润。

### RETAIL_PACKAGED_COMMERCIAL

典型：

- 超市包装食品
- 便利店饮料
- 货架商品

语义：

- 产品清晰
- 零售
- 商业陈列

视觉方向：

- 保留源图货架 / 柜台语境（特殊品类，见 scene-modules.md RETAIL_SHELF）
- 优化灯光、排列和主体分离
- 不把商品移到餐桌棚拍

食欲信号：包装印刷质感锐利、光泽分区控制、产品排列新鲜有序。

## 5. Photography Mode 语义选择

优先在以下三种中选择：

### NATURAL_EDITORIAL

适用于清鲜、轻食、粤菜、日料、甜点、烘焙、咖啡等需要自然、明亮、通透的主题。

### CINEMATIC_EDITORIAL

默认选择。适用于大部分中餐、主食、家常热菜和高端堂食。

### DRAMATIC_FOOD_CAMPAIGN

适用于火锅、烧烤、红油麻辣、夜市、强刺激川味热菜等确实需要更强氛围的主题。

**Cinematic 不等于暗、黄、烟。**

## 6. 语义路由输出模板

内部生成类似：

```text
dish_name: 青花椒酸菜鱼
dish_name_source: user
cuisine_type: 川味
flavor_profile: 鲜麻、酸香、开胃、热汤
primary_ingredients: 鱼片、酸菜、青花椒、青椒、热汤
semantic_route: SICHUAN_FRESH_PEPPER
dish_mood_keywords: 鲜麻、清辣、热气、川味、精致中带江湖感
material_stage_direction: 深灰哑光石板台面 + 深釉粗陶 + 克制黄铜，远景暖深暗部 bokeh
background_semantic_direction: 高级川味鲜麻热汤材质舞台（无场所结构）
prop_semantic_direction: 青花椒枝、酸菜陶罐、小料碟（盘外、虚化、从属）
color_semantic_direction: 藤椒绿、酸菜黄绿、汤汁暖金、深灰/深木
appetite_rendering_direction: 热汤面镜面反光、花椒油珠悬浮、鱼片边缘微卷水润、酸菜爽脆有汁感
lighting_character: 柔和定向主光 + 热汤背光 + 克制暖色环境光
photography_mode: CINEMATIC_EDITORIAL 或 DRAMATIC_FOOD_CAMPAIGN
```

字段取值来源：`material_stage_direction` / `appetite_rendering_direction` / `prop_semantic_direction` 优先从 `cuisine-style-map.md` 对应品类条目取材，再按源图属性裁剪（剔除源图不存在的属性）。

## 7. 最终原则

语义信息决定的是：

- 背景
- 环境
- 辅助道具
- 色彩方向
- 摄影情绪
- 灯光个性

语义信息**不得**成为：

- 添加菜品食材
- 删除源图食材
- 重做摆盘
- 改器皿
- 改鱼片 / 肉类 / 面条形态

的理由。
