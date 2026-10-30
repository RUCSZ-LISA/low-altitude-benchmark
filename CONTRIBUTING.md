# 如何提交数据集记录

## 四条规则

1. **新增前先查重。** 搜索 `datasets/` 中的数据集名称、别名、官方链接和论文链接。已有记录就修改原文件；同一数据集支持多个任务时填写多个 `tasks` 标签，不按浏览方向复制。只有官方独立发布的子集才可分别记录，并在 `notes` 中说明关系。
2. **统一命名和标签。** 文件名和 `id` 一致，使用小写英文、数字和连字符，例如 `visdrone-det.yaml`；优先使用下面已有的标签。`_template.yaml` 是模板，不算数据集记录。字段不确定时填写 `unknown` 或 `null`，不猜测。
3. **只提交目录信息。** 填写官方获取入口、论文入口与许可依据，不上传第三方图片、视频、标注文件、模型权重和论文 PDF。代码仓库或论文的许可不自动等于数据集许可，不能据此推定数据可商用或可再分发。
4. **修改经过审核。** 新增和修改均通过 PR，由一名维护者检查重复、来源、分类和未知项后合并。提交者不自行合并自己的 PR；有需澄清的信息就在同一个 PR 内补充。

## 用 GitHub 网页提交

1. 打开 [datasets/_template.yaml](datasets/_template.yaml)，复制模板内容；修改已有记录则直接打开对应 YAML 文件。
2. 回到 `datasets/`，选择 **Add file → Create new file**，输入文件名并粘贴模板；修改已有记录时点击铅笔按钮。
3. 按下面的字段说明填写，点击 **Commit changes…**，选择 **Create a new branch for this commit and start a pull request**，给分支起名，例如 `add-uavdt`。
4. 创建 PR，在描述中说明新增或修改了什么、依据的官方链接，以及哪些信息仍未知。如果本次新增记录，也在同一分支修改 README 中符合条件的浏览入口，只添加名称、简短说明和记录链接。
5. 一名维护者检查并合并；需要修改时继续编辑同一分支，PR 会自动更新。审核未通过前保持 PR 打开。

没有写入权限时，GitHub 可能引导你先 Fork 再发 PR；私有仓库需要先由负责人授予适当访问权限。

网页操作依据：[GitHub 官方新建文件说明](https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files)。

## 字段与已有标签

| 字段 | 填写方式 |
| --- | --- |
| `id` | 稳定的唯一标识，与文件名去掉 `.yaml` 后相同。 |
| `name` | 官方名称；有常用别名可写在 `notes`。 |
| `version` | 官方数据版本，按字符串填写，例如 `"2019"`；未确认填 `unknown`，不把论文年份当成数据版本。 |
| `tasks` | 任务列表；已有值：`object_detection`、`multi_object_tracking`。 |
| `modalities` | 输入模态列表；已有值：`rgb`、`infrared`。 |
| `viewpoint` | 从哪里看：`uav_view`（无人机机载视角）、`ground_view`（地面相机视角）、`mixed` 或 `unknown`。 |
| `targets` | 看什么：优先使用 `vehicle`、`pedestrian`、`bicycle`、`motorcycle`、`tricycle`、`uav`。这是便于检索的目标大类，不替代官方类别定义。 |
| `tags` | 补充特征；已有值：`small_objects`、`video`、`cross_modal`、`oriented_boxes`。无补充标签填 `[]`。 |
| `official_url` | 官方网站或作者官方仓库 URL；未知填 `null`。 |
| `paper_url` | 原始论文或作者预印本 URL；未知填 `null`。 |
| `license.name` | 明确覆盖数据及标注的许可名称；未找到可确认的声明填 `unknown`。 |
| `license.source_url` | 直接支持许可名称的官方条款链接；没有找到填 `null`，不要把无条款的下载页当作许可证明。 |
| `notes` | 简短说明来源、子集关系、官方类别映射、已确认限制或待核实项；无备注填 `""`。 |

列表信息未知时填 `[unknown]`；链接未知时填 `null`，不要写成字符串 `"null"`。确有必要使用新标签时，在同一 PR 中解释并补充本表。暂不强制填写尺寸分布、遮挡比例、划分统计或基线结果；实际下载核验后，再经 PR 补充必要字段及其来源。

`viewpoint` 与 `targets` 独立填写：无人机拍摄车辆写 `viewpoint: uav_view`、`targets: [vehicle]`；地面相机检测无人机写 `viewpoint: ground_view`、`targets: [uav]`。

## 维护者审核

主要维护者由仓库负责人担任，负责日常审核；备用维护者由负责人指定一名组员，主要维护者不便处理或提交者本人就是主要维护者时，由备用维护者审核。

每个 PR 只需一名维护者完成以下检查：

- [ ] 没有重复记录，文件名与 `id` 一致。
- [ ] 官方入口与论文来源明确，许可未被误推断。
- [ ] 任务、模态、视角与目标类别正确；README 入口链接指向同一份记录。
- [ ] 未知项如实标注；YAML 缩进、列表和链接可读，没有混入第三方数据文件。

初期采用人工审核约定；如尚未配置 GitHub 分支保护，该约定不构成技术上的强制拦截。
