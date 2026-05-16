# MEMORY.md - 长期记忆

## 项目背景
- 用户在腾讯金融科技部门，参与部门级 Harness 工程设计
- Harness 三层架构：应用层（Skills/动词）、原则层（Principles/形容词）、资料层（Materials/名词）
- 下阶段聚焦设计生产 Harness 搭建，尤其是页面生产 UI 方面

## Harness 架构关键决策
- 原则层定位为 Reference（判断型），不是 Skill
- 通用原则通过 Pre-hook 自动注入 design 类 Skill，设计师无感知
- 业务原则由 Skill 根据业务标签显式引用
- Post-hook 可用于自动合规检查（独立于 Skill 自查）
- 通用原则与业务原则的关系：继承 + 覆写，业务优先但必须显式声明覆写原因

## 通用原则一期清单（16 条）
U-001 费茨定律、U-002 格式塔原则、U-003 席克定律、U-004 峰终定律、U-005 米勒定律、U-006 反馈即时性、U-007 安全确认与容错、U-008 一致性、U-009 识别而非回忆、U-010 自然语言表达、U-011 无障碍可达、U-012 渐进式披露、U-013 信噪比、U-014 关键信息前置、U-015 用户控制与自由、U-016 透明与信任

## 通用原则设计规范
- 每条原则 7 字段：编号、一句话、判定条件、适用场景、与谁冲突、冲突时默认立场、正例/反例
- 判定条件是最核心字段，必须可判定（数值型/逻辑型/清单型）
- 冲突声明是灵魂——不冲突的原则可能不需要入库
- 数量控制：一期 16 条（原 10 条 + U-011 无障碍 + U-012 渐进式披露 + U-013 信噪比 + U-014 倒金字塔 + U-015 用户控制与自由 + U-016 透明与信任），二期按踩坑驱动追加
- 取舍准则有默认优先级（P0 安全确认与容错/无障碍可达 → P11 一致性），业务可覆写

## 团队分工
- 信用卡：资料层 tiantian、原则层 hookclin、应用层 stephy
- 通讯：资料层 jed、原则层 ruby、应用层 stephy(通用)
- 跨境：资料层 yuping、原则层 stephy、应用层 stephy(通用)

## 产出文件
- `/Users/tianlin/WorkBuddy/2026-05-15-task-20/universal-principles.md` - 通用设计原则完整文件（含 16 条卡片 + 16×16 冲突矩阵 + 取舍准则 P0-P11 + 二期候选 U-017~U-021 + 行业对标附录）
- `~/.workbuddy/skills/design-principles-review/` - 通用设计原则评审 Skill（原则层落地实现）

## GitHub 信息
- GitHub 用户名：tllll64，邮箱：astro12138@gmail.com
- SSH key 已配置（ed25519）
- 过程回顾页面已部署：https://tllll64.github.io/design-principles-review/
- 仓库地址：https://github.com/tllll64/design-principles-review

## 通用原则审查方法论
- 提出四维审查框架：D1 数量合理性、D2 业务适配性、D3 覆盖齐全度、D4 同事接受度
- D3 交互生命周期映射发现"信任"维度缺口，催生 U-016 透明与信任
- U-016 定位 P2（与 U-010 真实世界匹配同级），理由：信息缺失不造成直接损害但侵蚀信任根基
- U-016 冲突关系：U-012 渐进式披露 ○、U-013 信噪比 ○，默认立场"透明优先于简洁"

## 通用原则评审 Skill（design-principles-review）
- Skill 路径：`~/.workbuddy/skills/design-principles-review/`
- 6 步评审流程：识别对象 → 确定适用原则 → 逐条判定 → 冲突检测 → 生成报告 → 业务覆写提示
- 场景化原则筛选：支付/表单/信息展示/多步流程/错误页各有必查+按需原则列表
- 支持 Pre-hook 集成：将判定条件作为约束注入其他设计 Skill
- 包含评审报告模板（review-report.md）和冲突矩阵速查（conflict-matrix-quickref.md）
