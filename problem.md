# 伤害统计
1. 仅统计实际伤害（目标血量变化）（对玩家：血量+护盾变化）

## 怪物受到伤害
1. 无法统计无来源伤害的Causer（骤变、护盾破碎伤害、枪手“武装核心” 电磁手炮部分伤害、高度警觉）
2. 某些伤害不能被统计：破甲（即`Health`不变）、非`EnemyPawn`子类的“怪物”（如核心岩**本体**，非猴子）
3. 部分手雷造成的伤害无法统计武器类型（将记为`Weapon=Other`）
4. 侦察冰弩无法统计武器类型（将记为`Weapon=Other`）（普通弩箭可）（鬼船NB）

# 补给使用情况
1. 仅能统计使得弹药量变化比例大于1%的情况。

# 任务状态
1. 深潜的任务时间（`Mission Time`）在三个任务间是不重置的。
2. 失败的任务仍然会记为`result=0`
# Bug
1. 任务刚开始的某些时刻（`OnPlayerCharacterRegistered`后）调用`InventoryComponent`的`GetTotalAmmoLeft`方法将导致崩溃。
2. `GetTotalAmmoLeft`不能正确返回客机的子弹剩余量（将始终为最大值）。
3. `OnDamagedEnemy`是在客机处理的。
4. `FSDPlayerState`类中的`GetSupplyAmmoStatus`方法返回的值有更新延迟：`OnResupplied`事件发生后，仍然返回补给前的值。Delay 0.2s仍不可，Delay 0.5s可。
5. `FSDGameState`中的`PlayerMadeItToDropPod`即使在任务失败时也是`true`