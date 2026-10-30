# Low-Altitude Benchmark｜低空感知数据集目录

面向小目标检测、多目标跟踪和 RGB–红外感知的组内数据集目录。第一版提供数据集索引、统一填写模板和一名维护者审核的 PR 流程。

**一个数据集一份记录，文件夹负责存放，标签负责分类，首页负责导航。** 所有记录统一放在 `datasets/`，以 YAML 文件为准，不另行维护同内容的 Excel。

## 按任务浏览

### 小目标检测

浏览条件：`tasks` 包含 `object_detection`，且 `tags` 包含 `small_objects`。此标签表示数据集涉及小目标问题，不代表已经完成尺寸分布统计。

| 数据集 | 简短说明 | 记录 |
| --- | --- | --- |
| VisDrone-DET | 无人机视角 RGB 图像中的行人、车辆等目标检测。 | [visdrone-det.yaml](datasets/visdrone-det.yaml) |

### 多目标跟踪

浏览条件：`tasks` 包含 `multi_object_tracking`。

| 数据集 | 简短说明 | 记录 |
| --- | --- | --- |
| VisDrone-MOT | 无人机视角视频中的多目标轨迹恢复。 | [visdrone-mot.yaml](datasets/visdrone-mot.yaml) |

### RGB–红外感知

浏览条件：`modalities` 同时包含 `rgb` 和 `infrared`。

| 数据集 | 简短说明 | 记录 |
| --- | --- | --- |
| DroneVehicle | 无人机视角的 RGB–红外车辆检测。 | [dronevehicle.yaml](datasets/dronevehicle.yaml) |

同一条记录符合多个入口时，在多个入口链接同一个文件，不复制记录。VisDrone-DET 与 VisDrone-MOT 是官方分别发布的图像检测、视频跟踪子集，因此分别建档；同一子集支持多个任务时，直接增加 `tasks` 标签。

## 新增或修改记录

复制 [统一模板](datasets/_template.yaml) → 填写记录 → 提交 PR（合并申请）→ 一名维护者检查并合并。

组员可以在 GitHub 网页完成全部操作，无需安装 Git。具体步骤、字段和标签见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 使用范围

本仓库收录目录信息和官方获取入口。第三方图片、视频、标注文件、模型权重和论文 PDF 不在本仓库分发；下载及使用须遵循原提供方条款。`unknown` 或 `null` 表示信息尚未确认，不表示可以自由使用。

本项目自有内容采用 MIT 许可，适用范围见 [LICENSE](LICENSE)，该许可不覆盖任何第三方数据集。

正式开展评测时，再按实际任务增加 `benchmarks/`，明确数据版本、划分、指标与运行方法。当前不建立评测平台、排行榜或自动化工作流。
