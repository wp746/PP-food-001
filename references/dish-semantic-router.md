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
background_semantic_direction
prop_semantic_direction
color_semantic_direction
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
- 真实热气
- 丰富但不过度戏剧化

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

- 深色餐饮空间
- 局部红 / 铜 / 暖金
- 火锅热气
- 饭局氛围

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

- 夜间摊位 / 街头暖灯
- 炭火反光
- 受控轻烟
- 更强环境层次

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
- 湿润石材 / 清透海洋冷调氛围
- 清透高光
- 禁止泛滥的“蓝色海洋背景”俗套

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

- 咖啡馆自然光
- 原木 / 水泥 / 现代店内背景
- 轻编辑感

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

- 保留货架 / 柜台语境
- 优化灯光、排列和主体分离
- 不把商品移到餐桌棚拍

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
background_semantic_direction: 高级川味鲜麻热汤餐饮环境
prop_semantic_direction: 青花椒/酸菜相关的克制辅助意象，不改变主菜
color_semantic_direction: 藤椒绿、酸菜黄绿、汤汁暖金、深灰/深木
lighting_character: 柔和定向主光 + 热汤背光 + 克制暖色环境光
photography_mode: CINEMATIC_EDITORIAL 或 DRAMATIC_FOOD_CAMPAIGN
```

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
