# Super-SloMo

## 准备环境

该代码库是使用 PyTorch 0.4.1，CUDA 9.2 和 Python 3.6 开发和测试的。

- 对于 GPU，运行

```bash
conda install pytorch=0.4.1 cuda92 torchvision==0.2.0 -c pytorch
```

- 对于 CPU，运行

```bash
conda install pytorch-cpu=0.4.1 torchvision-cpu==0.2.0 cpuonly -c pytorch
```

## 训练

### 准备训练数据

为了使用提供的代码训练模型，需要以某种方式格式化数据。create_dataset.py 脚本使用 FFmpeg 从视频中提取帧。

#### Adobe240fps

对于 adobe240fps，下载数据集，解压缩，然后运行以下命令：

```bash
python data\create_dataset.py --ffmpeg_dir path\to\folder\containing\ffmpeg --videos_folder path\to\adobe240fps\videoFolder --dataset_folder path\to\dataset --dataset adobe240fps
```

#### 自定义数据集

对于自定义数据集，运行以下命令：

```bash
python data\create_dataset.py --ffmpeg_dir path\to\folder\containing\ffmpeg --videos_folder path\to\adobe240fps\videoFolder --dataset_folder path\to\dataset
```

### 运行

在 `Super-SloMo.ipynb` 中，设置参数（数据集路径，检查点目录等）并运行所有单元。

### TensorBoard

为了获得训练的可视化效果，您可以使用以下命令从项目目录运行 TensorBoard：

```bash
tensorboard --logdir log --port 6007
```

## 评估

### 预训练模型

您可以下载 [adobe240fps 数据集训练的预训练模型](https://drive.google.com/file/d/1IvobLDbRiBgZr3ryCRrWL8xDbMZ-KnpF/view)

### 训练数据转换器

您可以使用 `video_to_slomo.py`，将任何视频转换为慢动作或高 fps 视频，使用这个命令：

#### Windows

```bash
python video_to_slomo.py --ffmpeg path\to\folder\containing\ffmpeg --video path\to\video.mp4 --sf N --checkpoint path\to\checkpoint.ckpt --fps M --output path\to\output.mkv
```

#### Linux

```bash
python video_to_slomo.py --video path\to\video.mp4 --sf N --checkpoint path\to\checkpoint.ckpt --fps M --output path\to\output.mkv 
```

如果要将视频从 30fps 转换为 90fps，请将 `fps` 设为 90，`sf` 设为 3.
