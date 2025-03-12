---
title: GPT-4 Claude 3 Gemini Pro对决，还是GPT-4胜一筹.md
author: 老章 mlpy
date: 2024-03-08 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---

这两天折腾了两个Mac上的小应用，一个是从视频抽取音频，一个是短视频转Gif。

功能分别是将视频文件/文件夹拖拽到图标上，自动抽取视频中的音频文件；将短视频拖拽到图标上，自动转成Gif格式并保存到桌面。

![](https://r2.zhanglearning.com/blog/2024/03/29507fc08da685a9be690aad79ddc8cb.png)

这件事必然交给大模型来做最合适了，为了对比，我同时让GPT-4、Claude 3 Sonnet、Gemini去帮我生成代码。

以视频转Gif为例，我的Prompt是

> 我想在mac上将mp4格式的短视频转成gif，要求GIF的尺寸与原视频保持一致。我希望你能用Apple script实现它，并另存为application，我想直接讲视频拖拽到这个app的图标上就自动完成gif转换，请给我具体代码。 

结果只有GPT-4给出的代码非常精简、步骤详实且没有语法错误

![](https://r2.zhanglearning.com/blog/2024/03/0cb55ccfcfb59219f82fd4a5fa46ea21.png)

这个脚本之需要将其中ffmpeg的位置修改为自己电脑上的实际位置即可

![](https://r2.zhanglearning.com/blog/2024/03/ae32f2f3f34ecde806d8547856c213c7.png)

我对Apple script一无所知，所以没有深究其他大模型给出代码的实际问题，只知道在运行时会报出语法错误。

Claude 3 、Gemini，mistral，还有不点名的国产大模型，均败北。

![](https://r2.zhanglearning.com/blog/2024/03/98858eb1374196f39d5cda7e1a0d231f.png)



附件

顺便分享这三个小玩意儿的代码



Mp4转Gif：

```
on open of theFiles
    set desktopPath to POSIX path of (path to desktop)
    
    repeat with aFile in theFiles
        set filePath to POSIX path of aFile
        set fileName to do shell script "basename " & quoted form of filePath
        set destPath to desktopPath & text 1 thru -5 of fileName & ".gif"
        
        set shellCommand to "/opt/homebrew/bin/ffmpeg -i " & quoted form of filePath & " -vf \"fps=10,scale=-1:-1:flags=lanczos\" -c:v gif -f gif " & quoted form of destPath
        
        do shell script shellCommand
    end repeat
end open

```



Video抽取音频

```bash
on open of theFiles
    set desktopPath to POSIX path of (path to desktop)
    
    repeat with aFile in theFiles
        set filePath to POSIX path of aFile
        set fileName to do shell script "basename " & quoted form of filePath
        set destPath to desktopPath & text 1 thru -5 of fileName & ".gif"
        
        set shellCommand to "/opt/homebrew/bin/ffmpeg -i " & quoted form of filePath & " -vf \"fps=10,scale=-1:-1:flags=lanczos\" -c:v gif -f gif " & quoted form of destPath
        
        do shell script shellCommand
    end repeat
end open

```



webp转PNG

```bash
on open of theFiles
	repeat with aFile in theFiles
		set filePath to POSIX path of aFile if filePath ends with "-webp" then
		set outputPath to POSIX path of (path to desktop folder) & (do shell scri do shell script "sips-s format 					png " & quoted form of filePath & " --out
end if end repeat
end open
```



使用方法

1. 打开“脚本编辑器”（Script Editor）应用程序。
2. 粘贴上述AppleScript代码到脚本编辑器中。
3. 在脚本编辑器中，选择“文件” > “导出...”。
4. 在“导出”对话框中，选择文件格式为“应用程序”，给你的应用程序命名，然后保存。
5. 确保在“选项”下勾选了“保留运行时的父脚本”。