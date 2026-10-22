# 雅思写作评分准确度基准：五个平台 × 97 篇官方评分作文

[English](README.md)

我们找了 97 篇雅思写作，它们的官方总分都由 IELTS.org、Official IELTS Practice Materials 或剑桥雅思公开过，然后记下五个评分平台各自给出的总分。这里公开了每一篇的分数，[基准测试文章](https://ieltswritingpractice.app/zh/blog/ielts-writing-scoring-accuracy-benchmark/)里的每个数字都可以拿它核对、自己重算。

数据由 [IELTS Writing Practice](https://ieltswritingpractice.app/zh/) 发布，我们自己也是被比较的五个平台之一。正因为如此，我们把原始分数全部公开，读者不必只相信我们的总结。

## 97 篇整体结果

| 平台 | 平均绝对误差 | 平均偏差 | 误差 ≤0.5 分 | 误差 ≤1 分 | 误差超过 1 分 |
|---|---|---|---|---|---|
| IELTS Writing Practice | 0.53 | -0.27 | 74.2%（72/97） | 93.8%（91/97） | 6 |
| IELTSWritingChecker.org | 0.57 | -0.38 | 70.1%（68/97） | 86.6%（84/97） | 13 |
| ChatGPT | 0.88 | -0.85 | 46.4%（45/97） | 76.3%（74/97） | 23 |
| Engnovate | 0.94 | -0.86 | 39.2%（38/97） | 73.2%（71/97） | 26 |
| Writing9 | 1.72 | -1.58 | 19.6%（19/97） | 35.1%（34/97） | 63 |

IELTS Writing Practice 的平均绝对误差比 IELTSWritingChecker.org 低 0.036 分（前者减后者为 -0.036）。配对 bootstrap 的 95% 区间是 -0.119 到 +0.046，包含 0，所以在这个样本量下两者分不出高下。这两家都明显比 ChatGPT、Engnovate 和 Writing9 更接近官方分。按任务、模块、来源和剑雅 20/21 子集的拆分，以及两两比较，见 [`results/metrics.md`](results/metrics.md)。

## 文件

| 路径 | 内容 |
|---|---|
| `data/scores.csv` | 每篇一行：来源、出处定位、官方分、五个平台的分数 |
| `scripts/compute_metrics.py` | 从 CSV 重算全部指标（Python 3，只用标准库） |
| `results/metrics.md`、`results/metrics.json` | 脚本输出 |

各列含义见英文 README。Writing9 显示低于 4 分（`<4`）时，`writing9` 列按 3.5 计，记录下来的原值另存在 `writing9_displayed` 列。

## 方法

- **参照分**：每篇作文公开的官方总分。不比较四项小分。
- **采集**：每个平台对每篇作文（连同题目）记录一个分数，全部分数在 2026 年 8 月 30 日前采集完毕；平台接受 Task 1 图表时一并提供。平台给出的总分原样记录。题目和作文文本是从原始资料转录的，不同平台之间可能有细微的转录差异。
- **对应关系**：Writing9 和 Engnovate 的分数记录在一张按来源排序的表里，只有剑雅 20/21 的行写明了书号、Test 和 Task。其余行按来源顺序对应到作文 ID：录表的人已确认，表里每组的行就是按资料原顺序录入的；每一行的任务类型和官方分也都与对应结果一致。
- **Writing9**：它的公开流程不接受学术类 Task 1 的图表；显示 `<4` 时按 3.5 计，即该区间的上限。

## 局限

- 97 篇样本不大。平均绝对误差相差约 0.1 分以内的平台，这份数据无法可靠区分。
- 每个平台对每篇只评了一次，重复评分结果可能不同。
- 分数反映的是各平台截至 2026 年 8 月 30 日的状态。此后五个产品（包括 IELTS Writing Practice）都可能有变化。
- 较早公开的作文可能出现在模型训练数据里。剑雅 20/21 子集降低了这种风险，但不能排除。
- 自动评分是估计，不是官方雅思成绩。

作文原文、题目、图表和考官评语的版权属于各出版方，这里不收录。可以用 `source` 和 `locator` 两列找到原文。

## 许可与引用

数据（`data/`、`results/`）采用 [CC BY 4.0](LICENSE-DATA)，代码采用 [MIT](LICENSE-CODE)。引用方式见英文 README。问题与勘误：support@ieltswritingpractice.app
