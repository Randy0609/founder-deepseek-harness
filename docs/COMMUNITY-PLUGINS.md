# 社区插件评估（源码与文档阶段）

核查日期：2026-09-23。入口：[GitHub dsh-plugin 主题](https://github.com/topics/dsh-plugin)、[DeepSeek Harness 官方仓库](https://github.com/deepseek-ai/deepseek-harness)。主题标签可由仓库维护者自行添加；它不能证明仓库是原生 DSH 插件、适配当前版本或适合真实业务。

下表只确认公开仓库的 README、根目录 package.json、许可证与 DSH 插件声明。本项目**没有安装、运行、审计这些插件的完整源码，也没有对真实企业数据做测试**。项目描述中的功能属于各自作者的声明。

## 优先调研顺序

| 场景与候选 | 已核到的公开事实 | 建议与尚缺的验证 |
|---|---|---|
| 上下文诊断：[dsh-context](https://github.com/bowenliang123/dsh-context) | [package.json](https://github.com/bowenliang123/dsh-context/blob/main/package.json) 声明 dsh.bundle 与 dsh.client；[README](https://github.com/bowenliang123/dsh-context#readme)描述上下文组成与浏览器。 | **第一批隔离试点候选。**先用合成会话验证界面、版本与停用。它能展示实际上下文内容，需核对谁可查看提示词、工具参数和会话文本。作者列出的兼容版本不等于本机版本已验收。 |
| 企业知识库：[dsh-knowledge](https://github.com/lemoncat7/dsh-knowledge) | [package.json](https://github.com/lemoncat7/dsh-knowledge/blob/main/package.json) 声明 Bundle 与 Web 客户端；[README](https://github.com/lemoncat7/dsh-knowledge#readme)描述本地 SQLite、远程知识服务、检索、知识与笔记写入。 | **合成文档试点候选。**先确认本地数据位置、权限、自动回写、备份与版本升级路径。不要把“知识库已安装”理解为企业文档权限已治理。 |
| 财务工作流：[dsh-finance](https://github.com/zhang787jun/dsh-finance) | [package.json](https://github.com/zhang787jun/dsh-finance/blob/main/package.json) 声明 Bundle；[README](https://github.com/zhang787jun/dsh-finance#readme)列出对账、分录准备、结账、控制测试等工作流和人工审批界限。 | **合成账务样例候选。**可研究流程与校验工具；不承担记账系统、真实凭证批准或报税职责。第三方内容再利用须核对其双许可证与来源声明。 |

## 需要更严格隔离的方向

| 场景与候选 | 已核到的公开事实 | 当前建议 |
|---|---|---|
| 数据分析：[dsh-data-agent](https://github.com/omdsh-dev/dsh-data-agent) | 仓库有 [DSH Bundle 与客户端声明](https://github.com/omdsh-dev/dsh-data-agent/blob/main/package.json)；README 描述连接关系型数据库、生成并执行查询，并建议只读账号/模式。 | **研究与合成数据库试点。**当前 manifest 中多个 DSH peer dependency 指向较早的 alpha 版本，与本项目本机研究基线的兼容性未核。数据库本身必须另设只读账号、表范围和行数限制；不能只依赖插件文字说明。 |
| 商业策略：[dsh-business](https://github.com/winyh/dsh-business) | 仓库 [README](https://github.com/winyh/dsh-business#readme)描述商业模式、定价与盈利能力工具，并写明在 DSH 0.1.5-rc.2 上验证；[package.json](https://github.com/winyh/dsh-business/blob/main/package.json)声明 Bundle。 | **流程设计参考。**本项目个人实例的研究基线为 0.1.5-rc.3，不能把 rc.2 的作者测试外推成 rc.3 兼容。涉及价格与收入承诺应由经营者确认。 |
| 人事招聘：[recruiting-copilot](https://github.com/Viy1204/recruiting-copilot) | [package.json](https://github.com/Viy1204/recruiting-copilot/blob/main/package.json)声明 DSH Bundle 与 Web 客户端；README 描述岗位、简历和招聘网站流程。 | **仅做需求与权限研究。**候选人资料和外部招聘平台操作需要独立授权、隐私与平台规则核查，不进入本项目第一批默认插件。 |

[dsh-lab](https://github.com/hackerFish/dsh-lab)是社区评测与指南仓库，**不是经营插件**。它可以帮助寻找复现报告；任何第三方报告仍需对本项目锁定的 DSH 版本复核。

## 从候选到正式推荐的门槛

1. 核对包的来源、许可证、发布内容和真正的 DSH 装载入口；保留固定版本或提交哈希。
2. 在独立的 DSH Profile 中安装、启动、执行最小任务、停用和回滚，记录准确的 DSH/Node/插件版本。
3. 检查插件实际可读的文件、数据库、网络、凭据和模型上下文；对写入与对外动作另列授权。
4. 用合成数据验证输出的来源、口径、错误处理和可重复性。
5. 通过以上步骤后才把“隔离试点候选”升级为“在该版本已验证”。生产适用性是另一道门槛。

[DSH 官方安全说明](https://github.com/deepseek-ai/deepseek-harness/blob/master/SAFETY.md)明确提醒第三方插件与可访问资源的风险。这里的候选列表不构成安全审计或财务、人事建议。
