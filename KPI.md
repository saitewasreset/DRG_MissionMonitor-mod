V0.1.0

# 主约束条件

$A_1$：故意友伤是不可接受的
$A_{11}$：友伤使队友死亡再救起是严重“亏损”的
$A_2$：因“奋战”而倒地是可以接受的
$A_3$：因“奋战”而吃补给是可以接受的
$A_4$：不建议“极限一换一”
$A_5$：因“奋战”而不小心友伤是可以接受的

# 符号表

符号|含义
---|---
$D$|输出：对怪物的输出，**不含造成友伤**
$H$|友伤
$D_A$|全输出，$D_A = D + H$
$k$|击杀数
$K^\alpha$|带权击杀数，$K^\alpha = \sum_{i = 1}^{n} k_i \cdot p_i,其中k_i为第i种怪物的击杀数,p_i为第i种怪物的权(使用权值表\alpha)$
$D^\alpha$|带权输出，$D^\alpha = \sum_{i = 1}^{n} D_i \cdot p_i,其中D_i为对第i种怪物的输出,p_i为第i种怪物的权(使用权值表\alpha)$



# 指数定义

|指数符号|指数释义|定义|值域
|------|-------|----|----
$K_I^{\alpha}$|击杀数指数：击杀数占总击杀数的比例（带权值，采用权值表$\alpha$）|$\frac{K_x ^ \alpha}{\sum_{i = 1}^{n} K_i ^ \alpha}$|$[0,1]$
$D_I^{\alpha}$|输出指数：输出占总输出的比例（带权值，采用权值表$\alpha$）|$\frac{D_x ^ \alpha}{\sum_{i = 1}^{n} D_i ^ \alpha}$|$[0,1]$
$P_I$|高威胁目标：使用高威胁权值表$\sigma$的输出指数|$\frac{D_x ^ \sigma}{\sum_{i = 1}^{n} D_i ^ \sigma}$|$[0,1]$
$r_I$|救人指数：救人次数占总救人次数的比例，**若总救人次数为0，则为1**|$\frac{r_x}{\sum_{i = 1}^{n} r_i}$|$[0,1]$
$d_I$|倒地指数：倒地次数占总倒地次数的比例，**若总倒地次数为0，则为0**|$ - \frac{d_x}{\sum_{i = 1}^{n} d_i}$|$[-1,0]$
$f_I$|友伤指数：详细定义见下|见下|$(- \infty, 1]$
$n_I$|硝石指数：采集硝石量占总硝石采集量的比例|略|$[0,1]$
$s_I$|补给指数：补给次数占总补给次数的比例|略|$[-1,0]$
$p_I$|采集指数：采集量占总采集量的比例|略|$[0,1]$

## 友伤指数($f_I$)算法：

$f(x) = \frac{99}{x - 1} + 100,其中x为友伤比例= \frac{H_i}{D_{Ai}}$

$f(x)的定义域为[0,1],值域为({\color{red} -\infty}, 1](A_1)(A_5)$

$x \cdot 10 ^ {-3}$|$f(x)$
---|---
$\color{blue}0.0$|$\color{blue}1.000$
$1.5$|$0.851$
$2.5$|$0.752$
$3.5$|$0.652$
$4.0$|$0.602$
$6.5$|$0.352$
$\color{blue}10$|$\color{blue}0.000$
$15$|$-0.508$
$20$|$-1.020$
$100$|$-10.00$
$1000$|$-\infty$

# 职业原始KPI

**注意：由于项目难度不同，不同职业的原始KPI没有可比性**
注意：下文中“侦察($S$)”默认指辅助型侦察。

## 钻机
$D_1$：对群[3]
$D_2$：弱远程

项目|权重
----|----
击杀数指数($k_I^D$)|$k_D$
输出指数($D_I^D$)|$D_D$
高威胁目标($P_I$)|$P_D$
救人指数($r_I$)|$r_D$
倒地指数($d_I$)|$d_D$
友伤指数($f_I$)|$f_D$
硝石指数($n_I$)|$n_D$
补给指数($s_I$)|$s_D$
采集指数($p_I$)|$p_D$

