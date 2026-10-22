# Personal IP Creator · 个人 IP 创作

一个用于创建动画／Q版人类个人 IP，并持续生成一致静态内容的 Codex 技能。支持多个命名角色，内置自适应访谈，无需安装 grill-me。

## 两个独立环节

1. **创建 IP**：梳理定位与外观，选择原创或照片转化，确认预览后制作中性站姿四视图、适用的标志性物件细节、视觉规范与调用配置。用户确认完整设定后保存并停止。
2. **调用 IP**：用户指定已保存角色名称，生成头像、表情、正文配图、海报、封面等静态内容；按任务选择参考，并记录所用角色版本。

新角色默认约2.8头身，用户要求优先。正式设定、应用参考、普通作品分开保存；旧版本保留。初版不包含动态内容或外部已有IP导入。

## 安装

下载本仓库，将 `skills/personal-ip-creator` 整个文件夹复制到 Codex 技能目录：

- Windows：`%USERPROFILE%\.codex\skills\personal-ip-creator`
- macOS／Linux：`~/.codex/skills/personal-ip-creator`
- 配置了自定义 `CODEX_HOME` 时，使用其下的 `skills` 目录。

不要只复制 SKILL.md，需一并保留 references 和 agents。安装后在新会话中调用。需要运行环境提供图像生成／编辑能力；技能本身不捆绑模型、API密钥或图像服务。

## 使用示例

```text
使用 $personal-ip-creator，创建一个名为“小禾”的个人IP，
面向刚开始学习AI的上班族。采用原创角色，没有参考图。
```

完成并确认角色设定后：

```text
使用 $personal-ip-creator，用“小禾”画一张16:9配图，
表现AI整理学习笔记前后的变化，不加文字。
```

正文配图、封面、海报请提供尺寸或比例。明确的单张需求直接生成，批量先确认清单与样张。首次使用时确认资产库位置；角色配置、参考照片与作品存入独立资产库，不放入技能目录。

## 文档

- [技能入口](skills/personal-ip-creator/SKILL.md)
- [使用说明](docs/个人IP创作技能-使用说明.md)
- [完整流程约定](docs/IP创作Skill-流程约定.md)
- [创建流程](skills/personal-ip-creator/references/create.md)
- [内容生成](skills/personal-ip-creator/references/content.md)
- [图像验收](skills/personal-ip-creator/references/quality.md)
- [配置与保存](skills/personal-ip-creator/references/storage.md)

## 验证与参考

已完成技能格式、本地链接和部署一致性检查；尚未进行完整的图像生成实测。输出一致性与精确尺寸能力取决于实际图像工具和验收结果。

流程设计参考了 [deepseek-whalechan](https://github.com/ColinLiu1117/deepseek-whalechan) 的参考图职责、比例、提示词和验收思路。本仓库不包含其角色图片，也不包含个人照片、角色作品或本地资产库配置。
