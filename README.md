# APH101 预期寿命影响因素统计分析

**English title:** Statistical Analysis of Factors Influencing Life Expectancy  
**Course:** APH101  
**Project type:** 本科课程作业 / 独立统计分析报告  
**Primary tools:** R, ggplot2, linear regression, logistic regression  
**Author:** Yongbo Xia

## 项目概述

本项目研究公共卫生、社会经济状况与人口预期寿命之间的关系。课程提供了世界卫生组织和联合国相关数据，要求学生完成数据检查、探索性数据分析和回归建模，并回答两个核心问题：哪些变量与预期寿命密切相关，以及预期寿命不超过 65 岁的国家可以优先采取哪些改善措施。

我的报告以 2000–2015 年的年度健康数据为背景，并将实证分析聚焦于土库曼斯坦。分析考察了免疫接种、死亡率、医疗支出、营养状况和教育等指标，重点比较 BMI、受教育年限、成人死亡率和政府卫生支出与预期寿命之间的关系。项目同时使用连续结局和二分类结局，使我能够分别练习线性回归与 Logistic 回归，并将统计结果转化为公共卫生建议。

## 课程作业要求

课程原题要求学生：

1. 检查数据中的缺失值和错误记录，并说明清理方法；
2. 在建模前完成探索性数据分析，并使用图形展示变量关系；
3. 建立以预期寿命为连续结局的线性回归模型；
4. 将“预期寿命是否大于 65 岁”定义为二分类结局，并建立 Logistic 回归模型；
5. 展示从候选变量到最终模型的选择和解释过程；
6. 对线性回归模型进行诊断，并讨论模型假设可能存在的偏离；
7. 解释关键变量的实际含义，而不只报告显著性检验结果；
8. 根据模型结果，为预期寿命较低的国家提出可操作的政策建议；
9. 在报告附录中提供生成分析和回归结果的 R 代码。

评分由统计分析、结果解释、报告结构以及表格与图形四部分组成。这意味着作业不仅考察建模是否完成，也重视能否清楚解释模型并有效呈现证据。

## 数据说明

项目数据文件包含 **2,784 条国家—年份记录、174 个国家和 20 个变量**，时间范围为 **2000–2015 年**。变量主要包括：

- **结局变量：** Life Expectancy；
- **人口与死亡指标：** Adult Mortality、Infant Deaths、Under-Five Deaths、HIV/AIDS；
- **免疫与疾病指标：** Hepatitis B、Polio、Diphtheria、Measles；
- **健康与营养指标：** BMI、Alcohol、儿童及青少年消瘦率；
- **经济与社会指标：** Percentage Expenditure、Total Expenditure、Income Composition of Resources、Schooling；
- **背景变量：** Country、Year、Development Status。

原始课程任务面向全部国家数据。我的提交报告在介绍全球数据背景后，将主要图形和回归分析聚焦于土库曼斯坦 2000–2015 年的年度观测，因此报告中的结论更适合被理解为一个国家案例分析，而不是对所有国家的完整跨国因果结论。

## 我的分析过程

### 1 背景研究与问题定义

我首先通过文献回顾梳理了教育、经济发展、医疗支出、疾病负担和环境因素与预期寿命的潜在联系。在此基础上，我把统计问题拆分为两个结局：

- 连续结局：一个国家某年的预期寿命；
- 二分类结局：预期寿命是否大于 65 岁。

这种设计分别对应线性回归和 Logistic 回归，也使分析能够同时关注预期寿命的数值变化和跨越 65 岁阈值的可能性。

### 2 数据检查与处理

我检查了缺失值、异常记录和变量含义，并在报告中采用四分位距方法识别潜在离群值。课程材料建议优先使用同一国家的均值或中位数处理缺失值，在整国某变量均缺失时再参考其他国家的中位数。报告中的分析数据已经过清理，但不同变量的可用年度数并不完全一致，因此各图形和模型的样本量可能略有差异。

### 3 探索性数据分析

我使用 `ggplot2` 绘制散点图，比较预期寿命与多项候选变量之间的关系。探索性分析后，我将以下四个变量作为重点：

- BMI；
- Schooling；
- Adult Mortality；
- Total Expenditure。

图形显示，BMI 和受教育年限与预期寿命总体呈正向关系，成人死亡率与预期寿命呈明显负向关系。卫生支出与预期寿命的关系在该国小样本中不够稳定，需要结合模型结果谨慎解释。

### 4 线性回归

我分别拟合回归模型并加入拟合线，用于估计候选变量与连续预期寿命之间的关联方向。报告对系数符号和显著性进行了文字解释，重点讨论了教育、成人死亡率和 BMI 与预期寿命之间的关系。

### 5 Logistic 回归

我将预期寿命转换为二分类变量：

```text
Life Expectancy > 65 years = 1
Life Expectancy <= 65 years = 0
```