$D_1$： $k_D > D_D, k_D + D_D + P_D \ge 0.5$

$D_2$：$P_I = 0$

$A_1$：$f_D \ge 0.1, $

$A_2$：我们估计，平均每局总计输出大约为70k，钻机平均输出应大于10k，则不带权输出指数$D_I$应大约为$D^0 = \frac{1}{7}$，而带权输出指数$D^D_I$应大于$D_I$

我们估计，钻机每局*正常*倒地次数为2次($d^0$)，每局所有人总计倒地次数为6次($d^1$)，则由$A_2$：

$\frac{D^0}{d^0} \cdot D_D> \frac{1}{d^1} \cdot d_D$
解得$D_D > \frac{d^0 \cdot d_D}{d^1 \cdot D^0} = \frac{7}{3} \cdot d_D$

$A_3$：我们估计，钻机的补给指数约为$\frac{1}{4}$($s^0$)（钻机$\frac{1}{4}$，枪手$\frac{1}{4}$，工程$\frac{3}{8}$，侦察$\frac{1}{8}$）

我们估计，5k伤害对应一份补给，即一份补给对应约$\frac{D^0}{2} = \frac{1}{14}$

则由$A_3$：$\frac{D^0}{2} \cdot D_D > s^0 \cdot s_D$

解得$s_D < \frac{D^0 \cdot D_D}{2 s^0} = \frac{2}{7} D_D$

$A_4$：$d_D \ge r_D$


符合上述所有约束条件的一组参考权重如下：
项目|权重
----|----
击杀数指数($k_I^D$)|$0.400$
输出指数($D_I^D$)|$0.200$
高威胁目标($P_I$)|$0.000$
救人指数($r_I$)|$0.080$
倒地指数($d_I$)|$0.085$
友伤指数($f_I$)|$0.100$
硝石指数($n_I$)|$0.048$
补给指数($s_I$)|$0.057$
采集指数($p_I$)|$0.030$
## 枪手
$G_1$： 提供强有力的火力支援[3][4]：对单+对群[3]

项目|权重
----|----
击杀数指数($k_I^G$)|$k_G$
输出指数($D_I^G$)|$D_G$
高威胁目标($P_I$)|$P_G$
救人指数($r_I$)|$r_G$
倒地指数($d_I$)|$d_G$
友伤指数($f_I$)|$f_G$
硝石指数($n_I$)|$n_G$
补给指数($s_I$)|$s_G$
采集指数($p_I$)|$p_G$

$G_1$：$k_G + D_G + P_G \ge 0.75, D_G > P_G > k_G$

$A_1$：$f_G \ge 0.1$

$A_2$：我们估计，平均每局总计输出大约为70k，枪手平均输出应大于20k，则不带权输出指数$D_I$应大约为$D^0 = \frac{2}{7}$，而带权输出指数$D^G_I$应大于$D_I$

我们估计，枪手每局*正常*倒地次数为2次($d^0$)，每局所有人总计倒地次数为6次($d^1$)，则由$A_2$：

$\frac{D^0}{d^0} \cdot D_G> \frac{1}{d^1} \cdot d_G$
解得$D_G > \frac{d^0 \cdot d_G}{d^1 \cdot D^0} = \frac{7}{6} \cdot d_G$

$A_3$：我们估计，枪手的补给指数约为$\frac{1}{4}$($s^0$)（钻机$\frac{1}{4}$，枪手$\frac{1}{4}$，工程$\frac{3}{8}$，侦察$\frac{1}{8}$）

我们估计，8k伤害对应一份补给，即一份补给对应约$\frac{2D^0}{5} = \frac{4}{35}$

则由$A_3$：$\frac{2D^0}{5} \cdot D_G > s^0 \cdot s_G$

解得$s_G < \frac{2D^0 \cdot D_G}{5 s^0} = \frac{16}{35} D_G$

$A_4$：$d_G \ge r_G$

符合上述所有约束条件的一组参考权重如下：

