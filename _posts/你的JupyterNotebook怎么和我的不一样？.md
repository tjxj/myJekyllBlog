JR们好

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107115729.png)

`Jupyter Notebook` 想必大家都不陌生了，数据分析或机器学习数据探索时特别方便。

最近对它的颜值越来越不满意，尤其是晚上，感觉很刺眼，于是就换个暗点的主题。

可能有同学还不了解 `Jupyter Notebook` 可以换主题，这里就简单介绍一下，下面我列出了常用的几个主题效果。如果有喜欢的可以安装试试，如无可以 `Ctrl + w`

## 安装主题库
```
pip install jupyterthemes
```

## 查看可用主题

```
!jt -l

Available Themes: 
   chesterish
   grade3
   gruvboxd
   gruvboxl
   monokai
   oceans16
   onedork
   solarizedd
   solarizedl
```

## 切换主题

```
!jt -t chesterish
```

第一次切换主题需要重启`Jupyter Notebook`服务

之后再切换主题，仅需执行命令后`F5`刷新页面即可

下面 9 个主题的效果
![chesterish](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107115821.png)

![grade3](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107120028.png)



![gruvboxd](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107120114.png)

![gruvboxl](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107120153.png)


![monokai](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107120234.png)

![oceans16](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107120317.png)

![onedork](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107120355.png)

![solarizedd](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107120438.png)

![solarizedl](https://my-wechat.oss-cn-beijing.aliyuncs.com/20221107120505.png)


## tips
执行`jt -t chesterish`,有没有发现工具栏没了?

因为jt命令还有很多参数，可调整的内容很多。

我只关注颜色而已，所以没有深入研究，调出工具栏其实很简单，切换主题时加`-T`即可：`jt -t chesterish -T `

```
使用帮助：-h
主题列表：-l
主题名称安装：-t
代码的字体：-f
代码字体大小：-fs（默认值：11 ）
Notebook 字体：-nfNotebook
字体大小：-nfs（ 默认值： 13 ）
Text/MD 单元格的字体：-tfText/MD
单元格字体大小：-tfs （默认值： 13）
Pandas DF Fontsize：-dfs（默认值： 9）
输出面积字形大小：-ofs（默认值： 8.5 ）
介绍页边距 ：-m（默认值： auto）
单元格的宽度：-cellw （ 默认值： 980）
行高：-lineh（默认值： 170 ）
Mathjax 字形大小 (%)：-mathfs（默认值： 100）
光标宽度：-cursw（默认值： 2）
光标的颜色：-cursc
Alt键提示布局：-altp
Alt键Markdown背景颜色：-altmd
Alt键输出背景色：-altout
Vim风格 NBExt* ：-vim
工具栏可见：-T
名称和标识可见：-N
标志可见：-kl
重置默认主题：-r
强制默认字体：-dfonts
```

另 如果刚入门，Python&机器学习开发环境不顺手，可以参考我的这篇付费小文章：
