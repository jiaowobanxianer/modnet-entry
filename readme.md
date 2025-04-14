# 【MODNet-entry】开箱即用的人像抠图工具

由[项目连接](https://github.com/RimoChan/modnet-entry)fork。
模型效果参考看[原仓库](https://github.com/ZHKKKe/MODNet)。

## 安装

```bash
pip install git+https://github.com/jiaowobanxianer/modnet-entry.git
```

安装时会从Google Drive下载预训练模型，所以要保证网络。

## 示例

首先随便准备一张`test.png`或者是`test.jpg`，然后——

```python
from MODNet_entry import get_model, pnginfer, jpginfer

model = get_model('modnet_photographic_portrait_matting.ckpt')
pnginfer(model, 'test.png', 'alpha.png', 'new_image.png')
#jpginfer(model, 'jpg.png', 'jpgalpha.png', 'new_jpgimage.png')
```

## 接口

```python
def get_model(ckpt_name: str) -> MODNet: ...
```

获取一个预训练的模型。

参数:

- `ckpt_name`: 模型的名字。只有`modnet_photographic_portrait_matting.ckpt`/`modnet_webcam_portrait_matting.ckpt`两种可选。

```python
def get_model(ckpt_fullpath: str) -> MODNet: ...
```

从外部导入模型。

参数:

- `ckpt_fullpath`: 模型的完整路径。

<hr/>

```python
def infer(modnet: MODNet, im: np.ndarray[np.uint8], ref_size=1024) -> np.ndarray[np.float32]: ...
```

输入一张图，预测alpha通道。

参数: 

- `modnet`: 刚才加载的那个模型。

- `im`: 图片。RGB或RGBA或灰度的uint8矩阵。

- `ref_size`: 预测时如果图片的短边长于这个尺寸就缩小到这个尺寸。

返回一个与原图相同大小的灰度float矩阵。

<hr/>

```python
def pnginfer(modnet: MODNet, img_path: str, out_alpha_path: str = '', out_img_path: str = ''): ...
```

输入一个png图片路径，将抠图结果保存在硬盘上。

参数: 

- `modnet`: 刚才加载的那个模型。

- `img_path`: 输入图片路径。

- `out_alpha_path`: 输出alpha图片路径。

- `out_img_path`: 输出抠好的图的路径。

<hr/>

```python
def jpginfer(modnet: MODNet, img_path: str, out_alpha_path: str = '', out_img_path: str = ''): ...
```

输入一个jpg图片路径，将抠图结果保存在硬盘上。

参数: 
    同上

## 结束
