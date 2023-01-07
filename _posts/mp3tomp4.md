# 我用 AI “拍”了个 MV ，被吓尿了

最近特别清闲，无聊之中玩了一个根据音乐自动生成视频的项目——`Video Killed The Radio Star` ，给定一个 `MP3 or Youtube URL` 就可以制作视频。

我用它生成了一个泰坦尼克主题曲《我心永恒》的MV，简直是地狱风格，反正被吓尿了，大家感受一下：


本来我也不怎么乐观，想要生成真正能看的MV，AI还有很远的路要走。

## Video Killed The Radio Star 原理

① 根据该文本提示生成一个图像（使用 stable diffusion）。

② 将生成的图像作为 init_image，与文本提示重新组合，生成与第一个图像相似的变化。这将产生一个基于原始文本提示的极其相似的图像序列。

③ 图像被智能地重新排序，以找到这些帧的最平滑的动画序列。

④ 根据需要重复这个图像序列来填充动画的时间。

先浅看一下中间过程吧，他会根据歌词生成图像，很其他AI绘画产品没什么区别
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221018191017.png)

比如歌词：`I believe that the heart does go on`

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221018193435.png)

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221018193543.png)

还有一句歌词生成的蛮靠谱，居然有种泰坦尼克正在下沉，人们纷纷跳船的感觉。

歌词：`And youre here in my heart and My heart will go on and on `

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221018193736.png)

## “完整”实现方法

这项目可以在`colab`直接运行，没学会上网的同学就关了本文吧。

> colab.research.google.com/github/dmarx/video-killed-the-radio-star/blob/main/Video_Killed_The_Radio_Star_Defusion.ipynb#scrollTo=oPbeyWtesAoh

我就不详细介绍每一步了，这里只介绍容易出问题的几个步骤和解决办法。

PS：首次接触，项目中很多参数我也尚未搞明白

## 问题 1
`Installations` 中 `Provide your API Key` 这一步需要提供你`huggingface` 的`API`

注册`huggingface`后访问

> https://huggingface.co/settings/tokens

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221018172042.png)

把`Access Tokens` 复制到 `Colab` 即可


![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221018182403.png)

## 问题 2
`Infer speech from audio` 这一步需要修改`video_url`，去YouTube 找个MV即可，比如我找的是泰坦尼克主题曲《我心永恒》

> https://www.youtube.com/watch?v=3gK_2XdjOdY

## 问题 3
`Generate init images` 这一步也会出问题，解决办法很简单，访问：

https://huggingface.co/CompVis/stable-diffusion-v1-4

选中☑️后点击 `Access repository` 即可
![20221018171534](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221018171534.png)


## 问题 4
Compile your video! 这一步不能框选add_caption这个参数
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221018201350.png)

## 问题 5

`Generate init images` 这一步中的`theme_prompt`:

> by ralph steadman and radiohead,  so detailed, beautiful, amazing, provocative

`RalphSteadman` 是一位专辑封面的艺术家,他为小说《Fear and Loathing in Las Vegas》绘制的插图是其代表作品。

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221018190105.png)

`Radiohead` 是一个英国摇滚乐队

怪不得我生成的MV如此惊悚！

这里我咩有改，和其他AIGC一样，重点调试这个`theme_prompt`才会获得不同风格的MP4，不过每次都太费事、费时了，各种bug，网络不稳，GPU不稳，跑一次俩小时过去了。下次我再尝试吧，首发视频号，敬请期待。
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/WechatIMG491.jpeg)