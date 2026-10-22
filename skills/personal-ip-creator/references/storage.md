# 配置、资产与版本

## 位置与目录

首次使用时确认用户希望采用的资产库位置；如本次已有明确路径则直接沿用，不重复询问。把路径记入当前项目根目录的 `personal-ip-library.json`，以后读取该配置；没有项目时由用户确定该配置的保存位置。技能代码不保存个人照片或角色数据，重装技能不应抹掉资产。多个项目可显式指向同一资产库。

运行配置最小形式：`{"schema_version":1,"library_root":"用户确认的绝对路径"}`。该文件在真正建立资产库时写入，不在安装时虚构一个用户已批准的库。

资产库结构（有实际内容才创建对应目录）：

```text
<library_root>/
  registry.json
  <ip_id>/
    sources/                     持久保存的实际输入，含来源和用途记录
    drafts/<draft_id>/            访谈、预览、待确认设定、候选图
    versions/<version>/          确认后的profile.json、档案、规范、四视图、细节图
    application-references/      index.json及明确获准作为参考的作品
    works/<work_id>/             request.json、提示词、候选图、结果、review.json
```

`registry.json` 使用 `schema_version` 和 `ips` 数组，每项含 `name`、`ip_id`、`directory`、`current_version`、`drafts`。首次创建没有正式版时 `current_version` 为 null。名称是用户调用键，ip_id是稳定目录标识；如名称含非法路径字符，保留原显示名并采用安全目录标识，不静默重命名IP。检测路径穿越，保存路径须位于确认的库内。

名称重名时让用户选继续草稿、更新原IP或新名称，不覆盖、不自动加编号。名称未命中或有歧义时澄清，不猜角色。引用资源缺失时查本IP已登记路径，找不到则报告，不声称看过。

## 角色配置字段

`profile.json` 使用 schema_version: 1，字段如下。字段未确定用 null 或待确认说明，不填造假的最终值。

| 字段 | 内容 |
| --- | --- |
| name / ip_id / version / status | 名称、标识、版本、draft或approved |
| source_mode | original或photo_transform |
| positioning | 受众、主题、角色关系 |
| personality / behavior | 性格及具体表现习惯 |
| style | family为animation_chibi，记录画风描述；未来扩展需升级规范，不自动开放其他风格 |
| identity | 固定脸部、发型等识别特征 |
| proportion | preset、target、range、躯干四肢描述、baseline_asset；新角色默认semi-chibi/2.8/[2.695,2.995]，正式版沿用确认值 |
| default_appearance | 默认服装、配色、物件 |
| variation_rules | 允许临时变化及需永久更新的边界 |
| signature_items | 标志物结构、位置、佩戴规则及对应细节图；无则空数组 |
| references | 资产路径、来源、roles、采用与排除特征、关联IP版本 |
| deliverables | 档案、规范、四视图、适用细节、总览路径 |
| approval | 完整资料确认的时间、用户原话／可定位消息及确认范围；草稿为null |

资产路径相对库根目录保存，移库后统一解析；用户界面输出实际绝对路径链接。引用关系必须存在，配置不是资产本身的替代品。

草稿另存 `progress.json`：当前阶段、已确认结论、待答问题、下一步、预览与检查结果。逐步保存便于恢复，不要求用户重复已回答内容。

## 正式发布与更新

完整设定图和配置通过检查并获用户明确确认后，先写入新的版本目录并验证引用完整，再更新registry.current_version。旧版保持可读。中途失败保留草稿和原默认版本，不留下指向半成品的默认指针。

永久修改沿用ip_id建立新草稿，保存来源版本，确认后发布新版本；普通场景变化只记本次request。作品始终绑定生成时版本，不随默认指针变化改写历史。

## 本次任务记录

`request.json` 保存：work_id、IP名称和版本、用途、主题、数量、准确文字、requested_output（精确宽高或比例、透明要求）、场景与情绪描述、临时变化、所选参考及roles、本次需保留内容、批量清单及样张确认（适用时）。

同时保存实际提示词、实际可获取的工具／模型信息、每次尝试结果、provider_output和final_output实际尺寸、质量检查及未解决项。不得猜测工具未暴露的参数。反馈变更保留旧记录并记录变更原因，不静默覆写任务历史。

普通作品与应用参考分开：用户喜欢结果不自动代表允许长期引用。明确同意作为参考后才登记至application-references/index.json，记录源作品、IP版本、用途、路径和确认依据；保留源文件。后续IP更新时检查旧参考是否冲突，不无差别继承。应用参考不能修改正式身份。