项目|权重
----|----
击杀数指数($k_I^G$)|$0.050$
输出指数($D_I^G$)|$0.400$
高威胁目标($P_I$)|$0.300$
救人指数($r_I$)|$0.050$
倒地指数($d_I$)|$0.050$
友伤指数($f_I$)|$0.100$
硝石指数($n_I$)|$0.015$
补给指数($s_I$)|$0.025$
采集指数($p_I$)|$0.010$

## 工程
$E_1$： 输出[3][4]

项目|权重
----|----
击杀数指数($k_I^E$)|$k_E$
输出指数($D_I^E$)|$D_E$
高威胁目标($P_I$)|$P_E$
救人指数($r_I$)|$r_E$
倒地指数($d_I$)|$d_E$
友伤指数($f_I$)|$f_E$
硝石指数($n_I$)|$n_E$
补给指数($s_I$)|$s_E$
采集指数($p_I$)|$p_E$

$E_1$：$k_E + D_E + P_E \ge 0.65, D_E > P_E > k_E$

$A_1$：$f_E \ge 0.1, $

$A_2$：我们估计，平均每局总计输出大约为70k，工程平均输出应大于30k，则不带权输出指数$D_I$应大约为$D^0 = \frac{3}{7}$，而带权输出指数$D^E_I$应大于$D_I$

我们估计，工程每局*正常*倒地次数为2次($d^0$)，每局所有人总计倒地次数为6次($d^1$)，则由$A_2$：

$\frac{D^0}{d^0} \cdot D_E> \frac{1}{d^1} \cdot d_E$
解得$D_E > \frac{d^0 \cdot d_E}{d^1 \cdot D^0} = \frac{7}{9} \cdot d_E$

$A_3$：我们估计，工程的补给指数约为$\frac{3}{8}$($s^0$)（钻机$\frac{1}{4}$，枪手$\frac{1}{4}$，工程$\frac{3}{8}$，侦察$\frac{1}{8}$）

我们估计，10k伤害对应一份补给，即一份补给对应约$\frac{D^0}{3} = \frac{1}{7}$

则由$A_3$：$\frac{D^0}{3} \cdot D_E > s^0 \cdot s_E$

解得$s_E < \frac{D^0 \cdot D_E}{3 s^0} = \frac{8}{21} D_E$

$A_4$：$d_E \ge r_E$

符合上述所有约束条件的一组参考权重如下：

项目|权重
----|----
击杀数指数($k_I^E$)|$0.050$
输出指数($D_I^E$)|$0.500$
高威胁目标($P_I$)|$0.100$
救人指数($r_I$)|$0.050$
倒地指数($d_I$)|$0.050$
友伤指数($f_I$)|$0.100$
硝石指数($n_I$)|$0.045$
补给指数($s_I$)|$0.080$
采集指数($p_I$)|$0.025$

## 侦察

$S_1$：保证硝石供应[1][2][3][4]
$S_2$：处理高威胁单位[1][2][3]
$S_3$：杀敌不是主要工作[2][3][4]
$S_4$：采矿[3][4]

项目|权重
----|----
击杀数指数($k_I^S$)|$k_S$
输出指数($D_I^S$)|$D_S$
高威胁目标($P_I$)|$P_S$
救人指数($r_I$)|$r_S$
倒地指数($d_I$)|$d_S$
友伤指数($f_I$)|$f_S$
硝石指数($n_I$)|$n_S$
补给指数($s_I$)|$s_S$
采集指数($p_I$)|$p_S5$

$S_1$：$n_S \ge 0.3$
$S_2$：$P_S > D_S, P_S > k_S, P_S \ge 0.1$
$S_3$：$k_S + D_S + P_S \le 0.2$
$S_4$：$n_S + p_S \ge 0.5$

$A_1$：$f_S \ge 0.1, $

$A_2$：不适用

$A_3$：我们估计，侦察的补给指数约为$\frac{1}{8}$($s^0$)（钻机$\frac{1}{4}$，枪手$\frac{1}{4}$，工程$\frac{3}{8}$，侦察$\frac{1}{8}$），$D^0 = \frac{4}{35}$

