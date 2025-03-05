# Naifu

naifu（或称naifu-diffusion）是为训练具有各种配置和功能的生成模型而设计的。本仓库主分支中的代码正在开发中，随着新功能的添加可能会发生变化。

## 安装

要开始使用Naifu，请按照以下步骤安装必要的依赖项：

```bash
# 克隆Naifu仓库：
git clone --depth 1 https://github.com/mikubill/naifu

# 安装所需的Python包：
cd naifu && pip install -r requirements.txt
```

确保您安装了兼容版本的Python（Python 3.9或更高版本）。

## 使用方法

Naifu提供了一种灵活直观的方式，使用各种配置来训练模型。要训练模型，请使用trainer.py脚本并提供所需的配置文件作为参数。

```bash
python trainer.py --config config/<config_file>

# 或（与--config相同）
python trainer.py config/<config_file>
```

将`<config_file>`替换为下面列出的可用配置文件之一。

## 配置

根据训练目标和环境选择适当的配置文件。

训练SDXL（Stable Diffusion XL）模型
```bash
# 准备图像数据（转换为潜在空间）
python scripts/encode_latents_xl.py -i <input_path> -o <encoded_path>

# sd_xl_base_1.0_0.9vae.safetensors
python trainer.py config/train_sdxl.yaml

# 对于huggingface模型支持
# stabilityai/stable-diffusion-xl-base-1.0
python trainer.py config/train_diffusers.yaml

# 使用原始sgm损失模块
python trainer.py config/train_sdxl_original.yaml
```

训练SDXL精炼器（Stable Diffusion XL refiner）模型
```bash
# stabilityai/stable-diffusion-xl-refiner-1.0
python trainer.py config/train_refiner.yaml
```

训练原始Stable Diffusion 1.4或1.5模型
```bash
# runwayml/stable-diffusion-v1-5
# 注意：将以diffusers格式保存
python trainer.py config/train_sd15.yaml
```

使用LyCORIS训练SDXL模型
```bash
# 基于KohakuBlueleaf/LyCORIS的工作
pip install lycoris_lora toml
python trainer.py config/train_lycoris.yaml
```

使用fairscale策略进行分布式数据并行分片训练
```bash
pip install fairscale
python trainer.py config/train_fairscale.yaml
```

使用直接偏好优化（DPO）训练SDXL模型  
论文：Diffusion Model Alignment Using Direct Preference Optimization ([arxiv:2311.12908](https://arxiv.org/abs/2311.12908))
```bash
# 数据集：yuvalkirstain/pickapic_v2
# 调整分辨率和dpo_betas时要小心！
# 将以diffusers格式保存
python trainer.py config/train_dpo_diffusers.yaml # diffusers后端
python trainer.py config/train_dpo.yaml # sgm后端
```

训练Pixart-Alpha模型  
论文：Fast Training of Diffusion Transformer for Photorealistic Text-to-Image Synthesis ([arxiv:2310.00426](https://arxiv.org/abs/2310.00426))
```bash
# PixArt-alpha/PixArt-XL-2-1024-MS
python trainer.py config/train_pixart.yaml
```

训练SDXL-LCM模型  
论文：Latent Consistency Models: Synthesizing High-Resolution Images with Few-Step Inference ([arxiv:2310.04378](https://arxiv.org/abs/2310.04378))
```bash
python trainer.py config/train_lcm.yaml
```

训练StableCascade模型（[Sai](https://github.com/Stability-AI/StableCascade/)）
```bash
# 目前仅支持stage_c（带或不带文本编码器）
python trainer.py config/train_cascade_stage_c.yaml
```

训练GPT2模型
```bash
python trainer.py config/train_gpt2.yaml
```

使用[Phi-1.5/2](https://huggingface.co/microsoft)模型训练
```bash
python trainer.py config/train_phi2.yaml
```

训练语言模型（[LLaMA](https://github.com/facebookresearch/llama)、[Qwen](https://huggingface.co/Qwen)、[Gemma](https://huggingface.co/google)等）
```bash
# 注意：准备sharegpt/chatml格式的数据，或在data/text_dataset.py中定义您自己的数据集
# 参考示例数据集：function-calling-sharegpt
python trainer.py config/train_general_llm.yaml
```

使用lora或qlora训练语言模型（例如，[Mistral](https://huggingface.co/mistralai)）
```bash
python trainer.py config/train_mistral_lora.yaml
```

## 其他分支

* sgm - 使用[sgm](https://github.com/Stability-AI/generative-models)训练SDXL模型。
* sd3 - SD3模型的训练器 - 谨慎使用：可能产生不期望的结果
* hydit - 用于训练混元dit模型的训练器（v1.1和v1.2）
* main-archived - 包含用于训练Stable Diffusion 1.x模型的原始naifu-diffusion代码。

对于没有文档的分支，请按照上面提供的安装说明进行操作。