我会帮您创建详细的项目文档。首先让我查看项目的结构。

Ran tool
让我们深入了解一下主要的代码文件和模块。首先查看 README.md 来了解项目的基本信息。

Read file: README.md
让我们继续查看一些主要的代码文件。

Read file: trainer.py
基于对项目的了解，我将为您创建一个详细的项目文档。以下是文档的结构：

# Naifu 项目文档

## 1. 项目概述

Naifu（又称 naifu-diffusion）是一个用于训练生成式模型的框架，支持多种配置和特性。该项目主要用于训练和微调各种生成式模型，包括：

- Stable Diffusion XL (SDXL)
- SDXL Refiner
- Stable Diffusion 1.4/1.5
- PixArt-Alpha
- LCM (Latent Consistency Models)
- StableCascade
- 各种语言模型 (GPT2, LLaMA, Qwen, Gemma 等)

## 2. 系统要求

- Python 3.9 或更高版本
- CUDA 兼容的 GPU
- 足够的 GPU 显存（根据模型大小而定）

## 3. 项目结构

```
project_root/
├── trainer.py           # 主训练脚本
├── requirements.txt     # 项目依赖
├── modules/            # 核心模块目录
├── utils/             # 工具函数
├── scripts/           # 辅助脚本
├── models/            # 模型定义
├── dataset/           # 数据集处理
├── config/            # 配置文件
├── data_loader/       # 数据加载器
└── common/            # 通用功能模块
```

## 4. 核心模块说明

### 4.1 训练器 (trainer.py)

主要训练脚本，负责：
- 配置加载和解析
- 训练环境初始化
- 分布式训练支持
- 日志记录
- 训练循环控制

关键代码示例：
```
def main():
    args = parse_args()
    config = OmegaConf.load(args.config)
    config.trainer.resume = args.resume
    plugins = []

    # 初始化训练策略
    strategy = config.lightning.pop("strategy", "auto")
    strategy_params = config.lightning.pop("strategy_params", {})
    
    # 设置日志记录器
    loggers = pl.fabric.loggers.CSVLogger(".")
    
    # 初始化训练环境
    fabric = pl.Fabric(
        loggers=[loggers], 
        plugins=plugins, 
        strategy=strategy, 
        **config.lightning
    )
```

### 4.2 配置系统

项目使用 YAML 格式的配置文件，支持多种训练场景：

- train_sdxl.yaml: SDXL 模型训练
- train_refiner.yaml: SDXL refiner 训练
- train_sd15.yaml: Stable Diffusion 1.5 训练
- train_lycoris.yaml: LyCORIS 训练
- train_dpo.yaml: Diffusion DPO 训练
- train_pixart.yaml: PixArt-Alpha 训练
- train_lcm.yaml: LCM 模型训练
- train_cascade_stage_c.yaml: StableCascade 训练
- train_general_llm.yaml: 通用语言模型训练

## 5. 使用指南

### 5.1 安装

```
# 克隆仓库
git clone --depth 1 https://github.com/mikubill/naifu

# 安装依赖
cd naifu && pip install -r requirements.txt
```

### 5.2 基本使用

```
# 基本训练命令
python trainer.py --config config/<config_file>

# 或者
python trainer.py config/<config_file>
```

### 5.3 SDXL 训练示例

```
# 准备图像数据（转换为潜空间）
python scripts/encode_latents_xl.py -i <input_path> -o <encoded_path>

# 使用基础 SDXL 模型训练
python trainer.py config/train_sdxl.yaml

# 使用 Hugging Face 模型
python trainer.py config/train_diffusers.yaml
```

## 6. 高级特性

### 6.1 分布式训练

支持多种分布式训练策略：
- DDP (DistributedDataParallel)
- FSDP (Fully Sharded Data Parallel)
- DeepSpeed
- FairScale

### 6.2 精度控制

支持多种精度训练模式：
- FP32
- FP16
- BF16
- 混合精度训练

### 6.3 模型优化

支持多种模型优化技术：
- LoRA
- QLoRA
- LyCORIS
- DPO (Direct Preference Optimization)

## 7. 常见问题解答

1. 显存不足怎么办？
   - 尝试减小 batch size
   - 使用梯度累积
   - 启用 gradient checkpointing
   - 考虑使用 LoRA 或 QLoRA

2. 训练中断如何恢复？
   - 使用 `--resume` 参数指定检查点路径
   - 确保检查点文件完整

3. 如何调整学习率？
   - 在配置文件中修改 `learning_rate` 参数
   - 可以使用学习率调度器
   - 建议从小的学习率开始调整

## 8. 贡献指南

1. Fork 项目
2. 创建特性分支
3. 提交更改
4. 推送到分支
5. 创建 Pull Request

## 9. 许可证

项目使用 LICENSE 文件中指定的许可证。

这个文档提供了项目的主要组件和功能的概述。如果您需要某个特定模块或功能的更详细说明，我可以为您深入解释。
