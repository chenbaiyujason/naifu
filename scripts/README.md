# Scripts 脚本模块文档

## 模块概述

Scripts 目录包含了项目中的各种辅助脚本，用于数据处理、模型推理、工具测试等任务。这些脚本提供了完整的命令行接口，方便用户进行各种操作。

## 主要组件

### 1. 模型推理脚本

#### Cascade 模型推理
- `cascade_inf.py`: Cascade 模型推理脚本
- `gpt2_inference.py`: GPT-2 模型推理脚本
- `run_llava.py`: LLaVA 模型推理脚本

使用示例：
<code>
# Cascade 模型推理
python scripts/cascade_inf.py \
    --model path/to/model \
    --prompt "your prompt" \
    --output output.png

# GPT-2 推理
python scripts/gpt2_inference.py \
    --model path/to/model \
    --prompt "your prompt" \
    --max_length 100
</code>

### 2. 数据处理工具

#### 标签处理
- `deepdanbooru.py`: DeepDanbooru 标签生成器
- `wd14_tagger.py`: WD14 标签生成器

使用示例：
<code>
# 使用 DeepDanbooru 生成标签
python scripts/deepdanbooru.py \
    --input path/to/images \
    --output tags.json

# 使用 WD14 生成标签
python scripts/wd14_tagger.py \
    --input path/to/images \
    --output tags.csv
</code>

#### 数据编码
- `encode_latents_xl.py`: SDXL 潜空间编码工具

使用示例：
<code>
python scripts/encode_latents_xl.py \
    --input path/to/images \
    --output path/to/latents \
    --batch_size 32
</code>

### 3. 实验和测试工具

#### VAE 工具
- `vae_cache_inspector.ipynb`: VAE 缓存检查工具
- `vae_playground.ipynb`: VAE 实验工具

#### 其他工具
- `struc.py`: 项目结构分析工具
- `test_util.py`: 测试工具集
- `upload.py`: 文件上传工具

## 使用指南

### 1. 标签生成

使用 DeepDanbooru 或 WD14 为图像生成标签：

<code>
# DeepDanbooru
python scripts/deepdanbooru.py \
    --input images/ \
    --output tags.json \
    --batch_size 32 \
    --threshold 0.5

# WD14
python scripts/wd14_tagger.py \
    --input images/ \
    --output tags.csv \
    --batch_size 32 \
    --threshold 0.5
</code>

### 2. 潜空间编码

为 SDXL 训练准备数据：

<code>
python scripts/encode_latents_xl.py \
    --input training_images/ \
    --output encoded_latents/ \
    --batch_size 32 \
    --resolution 1024 \
    --device cuda
</code>

### 3. 模型推理

#### LLaVA 推理
<code>
python scripts/run_llava.py \
    --model path/to/model \
    --image input.jpg \
    --prompt "描述这张图片"
</code>

#### Cascade 推理
<code>
python scripts/cascade_inf.py \
    --model path/to/model \
    --prompt "生成一张图片" \
    --steps 30 \
    --cfg_scale 7.0
</code>

## 开发指南

### 添加新脚本

1. 创建新的 Python 脚本
2. 实现命令行接口
3. 添加错误处理
4. 更新文档

### 代码规范

- 使用 argparse 处理命令行参数
- 添加详细的帮助信息
- 实现进度显示
- 添加日志记录

### 测试要求

- 添加单元测试
- 提供示例数据
- 验证边界情况
- 测试错误处理

## 性能优化

### 1. 批处理优化
- 使用适当的批大小
- 实现数据预取
- 优化内存使用

### 2. GPU 利用
- 支持混合精度
- 优化 CUDA 内存使用
- 实现 GPU/CPU 切换

### 3. 并行处理
- 使用多进程处理
- 实现异步操作
- 优化 IO 操作

## 常见问题

### Q: 脚本运行时内存不足怎么办？
A: 调整批处理大小，使用生成器模式处理数据

### Q: 如何处理大规模数据集？
A: 使用分批处理，实现断点续传功能

### Q: 如何提高处理速度？
A: 使用多进程、GPU 加速，优化数据加载 