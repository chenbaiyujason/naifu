# Models 模型目录文档

## 目录概述

Models 目录用于存储预训练模型和训练过程中的模型检查点。这个目录的结构和组织方式对于管理不同版本的模型和检查点非常重要。

## 目录结构

<code>
models/
├── checkpoints/           # 训练检查点
│   ├── sdxl/             # SDXL 模型检查点
│   ├── llm/              # 语言模型检查点
│   └── multimodal/       # 多模态模型检查点
├── pretrained/           # 预训练模型
│   ├── sdxl/             # SDXL 预训练模型
│   ├── llm/              # 语言模型预训练
│   └── multimodal/       # 多模态预训练模型
└── converted/           # 转换后的模型
    ├── onnx/             # ONNX 格式模型
    └── tensorrt/         # TensorRT 格式模型
</code>

## 模型类型

### 1. SDXL 相关模型

- 基础 SDXL 模型
- SDXL Refiner
- SDXL 中文版本
- SDXL IP-Adapter

### 2. 语言模型

- GPT-2 模型
- Phi-2 模型
- Mistral 模型
- 通用语言模型

### 3. 多模态模型

- CLIP 模型
- LLaVA 模型
- LLaVA 1.6 模型

### 4. 其他生成模型

- Cascade 模型
- PixArt 模型
- LCM 模型

## 模型管理指南

### 1. 检查点命名规范

<code>
# 检查点命名格式
{model_type}-{version}-{timestamp}-{step}.ckpt

# 示例
sdxl-v1.0-20240305-100000.ckpt
llava-1.6-20240305-50000.ckpt
</code>

### 2. 模型版本控制

- 使用语义化版本号
- 记录模型变更历史
- 保存配置文件副本

### 3. 模型转换

#### ONNX 转换
<code>
python tools/convert_to_onnx.py \
    --model path/to/model.ckpt \
    --output path/to/model.onnx \
    --input_shape 1,3,1024,1024
</code>

#### TensorRT 转换
<code>
python tools/convert_to_tensorrt.py \
    --onnx path/to/model.onnx \
    --output path/to/model.engine \
    --fp16
</code>

## 存储管理

### 1. 空间管理

- 定期清理旧检查点
- 压缩不常用模型
- 使用软链接管理大文件

### 2. 备份策略

- 定期备份重要模型
- 使用版本控制系统
- 多地备份关键文件

### 3. 访问控制

- 设置适当的文件权限
- 记录访问日志
- 实现用户认证

## 最佳实践

### 1. 模型选择

- 根据任务选择合适的基础模型
- 考虑计算资源限制
- 评估模型性能指标

### 2. 检查点管理

- 保存关键训练节点
- 记录实验配置
- 标注模型特点

### 3. 性能优化

- 模型量化
- 模型剪枝
- 知识蒸馏

## 使用示例

### 1. 加载预训练模型

<code>
from modules.sdxl_model import SDXLModel

model = SDXLModel.from_pretrained(
    "models/pretrained/sdxl/v1.0/model.safetensors"
)
</code>

### 2. 保存检查点

<code>
# 保存完整检查点
model.save_checkpoint(
    "models/checkpoints/sdxl/model-v1.0-step100k.ckpt",
    save_optimizer=True
)

# 保存模型权重
model.save_weights(
    "models/checkpoints/sdxl/weights-v1.0.safetensors"
)
</code>

### 3. 模型转换

<code>
# 转换为 ONNX
model.export_onnx(
    "models/converted/onnx/model-v1.0.onnx",
    input_shapes={"x": [1, 3, 1024, 1024]}
)
</code>

## 常见问题

### Q: 如何选择合适的检查点？
A: 根据验证集性能和具体应用场景选择最佳检查点

### Q: 如何处理模型兼容性问题？
A: 保存完整的配置信息，使用版本转换工具

### Q: 如何优化模型存储空间？
A: 使用模型压缩技术，只保留必要的检查点 