# 当前访问网址：https://separate-hip-fonts-golden.trycloudflare.com/NKFCYQ1/

# NKFCYQ - 肝癌多组学数据分析平台

## 项目介绍

NKFCYQ是一个集成肝癌研究相关资源的多组学数据分析平台，涵盖miRNA、基因、甲基化和体细胞突变等多个分子层面的数据和分析工具，为肝癌研究人员提供一站式的数据分析服务。

## 功能模块

平台包含4个核心分析模块，各模块功能如下：

### 1. miRNA分析模块 (NKFCYQ2)
- **miRNA-基因预测**：输入miRNA识别其潜在靶基因
- **基因-miRNA预测**：输入功能基因寻找调控它的miRNA
- **表达分析/配对表达分析**：比较不同样本或配对组间的miRNA表达差异
- **生存分析**：关联miRNA表达水平与患者生存结局
- **ROC分析**：评估miRNA对肝癌的诊断价值

### 2. 单基因分析模块 (NKFCYQ3)
- **相关性分析**：分析目标基因与其他基因的表达相关性
- **表达分析/配对表达分析**：评估不同样本或配对组间的基因表达差异
- **生存分析**：关联基因表达水平与患者生存预后
- **ROC分析**：确定基因作为肝癌诊断标志物的潜力
- **药物敏感性分析**：比较按基因表达分层的各组间的药物敏感性差异
- **免疫浸润分析**：研究按目标基因表达分层的各组间的免疫细胞浸润模式
- **单细胞分析**：探索不同细胞类型中的基因表达模式

### 3. 甲基化分析模块 (NKFCYQ4)
- **基因-CpG映射**：搜索与特定基因相关的CpG甲基化位点
- **表达分析**：分析不同样本/条件下的甲基化水平差异
- **配对表达分析**：比较同一患者的肿瘤组织与癌旁正常组织的甲基化水平
- **生存分析**：研究甲基化水平与患者生存的关联
- **ROC分析**：评估甲基化模式作为肝癌诊断标志物的价值

### 4. 体细胞突变分析模块 (NKFCYQ5)
- **数据概览**：查看体细胞突变数据的简明概述和统计汇总
- **突变位点可视化**：直观展示特定基因内的突变位置
- **生存分析**：分析基因突变状态与生存结局的关联
- **药物-基因相互作用**：查找靶向特定突变基因的药物

## 技术栈

- **开发语言**：R
- **Web框架**：Shiny, Shinydashboard
- **数据处理**：tidyverse, dplyr
- **可视化**：ggplot2
- **机器学习**：mlr3, mlr3learners, mlr3verse, mlr3viz
- **交互组件**：shinybusy

## 环境要求

1. R 4.0+
2. RStudio（推荐）
3. 所需R包：
   - shiny
   - shinydashboard
   - shinybusy
   - tidyverse
   - dplyr
   - ggplot2
   - mlr3
   - mlr3learners
   - mlr3verse
   - mlr3viz

## 安装说明

1. 克隆或下载项目到本地
2. 打开R或RStudio，安装所需依赖包：
```r
install.packages(c("shiny", "shinydashboard", "shinybusy", "tidyverse", "dplyr", "ggplot2", "mlr3", "mlr3learners", "mlr3verse", "mlr3viz"))
```

## 运行方法

### 方式一：运行主平台
进入`NKFCYQ1`目录，运行`app.R`文件：
```r
setwd("NKFCYQ1")
shiny::runApp("app.R")
```

### 方式二：独立运行各分析模块
每个模块可以单独运行：
```r
# 运行miRNA分析模块
setwd("NKFCYQ2")
shiny::runApp("app.R")

# 运行单基因分析模块
setwd("NKFCYQ3")
shiny::runApp("app.R")

# 运行甲基化分析模块
setwd("NKFCYQ4")
shiny::runApp("app.R")
```

## 项目目录结构

```
NKFCYQ/
├── NKFCYQ1/                 # 主门户/介绍页面
│   ├── data/
│   │   └── introduction.Rmd
│   ├── app.R               # 主应用入口
│   └── NKFCYQ1.Rproj
├── NKFCYQ2/                 # miRNA分析模块
│   ├── data/
│   │   └── mirna.Rda
│   ├── app.R               # 模块入口
│   ├── server.R            # 服务器逻辑
│   ├── ui.R                # UI组件
│   ├── functions.R         # 工具函数
│   ├── header.R            # 头部组件
│   ├── sidebar.R           # 侧边栏组件
│   ├── body.R              # 主体内容组件
│   ├── all.R               # 汇总脚本
│   ├── codes_miRNA.R       # miRNA分析相关代码
│   └── NKFCYQMIR.Rproj
├── NKFCYQ3/                 # 单基因分析模块
│   ├── data/
│   │   ├── pq/             # parquet格式数据文件
│   │   ├── DrugPredictions.csv
│   │   ├── HCC_scRNA.rds
│   │   ├── clinical.Rda
│   │   ├── expr.Rda
│   │   └── paired_clinical.csv
│   ├── TCGA_LIHC/
│   │   └── CTRP2_Res.rds
│   ├── app.R               # 模块入口
│   ├── server.R            # 服务器逻辑
│   ├── functions.R         # 工具函数
│   ├── header.R            # 头部组件
│   ├── sidebar.R           # 侧边栏组件
│   ├── body.R              # 主体内容组件
│   ├── all.R               # 汇总脚本
│   ├── codes.R             # 核心分析代码
│   ├── codes_corr.R        # 相关性分析代码
│   ├── anno.rds            # 注释数据
│   ├── bpe.RData
│   ├── hpca.RData
│   └── NKFCYQSG.Rproj
├── NKFCYQ4/                 # 甲基化分析模块
│   ├── data/
│   │   ├── pq/             # parquet格式数据文件
│   │   └── methylation.Rda
│   ├── app.R               # 模块入口
│   ├── server.R            # 服务器逻辑
│   ├── functions.R         # 工具函数
│   ├── header.R            # 头部组件
│   ├── sidebar.R           # 侧边栏组件
│   ├── body.R              # 主体内容组件
│   ├── all.R               # 汇总脚本
│   ├── codes.R             # 核心分析代码
│   └── NKFCYQM.Rproj
└── README.md               # 项目说明文档
```

## 数据文件说明

由于`NKFCYQ3`（单基因分析模块）和`NKFCYQ4`（甲基化分析模块）包含大量parquet格式的组学数据文件，整体体积较大，当前版本未完整上传这两个模块的全部数据文件。如果您需要完整的数据集以运行这两个模块，请通过下方联系方式与我们取得联系。

## 联系方式

如果在使用过程中遇到问题，或有改进建议，欢迎通过以下方式联系我们：
- 邮箱：gongyq@mail.nankai.edu.cn

## 致谢

感谢所有为NKFCYQ平台开发做出贡献的个人和组织。
