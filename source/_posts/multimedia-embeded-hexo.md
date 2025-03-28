---
title: 插入多媒体文件到Hexo博客
date: 2023-07-02 20:29:34
categories:
- [科技,娱乐]
- [多媒体,视频,图像,音频,博客]
tags: [视频,音频,图像,博客,google drive,vimeo,imgbb,hexo,markdown]
toc: false
---
关于如何从本地硬盘和远程服务器上插入视频，图片和音频文件到Hexo博客的实用科技文章。
<!-- more -->
# 视频文件的插入
## 从本地插入视频文件
1. 将视频文件放到指定路径：首先，我们需要将视频文件放到hexo项目根目录下的`source` folder （为了方便管理，可以创建videos子目录）, 完整路径应该是 "hexo_project/source/videos/video.mp4"。
2. 将视频元素标签加入到hexo博客中：打开hexo博客的markdown文件，如下面所示，将视频路径添加到指定的位置。

```markdown
![My testing video from local drive](/videos/BRAVO_GALA_2019_ORLANDO_FL_Large.mp4)
```
<p align="center">

![My testing video from local drive](/videos/BRAVO_GALA_2019_ORLANDO_FL_Large.mp4)

</p>

这种插入形式从功能上说是没有问题的，但从使用者体验式看就有些差强人意了。主要是视频是以文件的形式显示在网页上的，因此很难引起注意和吸引读者。

一个好的解决办法就是连同视频播放器一起插入到文章中去，这样就需要一些基本的HTML要素

```html
<iframe width="700" height="393" src="/videos/BRAVO_GALA_2019_ORLANDO_FL_Large.mp4" title="Bravo 2019" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
```
显示效果如下：
<p align="center">

<iframe width="700" height="393" src="/videos/BRAVO_GALA_2019_ORLANDO_FL_Large.mp4" title="Bravo 2019" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

</p>

## 从Google Drive上插入视频
本地插入一个很严重的缺点就是视频文件只能保持在本地硬盘的指定位置，一旦变化（删除或移动）视频在网页上将无法显示。云端存储将解决这一问题，我们可以用任何主流的云端存储平台如Google Drive, Microsoft OneDrive, Dropbox等等，这里以Google Drive为例。

1. 首先登陆Google Drive并获取到欲插入文件的分享链接。
2. 从分享链接中获取`file id`
3. 将完整的视频路径添加到播放器HTML中。

默认的分享链接如下所示：
```
https://drive.google.com/file/d/168h5syU2CsSeC6JYkRw3G3_Cl1mSVt2s\view?usp=sharing
```
其中`file id`是"d/"后的一长串字符串**168h5syU2CsSeC6JYkRw3G3_Cl1mSVt2s**
我们需要修改一下文件的URL，将view?usp=sharing改为preview
```
https://drive.google.com/file/d/168h5syU2CsSeC6JYkRw3G3_Cl1mSVt2s\preview
```
将上面的地址添加到HTML中的`src`中就可以了：
```html
<iframe width="700" height="393" src="https://drive.google.com/file/d/168h5syU2CsSeC6JYkRw3G3_Cl1mSVt2s/preview" title="Bravo 2019" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
```
显示效果如下：
<iframe width="700" height="393" src="https://drive.google.com/file/d/168h5syU2CsSeC6JYkRw3G3_Cl1mSVt2s/preview" title="Bravo 2019" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## 从vimeo等video hosting网站上插入视频
更简单和稳定可靠的办法是将视频上传到vimeo, youtube等主流video hosting网站，从那里插入的话还能实现一些更高级的功能比如定制话视频封面thumbnail，视频剪辑和滤镜等等，但缺点是要上传限制，解除这些限制就得付费。

共有两种视频插入的方法，第一种是共享链接，将获取的共享链接添加到`src`作为值，类似与Google Drive。
```html
<iframe width="700" height="393" src="https://vimeo.com/841642634?share=copy" title="Bravo 2019" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
```
这种方法实际上是将vimeo播放页面嵌入进来，所以会有全部的网页信息，包括广告，显示效果如下：
<iframe width="700" height="393" src="https://vimeo.com/841642634?share=copy" title="Bravo 2019" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

第二种方法更简单但效果更好，那就是用video hosting网站提供的`Embed` code，直接插入到Markdown文件中，例如上边的sample video可以用Embed code实现没有网页元素，只是纯粹的播放器。

```html
<div style="padding:48.17% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/841642634?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="BoomScreenRecord"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
```
效果如下：
<div style="padding:48.17% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/841642634?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="BoomScreenRecord"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

