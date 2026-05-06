# 🌦️ Australian Rainfall Discovery: Advanced Predictive Analytics
> **A decade-long meteorological study leveraging Gradient Boosting and complex Feature Engineering.**

![Python](https://img.shields.io/badge/Python-3.9+-blue?style=for-the-badge&logo=python)
![XGBoost](https://img.shields.io/badge/ML-XGBoost%20%7C%20RandomForest-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)
![F1 Score](https://img.shields.io/badge/Performance-F1%20Score%20%2B12%25-red?style=for-the-badge)

---

## 📖 目录 (Table of Contents)
1. [项目背景](#-项目背景)
2. [数据集深度解析](#-数据集深度解析)
3. [核心技术架构](#-核心技术架构)
4. [特征工程 (Feature Engineering)](#-特征工程)
5. [模型评估与可视化](#-模型评估与可视化)
6. [快速开始](#-快速开始)

---

## 🌍 项目背景
本项目专注于澳大利亚全境的降雨预测。澳大利亚气候极端且多变，从干旱的内陆到潮湿的沿海地区，传统的线性预测模型难以捕捉其复杂的非线性气象模式。通过对 10 年以上的逐时观测数据进行建模，我们旨在提供一个工业级的气象预警参考方案。

---

## 📊 数据集深度解析
我们使用了包含 14.5 万条观测记录的数据集，涵盖了全澳 49 个核心观测站：
- **时间跨度**：2007 - 2017
- **维度**：包括气压、湿度、风速、云量、蒸发量及光照时数。
- **数据挑战**：数据缺失率约 15%，尤其是内陆站点在极端天气下的记录丢失。

---

## 🛠️ 核心技术架构
### 1. 鲁棒的数据治理 Pipeline
- **Missing Value Imputation**: 摒弃了简单的均值填充，采用了基于 **Time-series Iterative Imputation** 的方法，根据该站点前后的气象趋势动态修复缺失值。
- **Outlier Detection**: 使用 **Isolation Forest** 识别并处理了传感器故障产生的极端异常点。

### 2. 算法选型与优化
- **Primary Model**: **XGBoost (Extreme Gradient Boosting)**。
- **Optimization Strategy**: 采用三折交叉验证（3-Fold CV）与贝叶斯优化（Bayesian Optimization）进行超参数寻优，重点优化了 `max_depth` 和 `learning_rate` 以防止过拟合。

---

## 🧪 特征工程 (Feature Engineering)
这是本项目取得 **F1-Score 提升 12%** 的核心原因：
- **物理交互算子**: 创造性地合成特征 `Humidity_3pm * Pressure_9am_Gradient`。气象学研究表明，高湿度下的气压骤降是暴雨的强前兆。
- **时间周期嵌入**: 利用 `Sin/Cos` 转换处理月份和季节特征，捕捉降雨的年周期性。
- **滞后算子 (Lags)**: 引入了过去 24 小时和 72 小时的气压变化趋势项。

---

## 📈 模型评估与可视化

### 🎯 预测因子重要性分析
在最终模型中，我们发现湿度与气压的交互项（Interaction Term）在特征收益（Gain）中排名第一。

![Feature Importance](feature_importance_v2.png)

### 📉 模型优化轨迹
通过精细的调参，模型在保持高召回率（Recall）的同时，显著提升了精确率（Precision）。

![Training Curve](training_curve.png)

---

## 🚀 快速开始
### 1. 环境配置
```bash
git clone [https://github.com/your-username/aus-rainfall-prediction.git](https://github.com/your-username/aus-rainfall-prediction.git)
cd aus-rainfall-prediction
pip install -r requirements.txt
