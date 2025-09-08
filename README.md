<!--
 * @Author: lhx 769681799@qq.com
 * @Date: 2025-09-08 13:30:36
 * @LastEditors: lhx 769681799@qq.com
 * @LastEditTime: 2025-09-08 14:17:39
 * @FilePath: /CaeriLib/WowDEF.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
# 一、基础语法与核心命令
-----------------------------------------------------------------------------------
宏命令格式 <br>
所有宏命令以 / 开头，大小写不敏感，空格分隔参数。 <br>
例：/cast 技能名称（施放技能）、/use 物品名称（使用物品） <br>
条件判断符 [] <br>
用于根据场景自动切换行为，格式：命令 [条件1] 效果1; [条件2] 效果2 <br>
常用条件： <br>
@目标：指定目标（如 @player 自己、@targettarget 目标的目标、@focus 焦点目标） <br>
combat：战斗中 <br>
nocombat：非战斗中 <br>
dead：目标已死 <br>
help：目标为友方（可治疗） <br>
harm：目标为敌方（可攻击） <br>

# 二、技能与物品相关命令
-----------------------------------------------------------------------------------
施放技能：/cast <br>
基础用法：/cast 技能名称（如 /cast 治疗术） <br>
条件施法：/cast [@player] 治疗术（无论目标是谁，都给自己加血） <br>
优先级施法：/cast [harm] 寒冰箭; [help] 法力护盾（敌方放寒冰箭，友方套护盾） <br>
使用物品：/use <br>
基础用法：/use 药水名称（如 /use 强效治疗药水） <br>
按栏位使用：/use 13（使用饰品栏 1，13 = 第一饰品，14 = 第二饰品） <br>
技能队列：/castsequence <br>
按顺序施放技能，需依次点击： <br>
castsequence reset=10 暗影箭, 腐蚀术, 痛苦诅咒（10 秒未点击则重置顺序） <br>

# 三、目标选择命令
-----------------------------------------------------------------------------------
选中目标：/target <br>
按名称选目标：/target 玩家名称 <br>
选特定 NPC：/target 首领名称（如 /target 奥妮克希亚） <br>
协助目标：/assist <br>
自动选中目标的目标（常用于跟随坦克攻击）： <br>
/assist [@focus]（协助焦点目标攻击其目标） <br>
设置焦点：/focus <br>
将当前目标设为焦点（方便监控 / 优先处理）： <br>
/focus（无参数则设当前目标为焦点） <br>
/focus [@targettarget]（设目标的目标为焦点） <br>
清除目标 / 焦点：/cleartarget / /clearfocus <br>
cleartarget（清除当前目标）、clearfocus（清除焦点） <br>

# 四、战斗与状态命令
-----------------------------------------------------------------------------------
攻击 / 停止攻击：/startattack / /stopattack <br>
startattack（自动攻击当前目标）、stopattack（停止攻击） <br>
宠物命令（猎人 / 术士等） <br>
/petattack（宠物攻击当前目标） <br>
/petfollow（宠物跟随自己） <br>
/petstay（宠物停留原地） <br>
/petdismiss（解散宠物） <br>
坐骑与形态 <br>
召唤坐骑：/mount 坐骑名称 <br>
切换形态（德鲁伊等）：/cast 熊形态 <br>

# 五、表情与聊天命令
-----------------------------------------------------------------------------------
常用表情：/表情名称 <br>
/say 文本（当前频道说话） <br>
/yell 文本（大喊，周围玩家可见） <br>
/whisper 玩家名称 文本（密语玩家） <br>
趣味表情：/dance（跳舞）、/roar（咆哮）、/bow（鞠躬） <br>
宏内聊天提示 <br>
结合技能提示队友：/cast 治疗链; /say 正在刷治疗链，注意血线！ <br>

# 六、界面与系统命令
-----------------------------------------------------------------------------------
开关界面元素 <br>
/run ToggleFrame(WorldMapFrame)（开关世界地图） <br>
/console WorldMapZoom 1（世界地图缩放到最大） <br>
自动交接任务 <br>
/run SelectGossipAvailableQuest(); CompleteQuest(); GetQuestReward()（自动接取 / 完成任务并领奖励，部分场景适用） <br>

# 七、实用宏示例（结合基础命令）
-----------------------------------------------------------------------------------
治疗职业通用宏 <br>
#showtooltip 强效治疗术 <br>
/cast [@mouseover,help,nodead] 强效治疗术; [help,nodead] 强效治疗术; [@player] 强效治疗术 <br>
（鼠标悬停友方则治疗该目标，无目标则治疗自己） <br>
坦克拉怪宏 <br>
#showtooltip 嘲讽 <br>
/cast [@focus,harm,exists] 嘲讽; [@targettarget,harm,exists] 嘲讽; 嘲讽 <br>
（优先嘲讽焦点目标，其次嘲讽目标的目标，最后嘲讽当前目标） <br>
战斗 / 非战斗切换宏 <br>
#showtooltip <br>
/cast [combat] 血性狂暴; [nocombat] 进食充分 <br>
（战斗中开爆发，非战斗中吃食物 buff） <br>

## NORMAL ##
// 将当前目标设为焦点 <br>
/focus [@target] <br>

// 焦点嘲讽 没有焦点时，对目标的目标进行嘲讽,否则直接嘲讽 <br>
/cast [@focus,harm,exists] 嘲讽; [@targettarget,harm,exists] 嘲讽; 嘲讽 <br>

// 对悬停目标进行复生并且发送密语 <br>
/run local u="mouseover";if UnitExists(u) and UnitIsFriend("player",u) and not UnitIsDeadOrGhost(u) then CastSpellByName("复生",u);SendChatMessage("喂了 "..UnitName(u).." 一坨大便，如不能药到病除则开除贱籍","WHISPER",nil,UnitName(u))end

## DRUID ##
### 趴熊并且释放生存本能
/cast 熊形态; /cast 树皮术; /cast 生存本能 <br>

### 猎豹并且潜行(为进行战斗,否则疾跑)
/cast 猎豹形态 [nocombat] 潜行 [combat] 疾跑 <br>

