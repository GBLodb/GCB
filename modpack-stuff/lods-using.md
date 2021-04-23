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

```text
# 配置文件

Config {
    # 如将此项设置为false，则此文件中的所有变量将不会被使用。 [默认: true]
    B:enabled=true
}


Deposit {
    # 定义此矿脉中的矿物和它们的权重等级
    # 格式: 方块ID/矿辞 [, 权重]
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
    # 即 1 / 1000 * 100% = 0.1% [范围: 1 ~ 256000]
    I:rarity=800

    # 定义矿物生成时会替换什么方块。 [默认: [stone:*]]
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
    # Dimensions
    #--------------------------------------------------------------------------------------------------------#
    # Defines the dimensions which this deposit can be generated in.
    # Dimension is specified by its ID [-1 - Nether, 0 - Overworld, 1 - The End, etc.]
    # Each ID must be on a separate line without any delimiters.
    # If the whitelist is set, the blacklist will be ignored.
    ##########################################################################################################

    Dimensions {
        #  [default: ]
        S:blackList <
         >

        #  [default: ]
        S:whiteList <
         >
    }

    ##########################################################################################################
    # Biomes
    #--------------------------------------------------------------------------------------------------------#
    # Defines the biomes which this deposit can be generated in.
    # Biome is specified either by its numeric ID or by name (case-insensitive)
    # Each ID must be on a separate line without any delimiters.
    # If the whitelist is set, the blacklist will be ignored.
    ##########################################################################################################

    Biomes {
        #  [default: ]
        S:blackList <
         >

        #  [default: ]
        S:whiteList <
         >
    }

    ##########################################################################################################
    # Indicator
    #--------------------------------------------------------------------------------------------------------#
    # Defines the aboveground indicator for this deposit (e.g., a rare flower or a combination of circles of different flowers)
    ##########################################################################################################

    Indicator {
        # Defines the circles of indicators and their radiuses.
        # Syntax: indicatorId [, circleRadius]
        # The order of the circles is always shuffled.
        # The circles with the same radius will be randomly selected.
        # If the radius is not defined, it will be selected from the minimum available, starting from 1.
        # Examples:
        #      minecraft:cornflower, 2
        #      minecraft:orange_tulip, 4
        #  [default: [silentgems:glowrose:[gem=onyx], 3], [mysticFlowerBlack, 3], [double_plant:3, 3], [silentgems:glowrose:[gem=onyx], 6], [mysticFlowerBlack, 6], [double_plant:3, 6]]
        S:circles <
            silentgems:glowrose:[gem=onyx], 3
            mysticFlowerBlack, 3
            double_plant:3, 3
            silentgems:glowrose:[gem=onyx], 6
            mysticFlowerBlack, 6
            double_plant:3, 6
         >

        # Defines the percentage of the indicator shape that will be visible. [range: 0.0 ~ 100.0, default: 60.0]
        S:continuity=60.0

        # Defines the maximum displacement of the indicator shape elements. [range: 0 ~ 16, default: 1]
        I:distortion=1

        # Defines the id of the single-block indicator. [default: ]
        S:id=
    }

}



```

