# UE5 ActionRPG 学习进度

## 2026-09-28

### 学习环境
- 项目已 clone 到本地，并建立独立 Git 仓库。
- Unreal Engine：5.7.4 源码编译版。
- IDE：Rider 2026.2.2。
- 项目已成功编译并正常运行。

### 游玩观察
- 输入：WASD 移动；空格和鼠标右键翻滚；R 使用回血或回蓝道具；鼠标左键攻击并可三段派生；鼠标控制镜头；Esc 暂停并打开菜单。
- 玩家已观察到移动、攻击和闪避；本轮未观察到其他主动技能。
- 敌人类型包括近战小怪、远程小怪和近战精英怪；观察到敌人之间会互相造成伤害。
- 战斗 UI 包括血条、蓝条、技能图标、灵魂数量、波次倒计时；敌人头上有箭头指示，攻击后显示敌人血条。
- 精英怪似乎有概率掉落可强化武器的物品；强化后会改变攻击动作并提高伤害。
- 角色和敌人受击时有红色效果；使用血瓶/蓝瓶时出现对应回复特效。

### 已追踪：鼠标左键攻击
- `IA_NormalAttack` 映射到鼠标左键。
- 输入在 `BP_PlayerCharacter` 中处理，未在 `BP_PlayerController` 中找到绑定。
- `BP_PlayerCharacter` 调用 `DoMeleeAttack`。
- 蓝图通过 `Ability.Melee` Gameplay Tag 判断当前是否处于近战能力中。
- 随后通过 `JumpSectionForCombo` 调用 `Montage_SetNextSection`，设置 Montage 的下一个 Section，以衔接连段。
- 初步理解：`Montage_SetNextSection` 是安排当前 Section 后续转到哪个 Section；具体连段窗口、参数含义和实际分支尚待核实。

### 下次从这里继续
1. 查看 `DoMeleeAttack` 内部节点，确认 Tag 检查的具体方式、条件分支和各分支调用。
2. 查看 `JumpSectionForCombo`，记录传入的当前 Section 与目标 Section 名，并确认 Montage 何时读取这个设置。
3. 若有节点仍不清楚，提供相关蓝图截图，按执行顺序逐个解释。
4. 后续可再追 `GA_PlayerSwordMelee`、攻击 Montage/Notify、命中目标与伤害效果，核实攻击完整链路。

### 仓库状态提醒
截至本次查看，Git 状态还包含 `.vsconfig` 与 `ActionRPG.uproject` 的既有修改，以及未跟踪的计划文档文件；学习日志本身也是新文件。开始新修改前应先检查 `git status`，不要把环境配置变动误认为学习过程中新增的源码修改。
