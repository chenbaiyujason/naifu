# Naifu 项目文档

## 项目概述

Naifu（又称 naifu-diffusion）是一个强大的生成式模型训练框架，专注于提供灵活、高效的模型训练解决方案。本项目支持多种主流生成式模型的训练，包括 SDXL、语言模型、多模态模型等。

## 特性

- 支持多种模型架构
- 灵活的配置系统
- 高效的数据处理
- 分布式训练支持
- 完整的工具链

## 快速开始

### 安装

```
# 克隆仓库
git clone --depth 1 https://github.com/mikubill/naifu

# 安装依赖
cd naifu
pip install -r requirements.txt
```

### 基本使用

```
# 训练 SDXL 模型
python trainer.py config/train_sdxl.yaml

# 训练语言模型
python trainer.py config/train_general_llm.yaml
```

## 项目结构

```
naifu/
├── modules/           # 核心模型和训练模块
├── data_loader/       # 数据加载和处理
├── utils/            # 工具函数
├── scripts/          # 辅助脚本
├── config/           # 配置文件
├── models/           # 预训练模型
└── docs/            # 文档
```

## 模块说明

### [模型模块](../modules/README.md)

- SDXL 相关模型
- 语言模型
- 多模态模型
- 其他生成模型

### [数据加载模块](../data_loader/README.md)

- Arrow 数据处理
- 数据转换工具
- 数据清洗和处理
- 数据采集工具

### [工具模块](../utils/README.md)

- 模型比较工具
- 文件处理工具
- 辅助功能

## 配置系统

### 配置文件结构

```
# 基本配置结构
trainer:
  seed: 42
  wandb_id: ""
  max_steps: 100000
  
lightning:
  accelerator: "gpu"
  devices: 1
  precision: "16-mixed"
  
model:
  type: "sdxl"
  params:
    # 模型特定参数
    
optimizer:
  type: "adamw"
  params:
    lr: 1e-5
    weight_decay: 0.01
```

### 常用配置文件

- `train_sdxl.yaml`: SDXL 训练配置
- `train_refiner.yaml`: Refiner 训练配置
- `train_general_llm.yaml`: 语言模型训练配置
- `train_clip.yaml`: CLIP 训练配置

## 训练指南

### 1. 数据准备

1. 准备训练数据
2. 转换为 Arrow 格式
3. 数据清洗和预处理

### 2. 配置设置

1. 选择合适的配置文件
2. 调整模型参数
3. 设置训练参数

### 3. 开始训练

1. 运行训练脚本
2. 监控训练过程
3. 保存检查点

## 高级功能

### 分布式训练

支持多种分布式训练策略：
- DDP
- DeepSpeed
- FSDP
- FairScale

### 模型优化

- 梯度累积
- 混合精度训练
- 梯度裁剪
- 权重衰减

### 训练监控

- WandB 集成
- TensorBoard 支持
- 自定义日志记录

## 最佳实践

### 训练技巧

1. 从小批量开始调试
2. 逐步增加模型复杂度
3. 定期保存检查点
4. 监控训练指标

### 性能优化

1. 使用合适的批处理大小
2. 启用混合精度训练
3. 优化数据加载
4. 使用梯度累积

### 故障排除

1. 显存不足
   - 减小批量大小
   - 使用梯度累积
   - 启用梯度检查点

2. 训练不稳定
   - 调整学习率
   - 检查梯度裁剪
   - 验证数据质量

## 常见问题

### Q: 如何选择合适的训练配置？
A: 根据模型类型和硬件资源选择配置，从基础配置开始逐步调整

### Q: 如何处理训练中断？
A: 使用检查点恢复训练，确保定期保存模型状态

### Q: 如何提高训练效率？
A: 优化数据加载，使用混合精度训练，调整批处理大小

## 贡献指南

1. Fork 项目
2. 创建功能分支
3. 提交更改
4. 创建 Pull Request

## 许可证

本项目采用 LICENSE 文件中指定的许可证。

## 联系方式

- GitHub Issues: [项目问题追踪](https://github.com/mikubill/naifu/issues)
- 电子邮件：[项目维护者邮箱] 