我们估计，4k伤害对应一份补给（不然灯真的不够用啊qwq），即一份补给对应约$\frac{D^0}{2} = \frac{2}{35}$

则由$A_3$：$\frac{D^0}{2} \cdot D_S > s^0 \cdot s_S$

解得$s_S < \frac{D^0 \cdot D_S}{2 s^0} = \frac{16}{35} D_S$

$A_4$：$d_S \ge r_S$

符合上述所有约束条件的一组参考权重如下：

项目|权重
----|----
击杀数指数($k_I^S$)|$0.030$
输出指数($D_I^S$)|$0.040$
高威胁目标($P_I$)|$0.100$
救人指数($r_I$)|$0.102$
倒地指数($d_I$)|$0.115$
友伤指数($f_I$)|$0.100$
硝石指数($n_I$)|$0.300$
补给指数($s_I$)|$0.013$
采集指数($p_I$)|$0.200$

## 输出型侦察

$S'_1$：对单输出
$S'_2$：处理高威胁单位
$S'_3$：保证硝石供应
$S'_4$：采矿

项目|权重
----|----
击杀数指数($k_I^{S'}$)|$k_{S'}$
输出指数($D_I^{S'}$)|$D_{S'}$
高威胁目标($P_I$)|$P_{S'}$
救人指数($r_I$)|$r_{S'}$
倒地指数($d_I$)|$d_{S'}$
友伤指数($f_I$)|$f_{S'}$
硝石指数($n_I$)|$n_{S'}$
补给指数($s_I$)|$s_{S'}$
采集指数($p_I$)|$p_{S'}$

$S'_1$：$k_{S'} + D_{S'} + P_{S'} \ge 0.6, P_{S'} > D_{S'} > k_{S'}, k_{S'}=0$

$S'_2$：$P_{S'} \ge 0.3$

$S'_3$：$n_{S'} \ge 0.1$

$S'_4$：$n_{S'} + p_{S'} \ge 0.15$

$A_1$：$f_{S'} \ge 0.1$

$A_2$：我们估计，平均每局总计输出大约为70k，输出型侦察平均输出应大于15k，则不带权输出指数$D_I$应大约为$D^0 = \frac{3}{14}$，而带权输出指数$D^{S'}_I$应大于$D_I$

我们估计，输出型侦察每局*正常*倒地次数为1.5次($d^0$)，每局所有人总计倒地次数为6次($d^1$)，则由$A_2$：

$\frac{D^0}{d^0} \cdot D_{S'}> \frac{1}{d^1} \cdot d_{S'}$
解得$D_{S'} > \frac{d^0 \cdot d_{S'}}{d^1 \cdot D^0} = \frac{7}{6} \cdot d_{S'}$

$A_3$：我们估计，输出型侦察的补给指数约为$\frac{1}{4}$($s^0$)（钻机$\frac{1}{4}$，枪手$\frac{1}{4}$，工程$\frac{3}{8}$，(辅助型)侦察$\frac{1}{8}$）

我们估计，8k伤害对应一份补给，即一份补给对应约$\frac{8D^0}{15} = \frac{4}{35}$

则由$A_3$：$\frac{8D^0}{15} \cdot D_{S'} > s^0 \cdot s_{S'}$

解得$s_{S'} < \frac{8D^0 \cdot D_{S'}}{15 s^0} = \frac{16}{35} D_{S'}$

$A_4$：$d_{S'} \ge r_{S'}$

符合上述所有约束条件的一组参考权重如下：

项目|权重
----|----
击杀数指数($k_I^{S'}$)|$0.000$
输出指数($D_I^{S'}$)|$0.250$
高威胁目标($P_I$)|$0.350$
救人指数($r_I$)|$0.055$
倒地指数($d_I$)|$0.065$
友伤指数($f_I$)|$0.100$
硝石指数($n_I$)|$0.100$
补给指数($s_I$)|$0.030$
采集指数($p_I$)|$0.050$

# 权值表

除特殊说明，以下表格中未出现的怪物，权值为$1$

## 高威胁目标权值表$\sigma$

对于本表格，未出现的怪物，权值为$0$

|ID|中文名|权值
|--|-----|---
ED_Spider_Stalker|潜影异虫|$16$
ED_CaveLeech|洞穴水蛭|$8$
ED_BarrageInfector|瘟疫霰射吐珠|$7$
ED_TentaclePlant|瓦托克鳞甲荆丛|$7$
ED_Spider_Stinger|蛭尾异虫|$7$
ED_Grabber|捕手异虫蝇|$6$
ED_ShootingPlant|瘟疫吐珠|$6$
ED_Spider_Shooter|吐酸异虫|$6$
ED_Spider_Shooter_Ground|吐酸异虫|$6$
ED_Spider_Shooter_Rockpox_Plague|岩痘吐酸异虫|$6$
ED_Spider_Lobber|脓毒异虫|$6$
ED_Spider_RapidShooter|速射酸虫|$5$
ED_Mactera_Shooter_Normal|吐刺异虫蝇|$5$
ED_Mactera_TripleShooter|三颚异虫蝇|$5$
ED_Mactera_Shooter_HeavyVeteran|坚甲异虫蝇|$5$
ED_Spider_Spitter|吐丝异虫|$5$
ED_Spider_Buffer|异虫典狱长|$3$
ED_Bomber|黏液轰炸蝇|$2$
ED_Bomber_Explosive|火焰轰炸蝇|$2$
ED_Bomber_Ice|冰霜轰炸蝇|$2$
ED_Bomber_Rockpox_Plague|岩痘黏液轰炸蝇|$2$
ED_Spider_Exploder|自爆异虫|$1$
ED_Spider_Exploder_Rockpox_Plague|岩痘自爆异虫|$1$
ED_Spider_Exploder_Warning|自爆异虫|$1$
ED_Woodlouse|丘罗那地虱|$1$
ED_Woodlouse_Youngling|地虱幼体|$1$

## 钻机权值表$D$

|ID|中文名|权值
|--|-----|---
ED_Spider_Hoarder|嗜矿异虫|$5$
ED_EggSpider|蜂拥异虫|$5$
ED_InfestationLarva|肉食幼虫|$5$
ED_Spider_Spawn|异虫幼虫|$5$
ED_TunnelSwarmer|蜂拥异虫|$5$
ED_Spider_Swarmer|蜂拥异虫|$5$
ED_Spider_Swarmer_Ice|蜂拥异虫|$5$
ED_Spider_Swarmer_Mutated|蜂拥异虫|$5$
ED_Spider_Swarmer_Pheromone_NOFX|蜂拥异虫|$5$
ED_Spider_Boss_Heavy|巢主无畏异虫|$3$
ED_Spider_Boss_TwinA|强弩无畏异虫|$3$
ED_Spider_Boss_TwinB|重斧无畏异虫|$3$
ED_Spider_Tank_Boss|无畏异虫|$3$
ED_Spider_Exploder|自爆异虫|$3$
ED_Spider_Exploder_Rockpox_Plague|岩痘自爆异虫|$3$
ED_Spider_Exploder_Warning|自爆异虫|$3$
ED_Spider_Grunt|战士异虫|$3$
ED_Spider_Grunt_Attacker|刀锋异虫|$3$
ED_Spider_Grunt_Guard|护卫异虫|$3$
ED_Spider_Grunt_Ice|战士异虫|$3$
ED_Spider_Grunt_Mutated|战士异虫|$3$
ED_Spider_Grunt_RockpoxPlague|岩痘战士异虫|$3$
ED_Spider_GruntTutorial|战士异虫|$3$
ED_Spider_ShieldTank|暴君异虫|$2$
ED_Crawler|匍行核岩孽生兽|$2$
ED_Spider_Tank|禁卫异虫|$2$
ED_Spider_Tank_Ice|寒霜禁卫异虫|$2$
ED_Spider_Tank_Mutated|禁卫异虫|$2$
ED_Spider_Tank_RockpoxPlague|岩痘禁卫异虫|$2$

## 枪手权值表$G$

|ID|中文名|权值
|--|-----|---
ED_Spider_Hoarder|嗜矿异虫|$5$
ED_Nisse|圣诞小精灵|$5$
ED_GreatEggHunt_SpringBunny|春日兔兔|$5$
ED_Halloween_Skull|万圣节头骨|$5$
ED_Flea|脓蚤|$5$
ED_FlyingSmartRock|飞石|$5$
ED_FacilityTurret_Barrier|推斥炮塔|$3$
ED_FacilityTurret_Burst|连射炮塔|$3$
ED_FacilityTurret_Sniper|狙击炮塔|$3$
ED_HydraWeed|科洛克王草|$3$
ED_InfectedMule|BET-C|$3$
ED_PatrolBot|巡逻机器人|$3$
ED_PatrolBot_Caretaker|巡逻机器人|$3$
ED_Prospector|勘探者无人机|$3$
ED_Spider_Boss_Heavy|巢主无畏异虫|$3$
ED_Spider_Boss_TwinA|强弩无畏异虫|$3$
ED_Spider_Boss_TwinB|重斧无畏异虫|$3$
ED_Spider_Tank_Boss|无畏异虫|$3$
ED_Spider_ExploderTank|大自爆虫|$3$
ED_Spider_ExploderTank_King|自爆王虫|$3$
ED_Spider_Tank|禁卫异虫|$3$
ED_Spider_Tank_Amber|氪化禁卫异虫|$3$
ED_Spider_ShieldTank|暴君异虫|$3$
ED_Spider_Charger|禁卫异虫|$3$
ED_Spider_Tank_Ice|寒霜禁卫异虫|$3$
ED_Spider_Tank_Mutated|禁卫异虫|$3$
ED_Spider_Tank_RockpoxPlague|岩痘禁卫异虫|$3$
ED_Bomber|黏液轰炸蝇|$2$
ED_Bomber_Explosive|火焰轰炸蝇|$2$
ED_Bomber_Ice|冰霜轰炸蝇|$2$
ED_Bomber_Rockpox_Plague|岩痘黏液轰炸蝇|$2$
ED_Grabber|捕手异虫蝇|$2$
ED_Mactera_Shooter_Amber|氪化吐刺异虫蝇|$2$
ED_Mactera_Shooter_HeavyVeteran|坚甲异虫蝇|$2$
ED_Mactera_Shooter_Normal|吐刺异虫蝇|$2$
ED_Mactera_TripleShooter|三颚异虫蝇|$2$
ED_Spider_Amber_Shooter|氪化吐酸异虫|$2$
ED_Spider_Lobber|脓毒异虫|$2$
ED_Spider_RapidShooter|速射酸虫|$2$
ED_Spider_Shooter|吐酸异虫|$2$
ED_Spider_Shooter_Ground|吐酸异虫|$2$
ED_Spider_Shooter_Rockpox_Plague|岩痘吐酸异虫|$2$
ED_Spider_Spitter|吐丝异虫|$2$
ED_Spider_Tank_HeavySpawn|哨卫异虫|$2$

## 工程权值表$E$

|ID|中文名|权值
|--|-----|---
ED_Spider_Hoarder|嗜矿异虫|$5$
ED_Nisse|圣诞小精灵|$5$
ED_GreatEggHunt_SpringBunny|春日兔兔|$5$
ED_Halloween_Skull|万圣节头骨|$5$
ED_Flea|脓蚤|$5$
ED_HydraWeed|科洛克王草|$3$
ED_InfectedMule|BET-C|$3$
ED_Spider_Boss_Heavy|巢主无畏异虫|$3$
ED_Spider_Boss_TwinA|强弩无畏异虫|$3$
ED_Spider_Boss_TwinB|重斧无畏异虫|$3$
ED_Spider_Tank_Boss|无畏异虫|$3$
ED_Spider_ShieldTank|暴君异虫|$3$
ED_Bomber|黏液轰炸蝇|$2$
ED_Bomber_Explosive|火焰轰炸蝇|$2$
ED_Bomber_Ice|冰霜轰炸蝇|$2$
ED_Bomber_Rockpox_Plague|岩痘黏液轰炸蝇|$2$
ED_EggSpider|蜂拥异虫|$2$
ED_Mactera_Shooter_Amber|氪化吐刺异虫蝇|$2$
ED_Mactera_Shooter_HeavyVeteran|坚甲异虫蝇|$2$
ED_Mactera_Shooter_Normal|吐刺异虫蝇|$2$
ED_Mactera_TripleShooter|三颚异虫蝇|$2$
ED_PlagueLarva|岩痘幼虫|$2$
ED_PlagueShark|成熟岩痘幼虫|$2$
ED_Spider_Amber_Shooter|氪化吐酸异虫|$2$
ED_Spider_Charger|禁卫异虫|$2$
ED_Spider_ExploderTank|大自爆虫|$2$
ED_Spider_ExploderTank_King|自爆王虫|$2$
ED_Spider_Grunt|战士异虫|$2$
ED_Spider_Grunt_Attacker|刀锋异虫|$2$
ED_Spider_Grunt_Guard|护卫异虫|$2$
ED_Spider_Grunt_Ice|战士异虫|$2$
ED_Spider_Grunt_Mutated|战士异虫|$2$
ED_Spider_Grunt_RockpoxPlague|岩痘战士异虫|$2$
ED_Spider_GruntTutorial|战士异虫|$2$
ED_Spider_Spawn|异虫幼虫|$2$
ED_Spider_Swarmer|蜂拥异虫|$2$
ED_Spider_Swarmer_Ice|蜂拥异虫|$2$
ED_Spider_Swarmer_Mutated|蜂拥异虫|$2$
ED_Spider_Swarmer_Pheromone_NOFX|蜂拥异虫|$2$
ED_Spider_Tank|禁卫异虫|$2$
ED_Spider_Tank_Amber|氪化禁卫异虫|$2$
ED_Spider_Tank_Ice|寒霜禁卫异虫|$2$
ED_Spider_Tank_Mutated|禁卫异虫|$2$
ED_Spider_Tank_Rock|矿化禁卫异虫|$2$
ED_Spider_Tank_Rock_Warning|矿化禁卫异虫|$2$
ED_Spider_Tank_RockpoxPlague|岩痘禁卫异虫|$2$
ED_TunnelSwarmer|蜂拥异虫|$2$

## 侦察权值表$S$

|ID|中文名|权值
|--|-----|---
ED_Spider_Hoarder|嗜矿异虫|$5$
ED_Nisse|圣诞小精灵|$5$
ED_GreatEggHunt_SpringBunny|春日兔兔|$5$
ED_Halloween_Skull|万圣节头骨|$5$
ED_Flea|脓蚤|$5$
ED_Bomber|黏液轰炸蝇|$3$
ED_Bomber_Explosive|火焰轰炸蝇|$3$
ED_Bomber_Ice|冰霜轰炸蝇|$3$
ED_Bomber_Rockpox_Plague|岩痘黏液轰炸蝇|$3$
ED_HydraWeed|科洛克王草|$3$
ED_JellyBreeder|纳多赛特饲育水母|$3$
ED_JellyBreeder_RockpoxPlague|岩痘纳多赛特饲育水母|$3$
ED_Mactera_Shooter_Amber|氪化吐刺异虫蝇|$3$
ED_Mactera_Shooter_HeavyVeteran|坚甲异虫蝇|$3$
ED_Mactera_Shooter_Normal|吐刺异虫蝇|$3$
ED_Mactera_TripleShooter|三颚异虫蝇|$3$
ED_Spider_Amber_Shooter|氪化吐酸异虫|$3$
ED_Spider_Boss_Heavy|巢主无畏异虫|$3$
ED_Spider_Boss_TwinA|强弩无畏异虫|$3$
ED_Spider_Boss_TwinB|重斧无畏异虫|$3$
ED_Spider_Spitter|吐丝异虫|$3$
ED_Spider_Tank_Boss|无畏异虫|$3$
ED_FacilityTurret_Barrier|推斥炮塔|$2$
ED_FacilityTurret_Burst|连射炮塔|$2$
ED_FacilityTurret_Sniper|狙击炮塔|$2$
ED_FlyingSmartRock|飞石|$2$
ED_SpiderSpawner|异虫母巢|$2$

## 输出型侦察权值表$S'$

|ID|中文名|权值
|--|-----|---
ED_Spider_Hoarder|嗜矿异虫|$5$
ED_Nisse|圣诞小精灵|$5$
ED_GreatEggHunt_SpringBunny|春日兔兔|$5$
ED_Halloween_Skull|万圣节头骨|$5$
ED_Flea|脓蚤|$5$
ED_InfectedMule|BET-C|$4$
ED_Bomber|黏液轰炸蝇|$3$
ED_Bomber_Explosive|火焰轰炸蝇|$3$
ED_Bomber_Ice|冰霜轰炸蝇|$3$
ED_Bomber_Rockpox_Plague|岩痘黏液轰炸蝇|$3$
ED_FacilityTurret_Barrier|推斥炮塔|$3$
ED_FacilityTurret_Burst|连射炮塔|$3$
ED_FacilityTurret_Sniper|狙击炮塔|$3$
ED_FlyingSmartRock|飞石|$3$
ED_Grabber|捕手异虫蝇|$3$
ED_JellyBreeder|纳多赛特饲育水母|$3$
ED_JellyBreeder_RockpoxPlague|岩痘纳多赛特饲育水母|$3$
ED_Mactera_Shooter_Amber|氪化吐刺异虫蝇|$3$
ED_Mactera_Shooter_HeavyVeteran|坚甲异虫蝇|$3$
ED_Mactera_Shooter_Normal|吐刺异虫蝇|$3$
ED_Mactera_TripleShooter|三颚异虫蝇|$3$
ED_PatrolBot|巡逻机器人|$3$
ED_PatrolBot_Caretaker|巡逻机器人|$3$
ED_Prospector|勘探者无人机|$3$
ED_Spider_Amber_Shooter|氪化吐酸异虫|$3$
ED_Spider_Boss_Heavy|巢主无畏异虫|$3$
ED_Spider_Boss_TwinA|强弩无畏异虫|$3$
ED_Spider_Boss_TwinB|重斧无畏异虫|$3$
ED_Spider_Tank_Boss|无畏异虫|$3$
ED_Spider_Buffer|异虫典狱长|$3$
ED_HydraWeed|科洛克王草|$3$
ED_Spider_ShieldTank|暴君异虫|$3$
ED_Spider_Spitter|吐丝异虫|$3$
ED_Terminator|深渊复仇者|$3$
ED_Spider_ExploderTank|大自爆虫|$2$
ED_Spider_ExploderTank_King|自爆王虫|$2$
ED_Spider_Charger|禁卫异虫|$2$
ED_Spider_Tank|禁卫异虫|$2$
ED_Spider_Tank_Amber|氪化禁卫异虫|$2$
ED_Spider_Tank_HeavySpawn|哨卫异虫|$2$
ED_Spider_Tank_Ice|寒霜禁卫异虫|$2$
ED_Spider_Tank_Mutated|禁卫异虫|$2$
ED_Spider_Tank_Rock|矿化禁卫异虫|$2$
ED_Spider_Tank_Rock_Warning|矿化禁卫异虫|$2$
ED_Spider_Tank_RockpoxPlague|岩痘禁卫异虫|$2$

# 参考
[1]：https://www.bilibili.com/video/BV1ig4y197GB 02:00
[2]：https://tieba.baidu.com/p/7819452549
[3]：https://tieba.baidu.com/p/7253319800
[4]：https://api.xiaoheihe.cn/v3/bbs/app/api/web/share?link_id=119582418