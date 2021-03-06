# 使用Large Ore Deposits生成自定义矿脉

## 前言

自定义矿脉，入门，以我的方式

使用模组：[Large Ore Deposits](https://www.curseforge.com/minecraft/mc-mods/large-ore-deposits)\(CurseForge Link\)

## 第一步:安装，初始化

Large Ore Deposits\(下文简称lods\)算是比较强大的矿物生成控制模组了，使用也很简单。

首先安装lods，启动游戏，`config`下即会生成`adlods`文件夹，打开就会发现其中有三部分：

`Deposits`文件夹，`VanillaGen`文件夹和`adlods.cfg`。

其中`adlods.cfg`毫无卵用，跳过

`VanillaGen`和`Deposits`文件夹中都有多个cfg文件，每个都对应了一种"矿物"，`VanillaGen`文件夹中的文件均为摆设空壳子，相对于`Deposits`文件夹中真正的矿脉来说功能残疾。`Deposits`文件夹中有着功能健全的模板，这里以`coal.cfg`为例来一项一项解读：

顺带一提，所有的`minecraft:`命名空间都不必写，也就是说`stone:*`实为`minecraft:stone:*`

```yaml
# 配置文件

Config {
    # 如将此项设置为false，则此文件中的所有变量将不会被使用。 [默认: true]
    B:enabled=true
}


Deposit {
    # 定义此矿脉中的矿物和它们的权重等级
    # 格式: 方块ID/矿辞 [, 权重]
    # 当定义为矿辞时，自动选取此矿辞中的第一项
    # 例如(矿物ID, 不推荐这样写):
    #      minecraft:coal_ore
    #      minecraft:gold_ore, 2
    #      minecraft:iron_ore, 5
    #  或(矿辞, 推荐这样写):
    #      oreCoal
    #      oreGold, 2
    #      oreIron, 5
    #  意味着煤矿，金矿，铁矿会以1:2:5的比例在此矿脉中生成
    S:ores <
        oreCoal
     >

    # 定义矿脉稀有度(单位: 区块)
    # 数值越高，矿脉越稀有
    # 例如设置为1000，即为1000个区块中会生成1个矿脉
    # 即每个区块有1 / 1000 * 100% = 0.1%的几率生成此矿脉 [范围: 1 ~ 256000]
    I:rarity=800

    # 定义矿物生成时会替换什么方块
    # 支持*通配符  [默认: [stone:*]]
    S:replaceableBlocks <
        stone:*
     >

    ##########################################################################################################
    # 高度
    #--------------------------------------------------------------------------------------------------------#
    # 定义生成此矿脉的高度限制
    ##########################################################################################################

    Altitude {
        # 最高高度 [范围: 0 ~ 255, 默认: 80]
        I:max=80

        # 最低高度 [范围: 0 ~ 255, 默认: 32]
        I:min=32
    }

    ##########################################################################################################
    # 大小
    #--------------------------------------------------------------------------------------------------------#
    # 定义生成此矿脉的大小(单位: 块)
    ##########################################################################################################

    Size {
        # 最大量 [范围: 1 ~ 8000, 默认: 1800]
        I:max=1800

        # 最低量 [范围: 1 ~ 8000, 默认: 900]
        I:min=900
    }

    ##########################################################################################################
    # 维度
    #--------------------------------------------------------------------------------------------------------#
    # 定义此矿脉会生成的维度
    # 通过维度ID定义维度 [-1 - 地狱, 0 - 主世界, 1 - 末地, 等等]
    # 一行一个ID，不要添加分隔符
    # 如:
    #    -1
    #    0
    #    1
    # 如果设置了白名单，黑名单会被忽略
    ##########################################################################################################

    Dimensions {
        #  [默认: ]
        S:blackList <
         >

        #  [默认: ]
        S:whiteList <
         >
    }

    ##########################################################################################################
    # 生物群系
    #--------------------------------------------------------------------------------------------------------#
    # 定义此矿脉会生成的生物群系1
    # 可以通过数字ID或群系名称(区分大小写)定义生物群系
    # 一行一个ID，不要添加分隔符
    # 如:
    #    -114
    #    514
    #    aBiomeID
    # 如果设置了白名单，黑名单会被忽略
    ##########################################################################################################

    Biomes {
        #  [默认: ]
        S:blackList <
         >

        #  [默认: ]
        S:whiteList <
         >
    }

    ##########################################################################################################
    # 指示物
    #--------------------------------------------------------------------------------------------------------#
    # 定义此矿脉的地表指示物(比如一圈稀有的花之类的，或ContentTweaker自带的oreSample之类的东西)
    ##########################################################################################################

    Indicator {
        # 定义每圈的指示物和圈的大小
        # 格式: 指示物ID [, 圈的大小]
        # 排列顺序是从小到大从里到外排出去的
        # 圈大小相同的指示物会被随机选取
        # 如果没有定义圈大小，则从1开始自动选择最小的可行圈数
        # 例如:
        #      minecraft:cornflower, 2
        #      minecraft:orange_tulip, 4
        # 如需添加NBT，就这样:
        #      namespace:blockid:[nbt], radius
        S:circles <
            silentgems:glowrose:[gem=onyx], 3
            mysticFlowerBlack, 3
            double_plant:3, 3
            silentgems:glowrose:[gem=onyx], 6
            mysticFlowerBlack, 6
            double_plant:3, 6
         >

        # 定义显示指示物形状连续性的程度 [范围: 0.0 ~ 100.0, 默认: 60.0]
        S:=60.
        # 定义指示物替换时的最大值 [范围: 0 ~ 16, 默认: 1]
        I:distortion=1

        # 定义单方块指示物的ID [默认: ]
        S:id=
    }

}



```

基本就是这样了，复制一份模板，根据自己的需要修改数值后输入`/lods reload`指令重载配置即可，矿脉就会正常生成了，simple as that

值得一提的是，此模组还提供了几个调试用指令，如`/lods gen <deposit>`即可生成一个对应矿脉，并将其基本信息打印在聊天框。以及`/lods test <deposit> <amount>`在自己当前位置生成一个对应大小的对应矿脉。而`/lods strip chunk/around`则可以清除所在/3x3区块内所有不是矿物的方块。`/lods dress chunk/around/all`则相反，将当前区块/3x3区块内/全世界范围内被strip的方块复原
