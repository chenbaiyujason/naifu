# Utils 工具模块文档

## 模块概述

Utils 目录包含了项目中使用的各种工具函数和辅助脚本。这些工具主要用于文件处理、模型比较和其他辅助功能。

## 主要组件

### 1. 模型比较工具 (compare_model.py)

用于比较不同模型的参数和性能。

主要功能：
- 模型参数对比
- 性能指标比较
- 差异可视化

使用示例：
```
python utils/compare_model.py \
    --model1 path/to/model1 \
    --model2 path/to/model2 \
    --output comparison_result.txt
```

### 2. 文件移动工具 (mv_file.py)

用于批量移动和组织文件。

主要功能：
- 批量文件移动
- 文件重命名
- 目录结构重组

使用示例：
```
python utils/mv_file.py \
    --source source_dir \
    --target target_dir \
    --pattern "*.jpg"
```

### 3. 解压工具 (untar.py)

用于处理压缩文件。

主要功能：
- 解压 tar 文件
- 支持多种压缩格式
- 批量处理功能

使用示例：
```
python utils/untar.py \
    --input archive.tar.gz \
    --output output_dir
```

## 开发指南

### 添加新工具

1. 创建新的 Python 文件
2. 实现主要功能
3. 添加命令行接口
4. 更新文档

### 代码规范

- 所有工具脚本都应该提供命令行接口
- 必须包含详细的帮助文档
- 需要处理异常情况
- 添加适当的日志记录

### 测试

每个工具都应该包含：
- 单元测试
- 集成测试
- 使用示例

## 使用建议

1. 在使用文件处理工具前，建议先备份重要数据
2. 对于大规模操作，建议先在小数据集上测试
3. 注意检查工具的输出日志

## 常见问题

### Q: 如何处理文件权限问题？
A: 确保有适当的文件系统权限，必要时使用 sudo

### Q: 工具支持哪些操作系统？
A: 所有工具都支持 Linux 和 macOS，部分工具支持 Windows

### Q: 如何报告问题？
A: 在项目 Issue 页面提交问题，并附上详细的错误信息和复现步骤 