# Config 配置模块文档

## 模块概述

Config 目录包含了项目中所有模型训练的配置文件。这些配置文件使用 YAML 格式，定义了训练参数、模型结构、优化器设置等关键配置。

## 配置文件分类

### 1. SDXL 相关配置

#### 基础配置
- `train_sdxl.yaml`: SDXL 基础训练配置
- `train_sdxl_original.yaml`: SDXL 原始版本配置
- `train_sdxl_adaptive.yaml`: SDXL 自适应训练配置

#### 特殊功能配置
- `train_sdxl_cn.yaml`: SDXL 中文训练配置
- `train_sdxl_ipadapter.yaml`: SDXL IP-Adapter 训练配置
- `train_sdxl_deepspeed.yaml`: SDXL DeepSpeed 训练配置

### 2. 语言模型配置

- `train_general_llm.yaml`: 通用语言模型训练配置
- `train_gpt2.yaml`: GPT-2 模型训练配置
- `train_phi2.yaml`: Phi-2 模型训练配置
- `train_mistral_lora.yaml`: Mistral LoRA 训练配置

### 3. 多模态模型配置

- `train_llava.yaml`: LLaVA 基础版本配置
- `train_llava_1.6.yaml`: LLaVA 1.6 版本配置

### 4. 其他模型配置

- `train_cascade_stage_c.yaml`: Cascade Stage C 训练配置
- `train_pixart.yaml`: PixArt 模型训练配置
- `train_lcm.yaml`: LCM 模型训练配置

## 配置文件结构

### 基本结构示例

```
# 训练器配置
trainer:
  seed: 42                # 随机种子
  wandb_id: ""           # Weights & Biases ID
  max_steps: 100000      # 最大训练步数
  
# Lightning 配置
lightning:
  accelerator: "gpu"     # 加速器类型
  devices: 1             # 设备数量
  precision: "16-mixed"  # 精度设置
  
# 模型配置
model:
  type: "sdxl"          # 模型类型
  params:               # 模型参数
    # 具体参数设置
    
# 优化器配置
optimizer:
  type: "adamw"         # 优化器类型
  params:
    lr: 1e-5            # 学习率
    weight_decay: 0.01  # 权重衰减
```

## 使用指南

### 1. 选择配置文件

根据训练需求选择合适的配置文件：

```
# SDXL 基础训练
python trainer.py config/train_sdxl.yaml

# 使用 DeepSpeed
python trainer.py config/train_sdxl_deepspeed.yaml

# 语言模型训练
python trainer.py config/train_general_llm.yaml
```

### 2. 自定义配置

#### 修改训练参数
```
trainer:
  seed: 42
  max_steps: 50000
  save_every: 5000
  eval_every: 1000
```

#### 修改模型参数
```
model:
  type: "sdxl"
  params:
    hidden_size: 1024
    num_layers: 24
    dropout: 0.1
```

## 配置项说明

### 1. 训练器配置

- `seed`: 随机种子，确保实验可重复性
- `max_steps`: 最大训练步数
- `save_every`: 保存检查点间隔
- `eval_every`: 评估间隔
- `wandb_id`: W&B 项目 ID

### 2. 模型配置

- `type`: 模型类型
- `params`: 模型参数
  - `hidden_size`: 隐藏层大小
  - `num_layers`: 层数
  - `dropout`: Dropout 率

### 3. 优化器配置

- `type`: 优化器类型
- `params`: 优化器参数
  - `lr`: 学习率
  - `weight_decay`: 权重衰减
  - `betas`: Adam 优化器参数

### 4. 数据配置

- `batch_size`: 批处理大小
- `num_workers`: 数据加载线程数
- `shuffle`: 是否打乱数据

## 最佳实践

### 1. 配置选择

- 从基础配置开始
- 逐步调整参数
- 记录实验结果

### 2. 资源管理

- 根据硬件调整批大小
- 选择合适的精度设置
- 优化内存使用

### 3. 训练优化

- 使用学习率预热
- 实现梯度累积
- 启用混合精度训练

## 常见问题

### Q: 如何选择合适的学习率？
A: 从小学习率开始，使用学习率查找器确定最佳值

### Q: 如何处理显存不足？
A: 减小批大小，使用梯度累积，选择合适的精度设置

### Q: 如何提高训练效率？
A: 使用 DeepSpeed/FSDP，优化数据加载，调整批处理大小 