随后使用二项分布和 logit 链接函数建立 Logistic 回归，并对不同变量水平下超过 65 岁的概率进行预测。这部分展示了我从连续结局分析过渡到分类结局建模的能力。

### 6 结果解释与政策建议

提交报告最终将 **BMI、受教育年限和成人死亡率** 视为较重要的关联因素。Total Expenditure 的方向和显著性在不同分析中不够一致，尤其在 Logistic 回归中未表现出稳定的统计证据，因此不应单独据此作出强结论。

结合模型结果和文献背景，我提出的主要建议包括：

- 扩大基础教育和健康教育的可及性；
- 改善儿童和青少年的营养与生活条件；
- 降低可预防的成人死亡风险；
- 加强食品、基本医疗服务和公共卫生资源保障；
- 鼓励资源较充足的国家和机构向低预期寿命地区提供医疗与生活支持。

## 项目结论

该项目的主要价值不在于证明某个单一因素“导致”预期寿命变化，而在于展示如何把一个公共卫生问题转化为可分析的统计问题：先理解变量和数据质量，再通过可视化筛选关系，使用两类回归模型量化关联，最后把统计结果放回现实情境中解释。

在土库曼斯坦案例中，受教育年限较长和较高 BMI 与较高预期寿命相关，而较高成人死亡率与较低预期寿命相关。卫生支出的结果较不稳定，说明仅增加支出并不必然等同于更好的健康结果，支出的配置效率、医疗可及性以及样本范围也可能影响观察到的关系。

## 我在项目中展示的能力

这份作业可以为硕士申请文书提供以下具体证据：

- **统计建模：** 能够根据结局变量的类型选择线性回归和 Logistic 回归；
- **数据意识：** 注意缺失值、异常记录、变量定义和不同变量样本量不一致的问题；
- **数据可视化：** 使用 R 和 ggplot2 探索变量关系并呈现回归趋势；
- **结果解释：** 不只报告系数和 p 值，也尝试解释其公共卫生含义；
- **跨学科思考：** 将统计分析与教育、医疗资源、营养和社会发展问题联系起来；
- **学术写作：** 完成背景、文献回顾、方法、结果、讨论、结论、参考文献和代码附录等完整报告结构；
- **政策转化：** 根据实证结果提出面向低预期寿命国家的干预方向。

## 供文书老师参考的项目表述

### 中文概括

在 APH101 课程项目中，我使用 R 分析了 2000–2015 年的预期寿命与公共卫生指标。以土库曼斯坦为案例，我通过数据检查、散点图、线性回归和 Logistic 回归考察教育、BMI、成人死亡率和卫生支出与预期寿命的关系。这个项目让我认识到，统计分析的价值不仅在于得到显著结果，更在于判断数据质量、选择与研究问题匹配的模型，并将结果转化为谨慎且有现实意义的公共卫生解释。

### English summary

In an APH101 coursework project, I used R to examine the relationship between life expectancy and public-health indicators using data from 2000 to 2015. Focusing my empirical analysis on Turkmenistan, I conducted data checks, exploratory visualization, linear regression, and logistic regression to investigate the roles of schooling, BMI, adult mortality, and health expenditure. The project taught me to connect model choice with the type of outcome, interpret statistical associations in context, and translate quantitative findings into carefully qualified public-health recommendations.

## 使用本项目时需要注意的边界

为保证申请材料准确，建议在简历或文书中将本项目描述为 **coursework project** 或 **independent statistical analysis for a course**，不要表述为已发表研究或完整的全球因果研究。此外：

- 报告的核心实证分析是土库曼斯坦单国案例；
- 多数模型一次考察一个预测变量，不能排除混杂因素；
- 小样本下的显著性、概率预测和异常值处理需要谨慎解释；
- 回归结果说明关联，不直接证明因果关系；
- Total Expenditure 的图形与文字解释存在不完全一致，因此文书中更适合强调教育和成人死亡率等较稳定的发现。

这些限制并不削弱该项目作为统计学习经历的价值，反而能够体现我对模型边界、证据强度和负责任解释的认识。

## 项目文件

| 文件 | 内容 |
| --- | --- |
| `APH101 Coursework.pdf` | 课程作业说明、变量定义和评分标准 |
| `Coursework_Data (1).csv` | 2000–2015 年国家层面的预期寿命与健康指标数据 |
| `Yongbo Xia 2255161 (1).docx` | 提交的完整课程报告，包含文献回顾、分析、图形、讨论、参考文献和 R 代码附录 |

## 技术关键词

`R` · `ggplot2` · `Data Cleaning` · `Exploratory Data Analysis` · `Linear Regression` · `Logistic Regression` · `Public Health` · `Life Expectancy` · `Statistical Interpretation` · `Evidence-Based Recommendations`
