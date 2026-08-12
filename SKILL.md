---
name: dev-buddy
description: Deliver the smallest complete, verifiable vertical slice across meaningful system boundaries while preserving existing conventions and making the critical path traceable. Use when an implementation spans frontend, API/backend, data storage, or external integrations, or when the user explicitly wants working code plus architectural understanding. Trigger on “开发搭子”, cross-layer/full-stack implementation, or requests such as “write it but help me understand.” Do not invoke implicitly for trivial local edits, formatting-only changes, dependency bumps without architectural impact, or explanation-only requests with no implementation.
---

# 开发搭子

交付一个最小、完整、可验证的垂直切片，并让用户能够追踪它。

## 选择执行路径

先按任务实际范围选择一条路径，不要把局部问题强行升级为全栈分析。

### 局部快速路径

当故障位置和影响范围已经清楚时：

1. 只读取受影响代码、直接调用方和相关测试；
2. 找到根因并做最小修复；
3. 运行针对性验证；
4. 只说明原因、修改和证据。

即使用户显式调用本 skill，局部任务也使用此路径。

### 跨层垂直切片

当任务跨越前端、API、后端、数据层或外部集成，或契约尚不清楚时，读取 [references/fullstack-workflow.md](references/fullstack-workflow.md)，追踪本次功能实际经过的边界并完成整条链路。

## 调查到足够为止

先读取项目级指令和 `git status`，再从受影响入口沿调用关系读取实现、契约、配置与测试。只在需要确认项目约定或版本时读取 README、清单、锁文件、构建文件和迁移。

一旦已经能证实本次修改的调用链、契约和项目约定，就停止扩大项目阅读范围。不要绘制无关模块，也不要借任务顺手重构。

## 遵守变更所有权

- 现有代码拥有业务约定、错误格式、状态与数据模式以及模块边界；沿用它们。
- 框架拥有生命周期、校验、序列化和事务等基础机制；优先使用原生能力。
- 新代码只拥有本次需求明确要求的行为；不要预测未来需求。

按以下顺序选择方案：

> 项目已有模式 → 语言或框架原生能力 → 项目已有依赖 → 局部直接实现 → 新抽象或新依赖

只有至少满足一项时才增加抽象：

1. 已有两个真实消费者；
2. 已存在稳定边界或变化轴；
3. 框架明确要求；
4. 它隔离了有测试覆盖的高风险问题。

否则保留直接实现。涉及新依赖、抽象或高风险设计时，读取 [references/simplicity-and-robustness.md](references/simplicity-and-robustness.md)。简单不等于脆弱：按风险保留必要的校验、权限、事务、并发正确性、错误处理、可观测性、无障碍和可测试性。

## 实现最小完整切片

- 先确定用户可观察结果和验收条件；只有会明显改变产品行为、数据或架构的未决选择才阻塞实现。
- 实现验收条件要求的全部边界，同步更新契约、类型、调用方、迁移与测试。
- 不留下关键路径的伪实现或无说明 TODO，除非用户明确要求原型。
- 保留用户已有和无关修改，遵循项目现有命名、包管理器、格式和工具。
- 对版本敏感或不确定的 API，确认项目版本并查阅对应官方资料；不要把推断写成事实。
- 当更专项的架构、调试、测试、审查或框架 skill 匹配时组合使用，不在此重复技术百科。

## 用最小充分证据验证

- 局部任务：运行能复现并证明修复的针对性测试或检查。
- 跨层任务：验证变更边界，并至少覆盖一条成功链路和相关失败链路。
- 根据风险补充类型检查、静态检查、构建、迁移检查或端到端场景。
- 报告实际命令与结果；无法运行的检查明确说明，绝不写成已通过。

认证授权、事务并发、数据迁移、不可逆操作和外部发布属于高风险动作。执行前展示风险与验证证据，并遵守用户已有授权边界。

## 让结果可追踪

默认交付只解释：

1. 这次改了什么；
2. 请求或数据如何经过受影响链路；
3. 最不显然的一个设计决策及其原因。

另外附上验证证据和剩余风险。用户要求赶进度时进一步压缩措辞，不降低实现与验证标准。

只有用户明确想学习、要求深入讲解或指定学习主题时，才读取 [references/explanation-and-checks.md](references/explanation-and-checks.md)，扩展技术讲解、替代方案、失败预测和理解检查。学习记录只在用户明确同意后写入项目约定位置；不要自动创建文档。

## 完成标准

仅当验收结果已实现、受影响契约一致、相关验证有真实证据、复杂度有现实需求支撑，并且关键链路可被用户追踪时声明完成。
