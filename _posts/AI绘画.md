
先看最终成果吧

考虑到有些玩票同学基础几乎没有，所以就写的比较详细，就当大家的系统是空白的。

目录

- 配置
- Git
- Python 环境配置
- Stable Diffusion
- stable-diffusion-webui
- 参考

## 配置

我的系统及配置如下
- 系统：Win10专业版
- 处理器：i7-10700
- 内存：16G
- GPU：NVIDIA RTX 2060
- CUDA：11.7

主要吃GPU，我测试了一下

## 准备工作
Git是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
像Disco Diffusion、Stable Diffusion都是在Github开源的项目，我们可以用git命令拉取项目到本地。

下载地址
> https://gitforwindows.org/ 

![20221130111724](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221130111724.png)
点击 download 下载安装,我的版本是Git-2.38.1-64-bit.exe

一路下一步就行了，测试是否安装成功，只需桌面或任意文件夹右键鼠标，看到下图就OK了。

![20221130111735](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221130111735.png)

## Python 环境配置

Python 环境图省事的话可以直接装 Anaconda，这是一个开源的Python发行版本，其包含了conda、Python等180多个科学包及其依赖项。

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20191207233404.png)

Anaconda通过管理工具包、开发环境、Python版本，可大大简化工作流程。

其中conda是一个开源的包、环境管理器，可以用于在同一个机器上安装不同版本的软件包及其依赖，并能够在不同的环境之间切换。比如我们正在做的项目A和项目B分别基于python2和python3，而第电脑只能安装一个环境，这个时候就可以用Anaconda创建多个互不干扰的环境，分别运行不同版本的软件包，以达到兼容的目的，非常方便。

下载地址：https://www.anaconda.com/download/

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20220904212715.png)

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20220904212803.png)

选择下载对应系统位数的安装包，双击下载好的exe文件，一路下一步。出现如下界面，点击 Install 即可。

其中第一项指将Anaconda的默认环境设置添加到系统环境，也就是说如果你之前安装过python并添加到了环境，选了这一项之后原来的python会被覆盖掉，默认使用Anaconda的默认环境。第二项指设置Anaconda的默认环境为python3.9（这个其实无所谓）。

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20220905170930.png)

安装进入“Thanks for installing Anaconda!”界面则意味着安装成功，点击“Finish”完成安装。

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20220905171005.png)

验证

![20221130111759](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221130111759.png)

点击 Anaconda Prompt

输入命令python --version


## stable diffusion



## stable-diffusion-webui

https://sygil-dev.github.io/sygil-webui/docs/Installation/windows-installation

https://github.com/Sygil-Dev/sygil-webui

在命令行输入 git clone https://github.com/sd-webui/stable-diffusion-webui.git
    
有些同学可能登不上github

我这里打包了，访文末了，包括所有配套程序



Download the model into this directory: C:\Users\<username>\sygil-webui\models\ldm\stable-diffusion-v1


https://github.com/CompVis/latent-diffusion


下载stable diffusion模型

进入页面 ：

https://huggingface.co/stabilityai/stable-diffusion-2/blob/main/768-v-ema.ckpt


注：这个模型是用于后续生成AI绘图的绘图元素基础模型库。

![20221130111816](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221130111816.png)

Size of remote file: 5.21 GB

省事点，可以直接把上面地址复制到迅雷就行了





You'll receive warning messages on GFPGAN, RealESRGAN and LDSR but these are optionals and will be further explained below.

In the meantime, you can now go to your web browser and open the link to http://localhost:7860/.

Enter the text prompt required and click generate.

You should be able to see progress in your webui.cmd window. The http://localhost:7860/ will be automatically updated to show the final image once progress reach 100%

Images created with the web interface will be saved to \sygil-webui\outputs\ in their respective folders alongside .yaml text files with all of the details of your prompts for easy referencing later. Images will also be saved with their seed and numbered so that they can be cross referenced with their .yaml files easily.



## 其他
Optional additional models
There are three more models that we need to download in order to get the most out of the functionality offered by Sygil-Dev.

The models are placed inside src folder. If you don't have src folder inside your root directory it means that you haven't installed the dependencies for your environment yet. Follow this step before proceeding.

