# 使用Corpse Complex自定义死亡附加效果

## 前言

Corpse Complex 配置文件全翻译解析讲解 + 官方 Wiki 注释翻译.

使用模组：[Corpse Complex](https://www.curseforge.com/minecraft/mc-mods/corpse-complex)\(CurseForge Link\)


## 安装，初始化

Corpse Complex, 很简单很好用的死亡系统修改模组.

对, 没啥教程, 所以我摸了一个出来.

安装 Corpse Complex, 启动游戏, 可见 `config/corpsecomplex.cfg`.

Corpse Complex 有很多模组兼容, 但本页面不会列出除 `Baubles` 外的支持, 请自行举一反三.

如需更详细的 (或官方的) 解释, 请查询 [Corpse Complex GitHub Wiki](https://github.com/TheIllusiveC4/CorpseComplex/wiki/)\(GitHub Link\). (英语)

## 配置文件翻译解读

所有末尾加了句号的是我加的注释.

所有被进一步解读的原句末尾不会有句号.

```yaml
# 配置文件

##########################################################################################################
# 效果
#--------------------------------------------------------------------------------------------------------#
# 添加会在玩家重生后获得的药水效果
##########################################################################################################

effects {
    # 设置为 true 启用效果模块
    B:"Enable Effects Module"=true

    # 列出玩家重生后获得的,可以被使用 "Curative Items" 列表中物品消除的药水效果
    # 格式: [效果注册名] [时长 (秒)] [效果等级]
    # 最大值为 1600 秒, 10 级. "Uncurable Respawn Effects" 同理.
    S:"Curable Respawn Effects" <
     >

    # 使用后可以消除 "Curable Respawn Effects" 列表中效果的物品
    # 默认是牛奶, 可以添加别的, 直接写 string ID 即可.
    S:"Curative Items" <
        minecraft:milk_bucket
     >

    # 列出玩家重生后获得的的药水效果
    # 换句话说, 加载这个列表里的效果是无法被使用 "Curative Items" 列表中物品消除的.
    # 此处默认配置代表获得 30s 的等级为 4 的挖掘疲劳.
    # 格式: [效果注册名] [时长 (秒)] [效果等级]
    S:"Uncurable Respawn Effects" <
        minecraft:mining_fatigue 30 4
     >

    ##########################################################################################################
    # 自定义重生效果
    #--------------------------------------------------------------------------------------------------------#
    # 自定义重生效果以修改玩家的属性
    ##########################################################################################################

    "custom respawn effect" {
        # 设置为 true 启用自定义重生效果模块
        B:"Enable Custom Respawn Effect"=false

        # 设置效果时长 (秒)
        # 下面所有的 modifier 都基于此时间值, 也就是下面所有的 modifier 都会在此时段结束后回到默认值.
        I:Duration=0

        # 使用后可以消除中效果的物品
        # 默认是牛奶, 可以添加别的, 直接写 string ID 即可.
        S:"Curative Items" <
            minecraft:milk_bucket
         >

        # 设置为 true 启用渐渐恢复 (修改器将会随时间逐渐减弱)
        # 也就是以下所有的 modifier 都会随着时间恢复到默认值.
        B:"Gradual Recovery"=false

        # 设置最大生命值修改
        # 在 -1024 ~ 1024 之间.
        # 除非有其他模组或不可抗力的影响, 设置过低会导致玩家陷入无限死亡/重生的死循环.
        D:"Maximum Health Modifier"=0.0

        # 设置护甲值修改
        # 玩家的总护甲值不能低于 0 .
        D:"Armor Modifier"=0.0

        # 设置护甲硬度值修改
        # 在 -20 ~ 20 之间.
        D:"Armor Toughness Modifier"=0.0

        # 设置攻击值修改
        # 在 -2048 ~ 2048 之间.
        D:"Attack Damage Modifier"=0.0

        # 设置攻击速度值修改
        # 在 -1.0 ~ 1.0 之间.
        # -1.0 就是无法攻击, 1.0 则是两倍攻击速度.
        D:"Attack Speed Percent Modifier"=0.0

        # 设置移动速度值修改
        # 在 -1.0 ~ 1.0 之间.
        # -1.0 就是无法移动, 1.0 则是两倍移速.
        D:"Movement Speed Percent Modifier"=0.0

        # 设置为 true 启用当自定义重生效果生效时不能吃食物
        # 对所有 extend 了原版 ItemFood 类的物品都有效, 此外还包括原版和 Pam's Harvestcraft 的蛋糕.
        B:"Cannot Eat Food"=false

        # 设置为 true 启用当自定义重生效果生效时不能获得经验
        # 经验球仍会被玩家吸引, 但玩家无法拾取它们也无法从它们获取经验.
        B:"Cannot Gain XP"=false
    }

}


##########################################################################################################
# 经验
#--------------------------------------------------------------------------------------------------------#
# 自定义死亡丢失经验
##########################################################################################################

experience {
    # 设置为 true 启用经验模块
    B:"Enable Experience Module"=false

    # 设置为 true 启用死亡后保存所有经验
    # 同样的, 不会掉落任何经验球.
    B:"Keep All XP"=false

    # 死亡后丢失的经验数
    D:"Lost XP Percent"=1.0

    # 死亡后可以保存的最大经验值, 设置为 0 禁用.
    # 也就是死后最多可以剩下多少经验, 多余的都会被清除.
    # 比如设置为 5, 死前有 10, 那重生后只剩5, 但如果只有 3, 就仍保留 3.
    I:"Maximum Recoverable XP"=0

    # 死亡后可以保存的最大经验值百分比
    # 基本同上, 就是变成了可以保留原有经验的百分之多少, 与 "Maximum Recoverable XP" 不冲突, 看最后谁少就听谁的.
    D:"Recoverable XP Percent"=0.20000000298023224
}


##########################################################################################################
# 饥饿
#--------------------------------------------------------------------------------------------------------#
# 自定义重生后的饥饿值和饱食度
##########################################################################################################

hunger {
    # 设置为 true 启用饥饿模块
    B:"Enable Hunger Module"=false

    # 设置为 true 启用死亡后延续原饥饿值
    B:"Keep Food Level"=false

    # 设置为 true 启用死亡后延续原饱食度
    B:"Keep Saturation"=false

    # 重生后可获得的最少饥饿值
    # 0 ~ 20 之间.
    # 如没有启用 "Keep Food Level", 此选项和下一个选项都无效.
    I:"Minimum Food Level"=6

    # 重生后可获得的最大饥饿值
    # "Minimum Food Level" ~ 20 之间.
    # 不能低于, 但可以等于 "Minimum Food Level".
    I:"Maximum Food Level"=20
}


##########################################################################################################
# 物品栏
#--------------------------------------------------------------------------------------------------------#
# 自定义死亡后和重生后如何处理物品栏
##########################################################################################################

inventory {
    # 设置为 true 启用物品栏模块
    B:"Enable Inventory Module"=false

    # 设置为 true 启用死亡后保存装甲
    # 仅限穿着的.
    B:"Keep Armor"=false

    # 设置为 true 启用死亡后保存非主手快捷栏物品
    # 不 包 括 主 手 物 品.
    B:"Keep Hotbar"=false

    # 设置为 true 启用死亡后保存主手物品
    B:"Keep Mainhand"=false

    # 设置为 true 启用死亡后保存副手物品
    B:"Keep Offhand"=false

    # 设置为 true 启用死亡后保存主物品栏物品 (非装备和快捷栏)
    # 这所有的 "Keep xxx" 都不互相冲突, 可以同时开启, 自己琢磨关系吧.
    B:"Keep Main Inventory"=false

    # 死亡后, 扣除掉落物多少百分比的耐久
    D:"Durability Loss on Drops"=0.0

    # 设置为 true 启用扣除掉落物耐久取决于世界难度
    # 启用后, 所有的 "Durability Loss on Easy/Normal/Hard" 才会生效.
    B:"Durability Loss Dependent on Difficulty"=false

    # 死亡后, 在简单难度下扣除掉落物多少百分比的耐久
    D:"Durability Loss on Drops on Easy"=0.0

    # 死亡后, 在普通难度下扣除掉落物多少百分比的耐久
    D:"Durability Loss on Drops on Normal"=0.0

    # 死亡后, 在困难难度下扣除掉落物多少百分比的耐久
    D:"Durability Loss on Drops Hard"=0.0

    # 死亡后, 扣除被保存物品多少百分比的耐久
    D:"Durability Loss on Kept Items"=0.0

    # 设置为 true 启用启用被保存物品耐久取决于世界难度
    # 启用后, 所有的 "Durability Loss on Kept Items on Easy/Normal/Hard" 才会生效.
    B:"Kept Durability Loss Dependent on Difficulty"=false

    # 死亡后, 在简单难度下扣除被保存物品多少百分比的耐久
    D:"Durability Loss on Kept Items on Easy"=0.0

    # 死亡后, 在普通难度下扣除被保存物品多少百分比的耐久
    D:"Durability Loss on Kept Items on Normal"=0.0

    # 死亡后, 在困难难度下扣除被保存物品多少百分比的耐久
    D:"Durability Loss on Kept Items Hard"=0.0

    # 设置耐久丢失限制, 使得不会有工具因为死亡而破损
    B:"Limit Durability Loss"=false

    # 死亡后, 扣除掉落物多少百分比的能量
    # 也就是电.
    # 为什么没有难度选项? 不知道, 就是没有.
    D:"Energy Drain on Drops"=0.0

    # 死亡后, 扣除被保存物品多少百分比的能量
    D:"Energy Drain on Kept Items"=0.0

    # 被该本保存的物品仍会掉落的概率
    D:"Random Drop Chance"=0.0

    # 设置为 true 启用仅在主物品栏上应用 "Random Drop Chance"
    B:"Random Drop Only Main Inventory"=false

    # 掉落物会直接消失的概率
    D:"Random Destroy Chance"=0.0

    # 总会被保存的物品列表
    # 对, 还是 string ID.
    S:"Essential Items" <
     >

    # 总会掉落的物品列表
    # 对, 还是 string ID.
    # 此列表和 "Essential Items" 的优先级高于两者以上的所有设置.
    S:"Cursed Items" <
     >

    # 设置为 true 启用 "Cursed Items" 在掉落时直接消失
    B:"Destroy Cursed Items"=false

    # 掉落物被清除的时间 (秒), 设置为 -1 应用原版设置
    I:"Drop Despawn Timer"=-1

    # 设置为 true 启用死亡保存饰品栏物品
    B:"Keep Baubles"=false

    # 设置为 true 启用死亡掉落物不会被清除
    B:"No Drop Despawn"=false

    ##########################################################################################################
    # 灵魂绑定
    #--------------------------------------------------------------------------------------------------------#
    # 启用并自定义灵魂绑定附魔
    ##########################################################################################################

    soulbinding {
        # 设置为 true 启用灵魂绑定附魔
        B:"Enable Soulbinding Enchantment"=false

        # 附魔最大等级
        # 1 ~ 5, 如设置为 1 则不会显示等级.
        I:"Max Level"=1

        # 物品被保留时, 扣除多少附魔等级
        # 0.0 ~ 1.0 之间.
        # 如果物品仅有 1 级附魔, 扣除时会直接移除附魔.
        D:"Chance to Drop Level on Saved Item"=0.0

        # 物品会无视灵魂绑定附魔等级被保存的概率
        D:"Base Save Probability"=1.0

        # 附魔等级每高一级, 增加多少物品被保存的概率
        D:"Extra Save Probability per Level"=0.0

        # 设置为 true 允许灵魂绑定附魔出现在附魔台选项中
        # 如果没启用, 那就只能找战利品.
        B:"Can Apply at Enchanting Table"=true

        # 设置为 true 允许灵魂绑定附魔被附在书上
        B:"Allowed on Books"=true

        # 附魔的稀有等级 (COMMON, UNCOMMON, RARE, 或 VERY_RARE)
        # 会影响附魔经验消耗和战利品生成概率等, 原版机制.
        S:Rarity=VERY_RARE
    }

}


##########################################################################################################
# 重生
#--------------------------------------------------------------------------------------------------------#
# 自定义通用重生规则
##########################################################################################################

respawning {
    # 设置为 true 启用重生模块
    B:"Enable Respawning Module"=false

    # 设置为 true 禁用床设置重生点
    # 启用此项后, 从技术层面上来讲玩家仍然可以通过床设置重生点, 但这个重生点会在玩家死亡前被删除.
    B:"Disable Bed Spawn Points"=false

    # 设置为 true 启用一个可合成的, 使用后会将玩家传送回死亡地点的卷轴
    # 玩家每次复活后只能使用一次卷轴, 但可以持有多个卷轴.
    B:"Return Scroll"=false

    # 如果启用了 "Return Scroll", 设置为 true 将在玩家每次重生后给予玩家一个卷轴
    B:"Give Scroll on Respawn"=false

    # 一个在玩家重生后给予玩家物品的列表. 格式为 modid:item_name;stacksize;metadata
    # 举个例子, enderio:block_electric_light;16;1 就是 16 个 EIO 反向电灯. 别问我为什么用这举例子, 随手拿的.
    S:"Respawn Items" <
     >

    # 在死亡地点生成怪物
    # Entity ID.
    S:"Spawn Mobs on Death" <
     >
}
```

## Corpse Complex 兼容的模组列表

### 物品栏支持
* Baubles by Azanor
* Wearable Backpacks by copygirl
* Cosmetic Armor Reworked by ZLainSama
* Overpowered Inventory by Lothrazar
* RPG Inventory by Subaraki
* Thut Wearables by Thutmose
* Advanced Inventory by CubeX2

### 状态支持
* Tough as Nails by Glitchfiend, Adubbz, and Forstride

### 食物支持
* Cakes from Pam's Harvestcraft by MatrexsVigil

### 其他支持
* Corail Tombstone by Corail31 (注: Corail Tombstone 的经验模块与 Corpse Complex 冲突, 同时安装两者时 Corpse Complex 的经验模块会禁用.)
* GraveStone Mod by EuhDawson
* Gravestone mod - Graves by NightKosh
* Tomb Many Graves 2 by M4thG33k

