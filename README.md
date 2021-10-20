[TOC]

------

# 人类皮肤、口腔和肠道微生物组预测实际年龄

本研究对来自多个身体部位（肠道、口腔和皮肤）的人类微生物群进行了随机森林回归分析。 该存储库提供了用于生成手稿中所有结果的所有源数据和代码。 此外，在输出目录中，我们还提供了额外的探索性分析结果，以更好地了解我们基于微生物群的年龄预测模型。 

- Huang S, Haiminen N, Carrieri A-P, Hu R, Jiang L, Parida L, Russell B, Allaband C, Zarrinpar A, Vázquez-Baeza Y, Belda-Ferre P, Zhou H, Kim H-C, Swafford AD, Knight R, Xu ZZ. 2020. Human skin, oral, and gut microbiomes predict chronological age. mSystems 5:e00630-19. https://doi.org/10.1128/mSystems.00630-19.



# 数据来源

## meta-analysis 中涉及到的 Qiita study IDs  :

- 肠道微生物组:

| QIITA Study ID                                          | EBI accession ID | Project name            | Publication(s)                                               | # of samples involved |
| ------------------------------------------------------- | ---------------- | ----------------------- | ------------------------------------------------------------ | --------------------- |
| [10317](https://qiita.ucsd.edu/study/description/10317) | ERP012803        | American Gut Project    | [American Gut: an Open Platform for Citizen Science Microbiome Research](https://msystems.asm.org/content/3/3/e00031-18) | 2770                  |
| [11757](https://qiita.ucsd.edu/study/description/11757) | PRJEB18535       | GGMP regional variation | [Regional variation greatly limits application of healthy gut microbiome reference ranges and disease models](https://www.nature.com/articles/s41591-018-0164-x) | 1609                  |

- 口腔微生物组:

| QIITA Study ID                                          | EBI accession ID                | Project name                            | Publication(s)                                               | # of samples involved |
| ------------------------------------------------------- | ------------------------------- | --------------------------------------- | ------------------------------------------------------------ | --------------------- |
| [10317](https://qiita.ucsd.edu/study/description/10317) | ERP012803                       | American Gut Project                    | [American Gut: an Open Platform for Citizen Science Microbiome Research](https://msystems.asm.org/content/3/3/e00031-18) | 547                   |
| [1841](https://qiita.ucsd.edu/study/description/1841)   | PRJEB5726, PRJEB5727, PRJEB5728 | Flores_SMP                              | [Temporal variability is a personalized feature of the human microbiome](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4252997/) | 642                   |
| [550](https://qiita.ucsd.edu/study/description/550)     | ERP021896                       | Moving pictures of the human microbiome | [Moving pictures of the human microbiome](https://genomebiology.biomedcentral.com/articles/10.1186/gb-2011-12-5-r50) | 508                   |
| [1774](https://qiita.ucsd.edu/study/description/1774)   | ERP016472                       | Puerto Rico and Plantanal               | NA                                                           | 48                    |
| [2010](https://qiita.ucsd.edu/study/description/2010)   | ERP012216                       | Longitudinal babies project             | [Partial restoration of the microbiota of cesarean-born infants via vaginal microbial transfer](https://www.nature.com/articles/nm.4039) | 72                    |
| [2024](https://qiita.ucsd.edu/study/description/2024)   | ERP016621                       | TZ_probiotic_pregnancy_study            | [Microbiota at Multiple Body Sites during Pregnancy in a Rural Tanzanian Population and Effects of Moringa-Supplemented Probiotic Yogurt](https://aem.asm.org/content/81/15/4965) | 254                   |
| [2202](https://qiita.ucsd.edu/study/description/2202)   | PRJEB6518                       | mit_daily_timeseries                    | [Host lifestyle affects human microbiota on daily timescales](https://genomebiology.biomedcentral.com/articles/10.1186/gb-2014-15-7-r89) | 285                   |
| [10052](https://qiita.ucsd.edu/study/description/10052) | ERP008799, ERP008694            | Yanomani 2008                           | [The microbiome of uncontacted Amerindians](https://advances.sciencemag.org/content/1/3/e1500183) | 16                    |
| [11052](https://qiita.ucsd.edu/study/description/11052) | ERP021896                       | Knight_ABTX                             | NA                                                           | 178                   |

- 皮肤微生物组:

| QIITA Study ID                                          | EBI accession ID                | Project name                | Publication(s)                                               | # of samples involved |
| ------------------------------------------------------- | ------------------------------- | --------------------------- | ------------------------------------------------------------ | --------------------- |
| [10317](https://qiita.ucsd.edu/study/description/10317) | ERP012803                       | American Gut Project        | [American Gut: an Open Platform for Citizen Science Microbiome Research](https://msystems.asm.org/content/3/3/e00031-18) | 440                   |
| [11052](https://qiita.ucsd.edu/study/description/11052) | ERP021896                       | Knight_ABTX                 | NA                                                           | 177                   |
| [2010](https://qiita.ucsd.edu/study/description/2010)   | ERP012216                       | Longitudinal babies project | [Partial restoration of the microbiota of cesarean-born infants via vaginal microbial transfer](https://www.nature.com/articles/nm.4039) | 65                    |
| [1841](https://qiita.ucsd.edu/study/description/1841)   | PRJEB5726, PRJEB5727, PRJEB5728 | Flores_SMP                  | [Temporal variability is a personalized feature of the human microbiome](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4252997/) | 1293                  |



## 肠道、口腔和皮肤数据集中所有样本的年龄分布:

![img](https://raw.githubusercontent.com/shihuang047/age-prediction/master/age_distribution.png)

尽管皮肤或口腔微生物群数据集中的年龄分布偏斜可能会降低老年人年龄预测的准确性，但不会影响关于不同人类微生物群预测年龄的相对能力的结论。



# R scripts

这个存储库中有一些 R 脚本和文件也用于准备手稿的过程。 在这里，我将尝试解释其中的一些。 



## 使用要求和依赖项

此 meta-analysis 依赖于自行开发的 R 包 `crossRanger`，可下载如下。

```
## install.packages('devtools') # if devtools not installed
devtools::install_github('shihuang047/crossRanger')
```



## R 脚本 `Age.crossRF_reg.ranger.R` 做了哪些分析？ 

R 脚本 `Age.crossRF_reg.ranger.R` 执行微生物组数据的 meta-analysis 以预测实际年龄。 对于每个数据集（即肠道、口腔或皮肤），该脚本可以执行如下分析。 

- 数据修整（例如按 metadata 中的 NA 值进行样本过滤）。 
- 整个数据集的 RF 建模和性能评估。 
- 子数据集的 RF 建模和性能评估。 
- 为了测试混杂因素（例如性别）是否影响建模，我们首先在由混杂因素分层的子数据集中训练年龄模型，然后将其应用于所有其他子数据集。 对于模型训练和测试，我们使用平均绝对误差 (MAE) 评估回归性能。
-  基于子数据集的 RF 模型的交叉应用，并使用 MAE 评估性能。

通常可以在 Rstudio 或 R concole 中使用此脚本进行所有分析。 



## 这个 R 脚本需要哪些输入？ 

| Input              | gut_data                  | oral_data                   | skin_data                       | Description                                    |
| ------------------ | ------------------------- | --------------------------- | ------------------------------- | ---------------------------------------------- |
| `datafile`         | gut_data/gut_4434.biom    | oral_data/oral_4014.biom    | skin_data/skin_4168.biom        | Biom-table file                                |
| `sample_metadata`  | gut_data/gut_4434_map.txt | oral_data/oral_2550_map.txt | skin_data/skin_1975_map.txt     | Metadata file                                  |
| `feature_metadata` | gut_data/gut_taxonomy.txt | oral_data/oral_taxonomy.txt | skin_data/skin_taxonomy.txt     | Feature metadata file                          |
| `prefix_name`      | gut_4434                  | oral_2550                   | skin_1975                       | The prefix of datasets                         |
| `s_category`       | c("cohort", "sex")        | "qiita_host_sex"            | c("body_site","qiita_host_sex") | The metadata category for dividing datasets    |
| `c_category`       | "age"                     | "qiita_host_age"            | "qiita_host_age"                | The targeted metadata category for RF modeling |



# 关于 `Input/` 文件夹

该文件夹包含 RF 回归分析所需的所有输入文件（biom表、样本metadata和特征metadata文件）。 



# 关于 `Output/` 文件夹

此文件夹包含主 R 脚本 `Age.crossRF_reg.ranger.R`  的所有输出文件 。



