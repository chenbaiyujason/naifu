# Data Loader 数据加载模块文档

## 模块概述

Data Loader 目录包含了项目中所有的数据加载、预处理和数据转换相关的代码。这些模块主要用于处理各种格式的数据，并将其转换为模型训练所需的格式。

## 主要组件

### 1. Arrow 数据处理

#### 基础加载器
- `arrow_load_stream.py`: 基础 Arrow 流式加载器
- `arrow2_load_stream.py`: 改进版 Arrow 流式加载器
- `arrow_test.py`: Arrow 加载测试工具

#### 专用加载器
- `arrow_load_stream_for_cn.py`: 中文数据加载器
- `arrow_load_stream_for_clip.py`: CLIP 数据加载器
- `arrow_load_stream_for_ipadapter.py`: IP-Adapter 数据加载器

### 2. 数据转换工具

#### CSV 转 Arrow
- `csv2arrow.py`: 基础 CSV 转 Arrow 工具
- `csv2arrow_cn.py`: 中文数据转换工具
- `csv2arrow_custom_dan.py`: 自定义数据转换工具
- `csv2arrow_full.py`: 完整数据转换工具

#### 其他转换工具
- `arrow_2_json.py`: Arrow 转 JSON 工具
- `build_yaml.py`: YAML 配置生成工具

### 3. 数据清洗和处理

- `data_clean.py`: 数据清洗工具
- `tag_tool.py`: 标签处理工具
- `tile_process.py`: 图像分块处理工具

### 4. 数据采集

- `eugebooru.py`: Booru 网站数据采集
- `eugebooru_clip.py`: CLIP 训练数据采集
- `eugebooru_ipa.py`: IP-Adapter 训练数据采集

## 使用指南

### 1. 数据转换

#### CSV 转 Arrow 格式
<code>
# 基础转换
python data_loader/csv2arrow.py \
    --input data.csv \
    --output data.arrow

# 带评分检查的转换
python data_loader/csv2arrow_full_with_score_check.py \
    --input data.csv \
    --output data.arrow \
    --min_score 7.0
</code>

#### 数据清洗
<code>
python data_loader/data_clean.py \
    --input dirty_data.arrow \
    --output clean_data.arrow \
    --rules rules.json
</code>

### 2. 数据加载

#### 基础数据加载
<code>
from data_loader.arrow_load_stream import ArrowStreamLoader

loader = ArrowStreamLoader(
    arrow_file="data.arrow",
    batch_size=32,
    shuffle=True
)
</code>

#### CLIP 数据加载
<code>
from data_loader.arrow_load_stream_for_clip import ClipArrowStreamLoader

loader = ClipArrowStreamLoader(
    arrow_file="clip_data.arrow",
    batch_size=32,
    image_size=224
)
</code>

## 数据格式规范

### 1. Arrow 文件结构

基础字段：
- `image_path`: 图像路径
- `caption`: 图像描述
- `tags`: 标签列表（可选）
- `score`: 评分（可选）

### 2. 图像要求

- 支持格式：JPG, PNG, WEBP
- 建议分辨率：大于 512x512
- 色彩空间：RGB

### 3. 文本数据要求

- 描述语言：支持中文和英文
- 标签格式：逗号分隔
- 编码：UTF-8

## 开发指南

### 添加新的数据加载器

1. 创建新的加载器类
2. 实现必要的数据预处理方法
3. 添加数据增强功能
4. 实现批处理逻辑

示例：
<code>
class CustomDataLoader:
    def __init__(
        self,
        arrow_file: str,
        batch_size: int,
        shuffle: bool = True
    ):
        self.arrow_file = arrow_file
        self.batch_size = batch_size
        self.shuffle = shuffle
        
    def __iter__(self):
        # 实现数据迭代逻辑
        pass
        
    def __len__(self):
        # 实现数据长度计算
        pass
</code>

### 代码规范

- 所有加载器必须实现 `__iter__` 和 `__len__` 方法
- 数据预处理应该支持多进程
- 必须处理异常情况
- 添加适当的数据验证

## 性能优化

1. 数据缓存
   - 使用内存映射
   - 实现预取功能
   - 优化批处理逻辑

2. 多进程处理
   - 使用进程池
   - 实现并行数据加载
   - 优化内存使用

3. IO 优化
   - 使用异步 IO
   - 实现数据流式处理
   - 优化磁盘访问

## 常见问题

### Q: 如何处理大规模数据集？
A: 使用流式处理和多进程加载

### Q: 如何处理内存不足问题？
A: 调整批处理大小，使用数据流式处理

### Q: 如何提高数据加载速度？
A: 使用缓存，实现预取，优化数据格式 