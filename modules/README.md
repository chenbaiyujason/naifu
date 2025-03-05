# Modules 模块文档

## 模块概述

本目录包含了 Naifu 项目的训练脚本和工具模块。主要分为以下几个类别：

### 1. SDXL 训练脚本

#### 基础训练脚本
- `train_sdxl.py`: SDXL 基础训练脚本
- `train_sdxl_hezi.py`: SDXL 盒子训练版本
- `train_sdxl_edm.py`: SDXL EDM 训练版本
- `train_sdxl_original.py`: SDXL 原始版本训练脚本

#### 特殊训练脚本
- `train_sdxl_cn_hezi_deepspeed.py`: 中文版本 DeepSpeed 训练
- `train_sdxl_hezi_ipadapter.py`: IP-Adapter 训练
- `train_sdxl_hezi_ipadapter_face.py`: 人脸 IP-Adapter 训练

### 2. 语言模型训练脚本

- `train_general_llm.py`: 通用语言模型训练
- `train_gpt2.py`: GPT-2 模型训练
- `train_phi.py`: Phi 模型训练

### 3. 多模态模型训练脚本

- `train_clip.py`: CLIP 模型训练
- `train_llava.py`: LLaVA 模型训练

### 4. 其他生成模型训练脚本

- `train_pixart.py`: PixArt 模型训练
- `train_cascade_stage_c.py`: Cascade Stage C 训练
- `train_lcm.py`: LCM 模型训练

### 5. 工具和辅助模块

- `scheduler_utils.py`: 调度器工具
- `sdxl_utils.py`: SDXL 相关工具函数

## 使用示例

### SDXL 训练

```python
# 基础 SDXL 训练
python trainer.py config/train_sdxl.yaml

# 使用 DeepSpeed
python trainer.py config/train_sdxl_hezi_deepspeed.yaml

# 使用 IP-Adapter
python trainer.py config/train_sdxl_hezi_ipadapter.yaml
```

### 语言模型训练

```python
# 通用语言模型训练
python trainer.py config/train_general_llm.yaml

# GPT-2 训练
python trainer.py config/train_gpt2.yaml
```

## 开发指南

### 添加新训练脚本

1. 创建训练脚本文件
2. 实现训练循环
3. 添加配置文件
4. 更新文档

### 代码规范

- 使用类型注解
- 添加详细注释
- 实现进度显示
- 错误处理

## 最佳实践

### 1. 训练流程
- 数据加载和预处理
- 模型初始化
- 优化器配置
- 训练循环
- 检查点保存

### 2. 性能优化
- 使用混合精度训练
- 实现梯度累积
- 优化数据加载
- 内存管理

## 常见问题

### Q: 如何选择合适的训练配置？
A: 根据模型类型和硬件资源选择配置，从基础配置开始逐步调整

### Q: 如何处理训练中断？
A: 使用检查点恢复训练，确保定期保存模型状态

### Q: 如何提高训练效率？
A: 优化数据加载，使用混合精度训练，调整批处理大小 