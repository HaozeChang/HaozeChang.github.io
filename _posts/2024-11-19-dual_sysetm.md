---
layout: post
title: ”双系统配置搬运“
date: 2024-11-19
---

csdn博客搬运，不知道为什么每次都说我侵权
 
* [# 1.安装双系统](#1.安装双系统)
  * [1.1 安装windows系统](##1.1安装windows系统)
  * [1.2 就会出现如下问题：](##1.2就会出现如下问题：)
* [# 2.windows系统配置](#2.windows系统配置)
    * [2.1 配置tex](##2.1配置tex)
    * [2.2 配置zotero](##2.2配置zotero)
* [# 3.Linux系统配置](#3.Linux系统配置)
 
// 预览效果如下：
# 1.安装双系统
因为前几日安装vmware虚拟机导致键盘失灵，而且近几代的VMware下载比较麻烦，所以想直接装个双系统，在这里开源一下自己装机过程中踩坑的记录。
参考了：
[(保姆式教学) Win10 + Ubuntu 20.04——双系统安装方法 + 配置显卡 + root权限 + flash调配](https://blog.csdn.net/codeHonghu/article/details/111940656)

[Ubuntu20.04双系统安装详解（内容详细，一文通关！）](https://blog.csdn.net/wyr1849089774/article/details/133387874)
## 1.1 安装windows系统
安装windows系统有很多教程，我个人认为最好的是视频教程，因为现在的主板型号基本上都是那几款，需要用到双系统的也基本是计算机电子控制这类，基本都是拯救者、DELL等，这个视频讲的很细：
[【系统安装指南】win10/win11系统安装/激活/解疑指南，多方式安装，简单易懂，简介附免费激活工具！_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1tX4qejESM/?spm_id_from=333.999.0.0)

但是这里要注意一个细节就是，一般的新主板只会支持UEFI引导启动了，只有部分老机器会支持Legacy启动，这种方式会导致一个问题。ubuntu系统是只能识别uefi启动的，如果是mbr启动，就无法正常识别，ubuntu看不出来这个盘上有系统，他会觉得这是一堆文件。有的朋友会说，无所谓啊，我自己分区就行了，但是mbr又有一个问题，只能四个分区，ubuntu本身的根节点，home，交换空间，efi已经四个了，所以会导致windows进不去。自己踩了超多的坑
==第一个注意点！==
必须使用uefi安装。
参考：[MBR分区](https://blog.csdn.net/White_Idiot/article/details/80088115)
**假设你不是uefi：**
## 1.2 就会出现如下问题：
### 1.先安装mbr的windows：
无法正确分区ubuntu
### 2.安装mbr的windows，让ubuntu自己安装自己
ubuntu是可以有个选项和windows 共存的，但是mbr下他识别不出，这个选项没有，只能自己分区
![如果MBR是没有第一个选项的](https://i-blog.csdnimg.cn/direct/648af05301c14b7e923e76138e05c74a.png)
如果MBR是没有第一个选项的
### 3.少分两个区
不行，会导致windows无了
### 4.进windows再改为gpt
不行，我自己的黑屏了


==这里必须注意，这个点非常麻烦，进入windows再修改文件的形式会导致无法开机（我就是）==

------------------------------------------------------------------------------分割线-------------------------------------------------------------------------------------------
## 1.2 安装ubuntu系统
这里没踩坑，就参考网上的配置就行。制作系统盘的时候，个人感觉最快的是清华源
[清华软件源](https://mirrors.tuna.tsinghua.edu.cn/)
------------------------------------------------------------------------------分割线-------------------------------------------------------------------------------------------
# 2.windows系统配置
## 2.1 配置tex
参考了 [LaTeX-TeXlive和TeXstudio的下载、安装配置及使用](https://zhuanlan.zhihu.com/p/138586028)
这里要注意：
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/88b0de7fa62342b2a81a991e0a41dc12.png)
注意按照英文的配置改为Pdflatex，要不然后面会报
## 2.2 配置Zotero
相信有双系统需求的很大一批是科研狗，我也是，我原来是Zotero 6，我把我的数据库保存了下来，但是Zotero 7打开6的文库是会丢文件的！
参考 [Zotero路径配置详解](https://blog.csdn.net/tortorish/article/details/128987916)
==第二个注意点==
zotero 6用户的文库不要用7打开，会丢文件！！！！
# 3.Linux系统配置
参考了 
[ubuntu18.04双系统配置linux内核、nvidia、cuda、cudnn](https://blog.csdn.net/hxyzs/article/details/131972659?spm=1001.2014.3001.5502)
文章写的非常详细，我在这里仅记录几个不同的地方，
第一个是：
## 3.1 安装显卡驱动
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/06f06cc45afe485da691879fd7061af0.png)
执行这步之后我没有任何输出，所以直接安装了系统推荐的版本，就和该帖子中说的一样

## 3.2 安装CUDA
第二个是：
cuda的run文件下载问题，我尝试了n多次，都是在最后1s段错误，类似：
[Ubuntu18.04安装CUDA段错误（核心已转储）解决方案](https://blog.csdn.net/m0_57448978/article/details/130239746)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/30579857522f40c0aeb48282253d1f9d.png)
但是修改了还是不行，最后使用了多线程下载工具：
参考：[【Linux】多线程下载工具axel的安装和使用](https://blog.csdn.net/ARPOSPF/article/details/112163281)
**先安装！** 然后非常简单，只需要把
```python
wget https://developer.download.nvidia.com/compute/cuda/12.2.1/local_installers/cuda_12.2.1_535.86.10_linux.run
```
替换为：
```python
axel https://developer.download.nvidia.com/compute/cuda/12.2.1/local_installers/cuda_12.2.1_535.86.10_linux.run
```
**注意替换代码：把cuda-xx**替换为自己的版本
```python
export PATH=/usr/local/cuda-11.4/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-11.4/lib64:$LD_LIBRARY_PATH          
export LIBRARY_PATH=/usr/local/cuda-11.4/lib64:$LIBRARY_PATH
~                                                                
```
这里要注意，如果是复制的官方的配置命令，可能会在后面配置ROS的时候出错，即[ROS](https://blog.csdn.net/weixin_43077628/article/details/114969790)
## 3.3 安装cudnn
其实cudnn是一个头文件的集合，所以与其说安装，不如说配置，因此我非常推荐直接tar方式的安装，笔者曾经试过deb安装，但是安装完之后没反应。
还是参考上面的帖子：
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/1c46bf9300aa48d180e2006a75aaadb6.png)
==注意第二步中路径的差异==

## 3.4 配置docker
参考[我的个人主页](https://haozechang.github.io//posts/2024/05/blog-post-5/)
其中docker hello world这步因为国内的原因可能失败，可以替换一些可用的镜像加速
[国内能用的Docker镜像源【2024最新持续更新】](https://blog.csdn.net/u014390502/article/details/143472743)

## 3.5 配置anaconda

## 3.6 测试：
```python
# test_torch_cuda.py
import torch

if torch.cuda.is_available():
    print("CUDA is available! :)")
    print("CUDA Version:", torch.version.cuda)
else:
    print("CUDA is not available. :(")

# 检查 CUDA 是否可用
if torch.cuda.is_available():
    # 创建一个随机的 tensor
	tuple_data = (1.0,2.0)
	tensor_from_tuple = torch.tensor(tuple_data)

    # 将 tensor 移到 CUDA 设备上
    tensor_cuda = tensor.to('cuda')

    print("Tensor on CUDA:", tensor_cuda)
else:
    print("CUDA is not available. Please check your installation.")
```
注意一定要使用带小数点的张量，笔者亲测有的时候能创建1和2，但是1.0和2.0是有问题的