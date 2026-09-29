# NeuralNetworksZtoH
作为学习《Neural Networks: Zero to Hero》的项目目录。

## 环境配置
- 安装 mini-forge（安装时不勾选 Add to PATH 与 Register as default Python）
- 启动mini-forge power shell, 执行以下命令配置国内镜像（每台设备一次，写入 `%APPDATA%\pip\pip.ini`，对所有 conda 环境生效）:
```
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```
- 执行以下命令安装环境:
```
# 1. 建环境：只指定 Python 版本，不装任何包
conda create -n zero2hero python=3.11 -y

# 2. 激活
conda activate zero2hero

# 3. 通用依赖：requirements.txt 走清华镜像，跨平台通用（不含 torch）
pip install -r requirements.txt

# 4. torch 按平台单独装（二选一）:
#    a. 家里 GPU 机（5080 / 4060Ti）—— 必须用官方 CUDA 源（镜像里没有 GPU 版）:
pip install torch --index-url https://download.pytorch.org/whl/cu128
#    b. 云服务器（无 GPU / Linux）—— CPU 版（约 200MB）:
pip install torch --index-url https://download.pytorch.org/whl/cpu
```
> torch cu128 轮子约 3GB，来自 download.pytorch.org，国内下载较慢请耐心等待。

## 安装验证
```
# GPU 机（5080 / 4060Ti）
python -c "import torch; print(torch.__version__, torch.cuda.is_available(), torch.cuda.get_device_name(0))"
# 期望输出: 2.7.1+cu128 True <显卡名>

# 云服务器（无 N 卡，False 属正常）
python -c "import torch; print(torch.__version__, torch.cuda.is_available())"
# 期望输出: 2.7.1+cpu False
```

## 使用
- VS Code 打开 .ipynb 时，右上角内核选择 `zero2hero`
- 可选（micrograd 可视化计算图）: `winget install Graphviz.Graphviz` 后 `pip install graphviz`

## 课程配套代码仓库
| 讲次 | 仓库 |
|---|---|
| P1 micrograd | github.com/karpathy/micrograd |
| P2-P6 makemore | github.com/karpathy/makemore |
| P7 GPT | github.com/karpathy/nanoGPT |
| P9 Tokenizer | github.com/karpathy/minBPE |
| P10 复现 GPT-2 | github.com/karpathy/build-nanogpt |

