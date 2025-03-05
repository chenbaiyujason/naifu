# Data 数据处理模块文档

## 模块概述

Data 目录包含了项目中的核心数据处理模块，负责数据集的加载、预处理、数据增强和批处理等功能。这些模块为模型训练提供高效的数据处理流水线。

## 主要组件

### 1. 数据集实现

#### 基础数据集
- `text_dataset.py`: 文本数据集实现
- `llava_dataset.py`: LLaVA 多模态数据集实现
- `paired_wds.py`: 配对 WebDataset 实现

#### 数据存储
- `image_storage.py`: 图像存储管理
- `bucket.py`: 数据分桶实现

### 2. 数据处理工具

- `processors.py`: 数据处理器集合
- `prompt_style.py`: 提示词样式处理
- `webdataset_utils.py`: WebDataset 工具函数

### 3. 对话处理

- `conversation.py`: 对话数据处理模块

## 核心功能说明

### 1. 数据集实现

#### 文本数据集
<code>
from data.text_dataset import TextDataset

dataset = TextDataset(
    data_path="path/to/data",
    tokenizer=tokenizer,
    max_length=512,
    shuffle=True
)
</code>

#### LLaVA 数据集
<code>
from data.llava_dataset import LLaVADataset

dataset = LLaVADataset(
    image_folder="path/to/images",
    conversation_file="path/to/conversations.json",
    image_processor=processor,
    tokenizer=tokenizer
)
</code>

### 2. 数据存储管理

#### 图像存储
<code>
from data.image_storage import ImageStorage

storage = ImageStorage(
    root_dir="path/to/storage",
    cache_size=1000,
    device="cuda"
)

# 存储图像
storage.save(image_id, image_tensor)

# 读取图像
image = storage.load(image_id)
</code>

#### 数据分桶
<code>
from data.bucket import DynamicBucket

bucket = DynamicBucket(
    bucket_size=32,
    min_size=256,
    max_size=1024,
    step=64
)

# 添加数据
bucket.add(data, size)

# 获取批次
batch = bucket.get_batch()
</code>

### 3. 对话处理

<code>
from data.conversation import Conversation

conversation = Conversation(
    system="你是一个AI助手",
    messages=[
        {"role": "user", "content": "你好"},
        {"role": "assistant", "content": "你好！有什么我可以帮你的吗？"}
    ]
)

# 获取格式化对话
formatted = conversation.get_formatted()

# 添加新消息
conversation.append_message("user", "请帮我写一首诗")
</code>

## 数据处理流程

### 1. 数据加载
- 支持多种数据格式
- 实现数据流式加载
- 处理大规模数据集

### 2. 数据预处理
- 文本标准化
- 图像变换
- 标签处理

### 3. 数据增强
- 随机裁剪
- 颜色抖动
- 文本增强

### 4. 批处理
- 动态批处理
- 内存管理
- 并行处理

## 开发指南

### 添加新数据集

1. 创建数据集类
<code>
class CustomDataset:
    def __init__(
        self,
        data_path: str,
        transform: Optional[Callable] = None
    ):
        self.data_path = data_path
        self.transform = transform
        
    def __len__(self) -> int:
        # 实现数据集长度计算
        pass
        
    def __getitem__(self, idx: int) -> Dict[str, torch.Tensor]:
        # 实现数据加载逻辑
        pass
</code>

2. 实现数据处理
<code>
class CustomProcessor:
    def __init__(self, **kwargs):
        self.kwargs = kwargs
        
    def __call__(self, data: Dict[str, Any]) -> Dict[str, torch.Tensor]:
        # 实现数据处理逻辑
        pass
</code>

### 代码规范

- 使用类型注解
- 添加详细文档
- 实现数据验证
- 处理边界情况

## 性能优化

### 1. 数据加载优化
- 使用内存映射
- 实现预取机制
- 优化 IO 操作

### 2. 处理加速
- 使用多进程处理
- GPU 加速
- 向量化操作

### 3. 内存管理
- 实现数据缓存
- 控制内存使用
- 及时释放资源

## 常见问题

### Q: 如何处理大规模数据集？
A: 使用流式处理，实现数据分片，采用多进程加载

### Q: 如何提高数据处理速度？
A: 优化数据加载，使用缓存，实现并行处理

### Q: 如何处理不平衡数据？
A: 实现数据重采样，使用权重采样，增强少数类样本 