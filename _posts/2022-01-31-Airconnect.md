---
layout: post
title:  使用 Airconnected 将音箱接入 Airplay
date:   2022-01-31
author:     Leo
header-img: img/post_bao_yan.jpg
catalog: true
# toc: true
tags:
    - Something else
---
<!-- * 目录  
{:toc #markdown-toc} -->

## 前言

 本文使用 MacBook，将（小爱）音箱接入 AirPlay，从而可以让手机上的网易云音乐在音箱上直接播放。

 Audio-only! 该方法只能播放纯音频，不能在边在手机上看视频，边在音箱上播放视频声音。且该方法存在 5 秒左右的延迟。

## 所需设备

* MacBook 一台
* 小爱音箱一台，打开音箱的 DLNA 功能（这一步不确定是否需要，最好打开一下。）

## Airconnect 安装并使用
1. 在该 [文件夹](https://github.com/philippe44/AirConnect/tree/master/bin) 中找到 “airupnp-osx-multi” 文件并下载；
2. 将 “airupnp-osx-multi” 文件放入 Documents 中。在 terminal 里定位到 Documents，并输入 “chmod +x airupnp-osx-multi” 并回车，该脚本变成一个可执行文件；
3. 在 terminal 里输入命令 “./airupnp-osx-multi -l 1000:2000” 执行该二进制文件。这时可以在 terminal 里看到很多代码执行信息。等一下下就可以在 AirPlay 里找到小爱音箱；
4. 在 terminal 里面输入 exit，可以停止软件运行；
5. 在 terminal 里面输入 “./airupnp-osx-multi -l 1000:2000 -Z”，可以在后台运行该软件。这时可以直接关掉 terminal 窗口。

## xbar 安装与使用（该软件让你可以直接在通知栏里面点击按钮使用或停止 Airconnect）
1. 在 [该网址](https://github.com/matryer/xbar/releases) 下载最新版并安装，安装完成之后先不要打开；
2. 在 [该网址](https://xbarapp.com/docs/plugins/Music/airconnect.1d.sh.html) 中点击 "open in xbar app" 按钮，打开 xbar 软件并安装插件；
3. 安装完成之后在插件配置界面点击 “open in external editor” 修改代码；
<img src="figures/plugin.png" width="100%">
4. 使用 [代码](https://github.com/derek1998/derek1998.github.io/blob/main/src/xbar_plugin.txt) 替换原有代码：
5. 接着在插件配置界面左上角点击刷新按钮。
6. 在通知栏里找到 xbar 图标，点击 “start Airconnect” 即可开始使用！