### GFPGAN
If you want to use GFPGAN to improve generated faces, you need to install it separately.
Download GFPGANv1.3.pth and GFPGANv1.4.pth and put it into the /sygil-webui/models/gfpgan directory.
### RealESRGAN
Download RealESRGAN_x4plus.pth and RealESRGAN_x4plus_anime_6B.pth.
Put them into the sygil-webui/models/realesrgan directory.
### LDSR
Detailed instructions here. Brief instruction as follows.
Git clone Hafiidz/latent-diffusion into your /sygil-webui/src/ folder.
Run /sygil-webui/models/ldsr/download_model.bat to automatically download and rename the models.
Wait until it is done and you can confirm by confirming two new files in sygil-webui/models/ldsr/
(Optional) If there are no files there, you can manually download LDSR project.yaml and model last.cpkt.
Rename last.ckpt to model.ckpt and place both under sygil-webui/models/ldsr/.
Refer to here for any issue.


3333333333333333333


pip install -r requ
pip install streamlit

pip install hydralit
pip install streamlit_server_state

pip install streamlit_nested_layout

pip install -r requirements.txt

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221130111833.png)


![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221130111840.png)

## 用法
https://zhuanlan.zhihu.com/p/570954565

使用
通过前面的安装配置，你就可以通过你设置的端口进行访问。

访问内容后分为几个大的模块;


txt2img --- 标准的文字生成图像；
img2img --- 根据图像成文范本、结合文字生成图像；
Extras --- 优化(清晰、扩展)图像；
PNG Info --- 图像基本信息
Checkpoint Merger --- 模型合并
Textual inversion --- 训练模型对于某种图像风格
Settings --- 默认参数修改
txt2img部分介绍
内容输入部分：


prompt 该部分主要就是对于图像进行描述，有内容风格等信息进行描述。后面的画板可以一些随机的风格、下面箭头是之前任务的参数；

Negative prompt 这个主要是提供给模型，我不想要什么样的风格；特别对于图上出现多个人的情况，就可以通过2girls等信息进行消除；

优化方法部分：


Sampling Steps diffusion model 生成图片的迭代步数，每多一次迭代都会给 AI 更多的机会去比对 prompt 和 当前结果，去调整图片。更高的步数需要花费更多的计算时间，也相对更贵。但不一定意味着更好的结果。当然迭代步数不足（少于 50）肯定会降低结果的图像质量；

Sampling method 扩散去噪算法的采样模式，会带来不一样的效果，ddim 和 pms(plms) 的结果差异会很大，很多人还会使用euler，具体没有系统测试；

Width、Height 图像长宽，可以通过send to extras 进行扩大，所以这里不建议设置太大[显存小的特别注意]；

Restore faces 优化面部，绘制面部图像特别注意；

Tiling 生成一个可以平铺的图像；

Highres. fix 使用两个步骤的过程进行生成，以较小的分辨率创建图像，然后在不改变构图的情况下改进其中的细节，选择该部分会有两个新的参数 Scale latent 在潜空间中对图像进行缩放。另一种方法是从潜在的表象中产生完整的图像，将其升级，然后将其移回潜在的空间。Denoising strength 决定算法对图像内容的保留程度。在0处，什么都不会改变，而在1处，你会得到一个不相关的图像；

Batch count、 Batch size 都是生成几张图，前者计算时间长，后者需要显存大；

CFG Scale 分类器自由引导尺度——图像与提示符的一致程度——越低的值产生越有创意的结果；

Seed 种子数，只要中子数一样，参数一致、模型一样图像就能重新；

img2img部分介绍
这部分参数很多与txt2img类似，这里主要说明一下不同部分；

内容输入部分：

这里主要增加的是要模仿的图片，可以是手绘的、也可以是类似的；


其他文字信息类似，这里依然是描述越准确越好；

对于其中参数主要是图像是否要保存相同尺寸：

Just resize、 Crop and resize、 Resize and fill 这三种模式保证图输出效果，因为下面会有新的尺寸，是填充还是性对应缩放；

调整部分


这部分大部分参数与上面一致，主要新增加的是：

Denoising strength 与原图一致性的程度，一般大于0.7出来的都是新效果，小于0.3基本就会原图缝缝补补；

Extras部分介绍
该部分主要将图像进行优化，其中很多方法的模型使用的时候会自动下载，很容易下载失败导致报错。

图片导入，也可以通过其他模块中的send to extras直接使用；


下面相关参数主要是对于图像的优化等工作，具体使用大家可以自己测试。

GFPGAN visibility 主要就是对于图像清晰度进行优化，例如下图：


其他参数使用不多，这里不做过多介绍。

PNG Info部分介绍
该部分主要说明图像大小等信息。




后面的几个模块基本是调整模型何如何训练新的prompt的，这里就不做过多说明。
## 参考

开发者项目库：https://github.com/sd-webui/stable-diffusion-webui