## 从youtube上插入视频
方法与vimeo非常相似，不同的是第二种`embed`方法在vimeo可以选择responsive ratio and fxied ration,但在youtube只有fixed ratio, 这个设置显然对跨平台，跨设备显示不是很友好，也就是说固定的视频窗口大小可能在桌面浏览器端显示得很好，但对于平板电脑或者手机就不适合了，为了解决这个问题，我们需要添加一些`html`代码对youtube的default embed code进行一下调整。

例如下面这段youtube视频用的是默认的embed代码
```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/M3DrqV9UFDc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
```
效果如下（需要在不同的设备浏览器上验证）：

<iframe width="560" height="315" src="https://www.youtube.com/embed/M3DrqV9UFDc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

添加了responsive code后，代码变成
```html
<div style="padding:48.17% 0 0 0;position:relative;">
<iframe src="https://www.youtube.com/embed/M3DrqV9UFDc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>
```
显示效果如下：
<div style="padding:48.17% 0 0 0;position:relative;">
<iframe src="https://www.youtube.com/embed/M3DrqV9UFDc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>

<div style="padding:48.17% 0 0 0;position:relative;">
<iframe  src="https://www.youtube.com/embed/z1pIJ_BKE2w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>
# 图片文件的插入
## 本地图片和图床图片的插入
首先明确一下图床网站的定义，对所存储图片提供各种格式链接的网站才是图床（photo hosting server), 关于操作方法可以参考Herman的一篇博客文章 [**How to let local images display on your hexo blog website**](http://blog.hermanteng.net/2020/11/27/How-to-let-local-images-display-on-your-hexo-blog-website/)
## Google Drive中图片的插入
这里有点tricky，图片共享链接不能拿来直接用，因为页面不会显示图片，所以，要对URL进行一下改写和调整，具体来说将默认的共享链接
```
https://drive.google.com/file/d/[image_id]/view?usp=sharing
```
换成下面的格式
```
https://drive.google.com/uc?export=view&id=[image_id]
```
```html
<img src="https://drive.google.com/uc?export=view&id=12AHklgVeAdFvUa-DaT1gNea_Kds03zxh" width="500" height="850">
```
效果如下：
<img src="https://drive.google.com/uc?export=view&id=12AHklgVeAdFvUa-DaT1gNea_Kds03zxh" width="500" height="850">

 音频文件的插入
## 从本地硬盘中插入
与插入视频文件类似，将音频文件放到`source`文件夹中，然后将相对路径写入到`markdown`博客文件中就行了，但为了能更好的用户体验，最好也连播放器一起插入
```html
<audio controls>
  <source src="/audios/BEP040ADV-Interviews1_First_round.mp3" type="audio/mpeg">
</audio>
```
效果如下：
<audio controls>
  <source src="/audios/BEP040ADV-Interviews1_First_round.mp3" type="audio/mpeg">
</audio>

## 从Google Drive上插入

当然为了音频文件的长久有效，还是推荐将文件放到云端服务器上如Google Drive
```markdown
[音频链接](https://drive.google.com/file/d/0B9x2Xs_Sh1eARTdNcGtiMkNyM2s/view?usp=sharing&resourcekey=0-BudwhgjRDp7parGXgmn4ew)
```
效果如下：
[音频链接](https://drive.google.com/file/d/0B9x2Xs_Sh1eARTdNcGtiMkNyM2s/view?usp=sharing&resourcekey=0-BudwhgjRDp7parGXgmn4ew)

## 从music hosting server上插入
最简单的方式是从在线音乐平台网站上获取文件链接然后插入，但前提是需要以会员身份登录获取链接，下面以Google Music为例

### 以链接的形式显示并redirect到Google Music
[斑马，斑马](https://music.youtube.com/watch?v=CsSfrHFKqH0&feature=share)

### 将播放器内嵌到博客网页
```html
<iframe width=100% height=100% src="https://music.youtube.com/watch?v=CsSfrHFKqH0&feature=share"></iframe>
```
效果如下：
<iframe width=100% height=100% src="https://music.youtube.com/watch?v=CsSfrHFKqH0"></iframe>
也可以对播放器外观进行调整例如改变大小比例以便显示唱片封面
```html
<iframe width="700" height="390" src="https://music.youtube.com/watch?v=CsSfrHFKqH0&feature=share"></iframe>
```
<iframe width="700" height="390" src="https://music.youtube.com/watch?v=CsSfrHFKqH0&feature=share"></iframe>






