# Modules 模块文档

## 目录概述

本目录包含了 Naifu 项目的训练脚本和工具模块，按照不同模型类型进行组织。

## 目录结构

```
modules/
├── sdxl/                # SDXL 相关训练脚本
│   ├── __init__.py
│   ├── train_sdxl.py                    # 基础训练脚本
│   ├── train_sdxl_hezi.py               # 盒子训练版本
│   ├── train_sdxl_edm.py                # EDM 训练版本
│   ├── train_sdxl_original.py           # 原始版本训练
│   ├── train_sdxl_cn_hezi_deepspeed.py  # 中文版本 DeepSpeed
│   ├── train_sdxl_hezi_ipadapter.py     # IP-Adapter 训练
│   └── train_sdxl_hezi_ipadapter_face.py # 人脸 IP-Adapter
├── llm/                 # 语言模型训练脚本
│   ├── __init__.py
│   ├── train_general_llm.py             # 通用语言模型
│   ├── train_gpt2.py                    # GPT-2 训练
│   └── train_phi.py                     # Phi 模型训练
├── clip/                # CLIP 训练脚本
│   ├── __init__.py
│   └── train_clip.py                    # CLIP 模型训练
├── pixart/             # PixArt 训练脚本
│   ├── __init__.py
│   ├── train_pixart.py                  # 基础训练脚本
│   └── train_pixart_sigma.py            # Sigma 版本训练
├── cascade/            # Cascade 训练脚本
│   ├── __init__.py
│   └── train_cascade_stage_c.py         # Stage C 训练
├── llava/              # LLaVA 训练脚本
│   ├── __init__.py
│   └── train_llava.py                   # LLaVA 模型训练
└── utils/              # 工具函数
    ├── __init__.py
    ├── scheduler_utils.py               # 调度器工具
    └── sdxl_utils.py                    # SDXL 工具函数
```

## 模块说明

### 1. SDXL 训练模块 (sdxl/)
- 基础和高级 SDXL 训练实现
- 支持中文、IP-Adapter 等特殊版本
- DeepSpeed 分布式训练支持

### 2. 语言模型训练模块 (llm/)
- 通用语言模型训练框架
- GPT-2 专用训练脚本
- Phi 模型训练支持

### 3. CLIP 训练模块 (clip/)
- CLIP 模型训练实现
- 多模态表示学习

### 4. PixArt 训练模块 (pixart/)
- PixArt 基础训练
- Sigma 版本训练支持

### 5. Cascade 训练模块 (cascade/)
- Cascade 模型 Stage C 训练
- 多阶段训练支持

### 6. LLaVA 训练模块 (llava/)
- LLaVA 模型训练实现
- 视觉-语言预训练

### 7. 工具模块 (utils/)
- 调度器工具函数
- SDXL 相关工具函数

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

1. 在对应子目录创建训练脚本
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