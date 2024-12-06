---
layout: post
title: "遇到的bug记录"
date: 2024-11-25
---
## 工具篇
1. 清华源：不用搜索清华源三个字

pip install -i https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple some-package

## 常见库类型
1.PIL和opencv打开图像和保存图像
```python
#opencv

img_path = os.path.join(path, img_name)
img = cv2.imread(img_path)
img_resize = cv2.resize(img,(300,300))
resized_img_name = 'reshape_'+img_name
resized_img_path = os.path.join(path, resized_img_name)
print(resized_img_path)
cv2.imwrite(resized_img_path,img_resize)

```

```python
#PIL
img=out_net["x_hat"].cpu().numpy().squeeze(0).transpose(1,2,0)
img=Image.fromarray(np.uint8(img*255))
img.save("./testres/"+img_name)

```
两个常见的坑：
1、TypeError: Cannot handle this data type: (1, 1, 300), <f4 没有把图像转换为WH3的格式，需要transpose(1,2,0)

2、TypeError: Cannot handle this data type: (1, 1, 300), <u1 没有把图像转换uint8,一般tensor都是0-1，所以需要*255

2.os
列出全部文件：os.listdir(path)

创建文件夹：推荐嵌套创建：os.makedirs()

## JPEG5py库报错：AttributeError: 'JPEG' object has no attribute 'decompressor'
缺少libturbojpeg 库  安装via:sudo apt-get install libturbojpeg

## 成功解决：AssertionError: Torch not compiled with CUDA enabled
### 1.问题1版本不匹配
很多帖子都是碰到了版本不匹配，但是我ubuntu经验比较足，知道那个nvidia-smi显示的是最高版本

### 问题2：安装的不是gpu torch
这个是我的问题，但是我是安装torch官网安装的

<img src="/post_imgs/minborbug/1.png"/>

后来我发现如果==使用清华源加速==，就会安装cpu torch
所以去掉加速：
成功：

<img src="/post_imgs/minborbug/2.png"/>

## import的包找不到/不能被pylance解读
如果是vscode的直接reload windows

## DataParallel中：【PyTorch】常见错误: RuntimeError: Input type (torch.FloatTensor) and weight type (torch.cuda.FloatTensor)
没放到显卡上，简单的错误，

### 如果是单卡：

直接todevice，无需多言

### 如果是多卡：
*模块未注册：如果你将模块存储在一个普通的 Python 列表（如 self.list = []）中，PyTorch 不会将这些模块视为模型的子模块，因此 DataParallel 不会自动将它们迁移到 GPU 上。*

改用modulelist
self.ca256 = nn.ModuleList([CoorAtten(self.c_256[i]) for i in range(5)])

## 爆显存：

简化模型，降低输入分辨率，多卡并行，都是很好的方法
