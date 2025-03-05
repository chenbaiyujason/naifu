# Modules 模块文档

## 模块概述

本目录包含了 Naifu 项目的核心模型和训练模块。主要分为以下几个类别：

### 1. SDXL 相关模块

#### 基础模型
- `sdxl_model.py`: SDXL 基础模型实现
- `sdxl_model_cn.py`: SDXL 中文版本模型实现
- `sdxl_model_diffusers.py`: 基于 Diffusers 的 SDXL 模型实现
- `sdxl_model_ipadapter.py`: SDXL IP-Adapter 模型实现

#### 训练脚本
- `train_sdxl.py`: SDXL 基础训练脚本
- `train_sdxl_hezi.py`: SDXL 盒子训练版本
- `train_sdxl_edm.py`: SDXL EDM 训练版本
- `train_sdxl_original.py`: SDXL 原始版本训练脚本

### 2. 语言模型相关

- `train_general_llm.py`: 通用语言模型训练
- `train_gpt2.py`: GPT-2 模型训练
- `train_phi.py`: Phi 模型训练

### 3. 多模态模型

- `train_clip.py`: CLIP 模型训练
- `train_llava.py`: LLaVA 模型训练
- `clip_model.py`: CLIP 模型实现

### 4. 其他生成模型

- `train_pixart.py`: PixArt 模型训练
- `train_cascade_stage_c.py`: Cascade 模型 Stage C 训练
- `train_lcm.py`: Latent Consistency Model 训练

### 5. 优化和工具

- `scheduler_utils.py`: 调度器工具
- `sdxl_utils.py`: SDXL 相关工具函数

## 主要功能说明

### SDXL 模型 (sdxl_model.py)

核心功能：
- UNet 模型定义和实现
- 条件编码器集成
- 损失函数计算
- 训练循环控制

### 训练器模块

所有训练脚本都遵循以下基本结构：
1. 数据加载和预处理
2. 模型初始化
3. 优化器配置
4. 训练循环
5. 检查点保存

### 配置系统

- `config_sdxl_base.py`: SDXL 基础配置
- `config_sdxl_refiner.py`: SDXL Refiner 配置

## 使用示例

### SDXL 训练

```
# 基础 SDXL 训练
python trainer.py config/train_sdxl.yaml

# 使用 DeepSpeed
python trainer.py config/train_sdxl_hezi_deepspeed.yaml

# 使用 IP-Adapter
python trainer.py config/train_sdxl_hezi_ipadapter.yaml
```

### 语言模型训练

```
# 通用语言模型训练
python trainer.py config/train_general_llm.yaml

# GPT-2 训练
python trainer.py config/train_gpt2.yaml
```

## 开发指南

### 添加新模型

1. 创建模型定义文件（例如：`new_model.py`）
2. 创建对应的训练脚本（例如：`train_new_model.py`）
3. 添加配置文件到 `config` 目录
4. 更新文档

### 代码规范

- 所有模型类都应继承自 `torch.nn.Module`
- 训练脚本应遵循统一的接口规范
- 必须包含详细的类型注解
- 关键函数需要添加文档字符串 