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
4. 使用下面的代码替换原有代码：
```
#!/bin/bash

###
#
# Make sure you take care of the <xbar.dependencies>, then
#
# CHANGE THESE
#

readonly path="/Users/leo_ma/Documents/"
readonly processName="airupnp-osx-multi"

#
# NOTE: These values cannot contain single or double quotation marks.
# Would love to know how to get BitBar to parse these correctly!
# (Incidentally, |href also chokes on spaces.)
#
###



# Info

# <xbar.title>AirConnect</xbar.title>
# <xbar.version>v1.1.0</xbar.version>
# <xbar.author>CartoonChess</xbar.author>
# <xbar.author.github>cartoonchess</xbar.author.github>
# <xbar.desc>Launches AirConnect to enable streaming AirPlay audio to Chromecast devices.</xbar.desc>
# <xbar.image>https://user-images.githubusercontent.com/43363630/101709887-aa9f2900-3ad3-11eb-8863-4309a068aa3c.png</xbar.image>
# <xbar.dependencies>airconnect,bash</xbar.dependencies>
# <xbar.abouturl>https://github.com/cartoonchess/bitbar-airconnect</xbar.abouturl>



# Strings

readonly app="AirConnect"



# Icons

readonly onIcon="iVBORw0KGgoAAAANSUhEUgAAACQAAAAkCAYAAADhAJiYAAAACXBIWXMAABYlAAAWJQFJUiTwAAAGX2lUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPD94cGFja2V0IGJlZ2luPSLvu78iIGlkPSJXNU0wTXBDZWhpSHpyZVN6TlRjemtjOWQiPz4gPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iQWRvYmUgWE1QIENvcmUgNi4wLWMwMDMgNzkuMTY0NTI3LCAyMDIwLzEwLzE1LTE3OjQ4OjMyICAgICAgICAiPiA8cmRmOlJERiB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiPiA8cmRmOkRlc2NyaXB0aW9uIHJkZjphYm91dD0iIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtbG5zOmRjPSJodHRwOi8vcHVybC5vcmcvZGMvZWxlbWVudHMvMS4xLyIgeG1sbnM6cGhvdG9zaG9wPSJodHRwOi8vbnMuYWRvYmUuY29tL3Bob3Rvc2hvcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RFdnQ9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZUV2ZW50IyIgeG1wOkNyZWF0b3JUb29sPSJBZG9iZSBQaG90b3Nob3AgMjIuMSAoTWFjaW50b3NoKSIgeG1wOkNyZWF0ZURhdGU9IjIwMTUtMDMtMjFUMDQ6NTQ6MjArMDk6MDAiIHhtcDpNb2RpZnlEYXRlPSIyMDIwLTEyLTEwVDEwOjIzOjQyKzA5OjAwIiB4bXA6TWV0YWRhdGFEYXRlPSIyMDIwLTEyLTEwVDEwOjIzOjQyKzA5OjAwIiBkYzpmb3JtYXQ9ImltYWdlL3BuZyIgcGhvdG9zaG9wOkNvbG9yTW9kZT0iMyIgcGhvdG9zaG9wOklDQ1Byb2ZpbGU9InNSR0IgSUVDNjE5NjYtMi4xIiB4bXBNTTpJbnN0YW5jZUlEPSJ4bXAuaWlkOjk2MzQxY2VkLTRlNmQtNDYxMi1hNzZhLTUzMGU4YmQ4N2RhYiIgeG1wTU06RG9jdW1lbnRJRD0iYWRvYmU6ZG9jaWQ6cGhvdG9zaG9wOmUzMjIyZmNiLWIxMGYtZDU0ZC05NDQ3LWMzZWJiNzdmMWY1NCIgeG1wTU06T3JpZ2luYWxEb2N1bWVudElEPSJ4bXAuZGlkOjQ1ZjAwZjFiLTIyMzEtNDVmYy05NzdhLTI0NGYxM2U1MTM1ZSI+IDx4bXBNTTpIaXN0b3J5PiA8cmRmOlNlcT4gPHJkZjpsaSBzdEV2dDphY3Rpb249ImNyZWF0ZWQiIHN0RXZ0Omluc3RhbmNlSUQ9InhtcC5paWQ6NDVmMDBmMWItMjIzMS00NWZjLTk3N2EtMjQ0ZjEzZTUxMzVlIiBzdEV2dDp3aGVuPSIyMDE1LTAzLTIxVDA0OjU0OjIwKzA5OjAwIiBzdEV2dDpzb2Z0d2FyZUFnZW50PSJBZG9iZSBQaG90b3Nob3AgMjIuMSAoTWFjaW50b3NoKSIvPiA8cmRmOmxpIHN0RXZ0OmFjdGlvbj0iY29udmVydGVkIiBzdEV2dDpwYXJhbWV0ZXJzPSJmcm9tIGFwcGxpY2F0aW9uL3ZuZC5hZG9iZS5waG90b3Nob3AgdG8gaW1hZ2UvcG5nIi8+IDxyZGY6bGkgc3RFdnQ6YWN0aW9uPSJzYXZlZCIgc3RFdnQ6aW5zdGFuY2VJRD0ieG1wLmlpZDo5NjM0MWNlZC00ZTZkLTQ2MTItYTc2YS01MzBlOGJkODdkYWIiIHN0RXZ0OndoZW49IjIwMjAtMTItMTBUMTA6MjM6NDIrMDk6MDAiIHN0RXZ0OnNvZnR3YXJlQWdlbnQ9IkFkb2JlIFBob3Rvc2hvcCAyMi4xIChNYWNpbnRvc2gpIiBzdEV2dDpjaGFuZ2VkPSIvIi8+IDwvcmRmOlNlcT4gPC94bXBNTTpIaXN0b3J5PiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PhYdaq8AAAH7SURBVFiF7ZfRcdswDIa/9jKANqi6gT1B3AniDapsIE9gZYK2E4QbJJ2gygTRBtEG0QbtA4EQoinZdSTlxd8djzQIm78BkpDgwoX38cmMM6CQfkk6wEn/RgY8A38/qD0TBaL8QDHaSoArEyGlBp7iuM7ENbCxGq4STk9AtYgcv87GGj4vtPDJpCJk2RD9gwmopSU5RdB+Oi1v1EMTKqhiuX0zyrE95IAd0M6uRDgmqAV+Al+BW6LbdA5UUEW4oF6ABw7LiBNhbglBlhzYAvfAq/S5zHX4SN0uKSimwEetMjYHrJkhhSrIAd+k3QFNwnePL4K5fG7EfzFyfLriIvgKrIxfkfAZa5X5bhXbx1LW4vfKmn7EMuAPIVKOCTd66pTpCVMafGrsopn4KTsm2k+pCG3xqXqRMYTTZUWtCOHvRNQsgpQcH4V7Y9vRT9+efuraqQQ5fFriBcGn74eMOw7vIFt8f71XkBbXVlqNLxWlLJTJfIl/cHvEC3aEfVYQ9tAjx18S6jO1ssIfcVtSlJz+US44j4qBY68TD/QvvrtIhC7c0k/tzZmCDogf0Lb4h7I1odJ/J1yEN4ST9tvYtVeqE9e/NuMv8Q/YFNg7pozmlM2AHf7v5u69Bg0d+60ZNwM+U9IgkdeU1SPOLf29dMzOiD1FR+JV+sKFc/kHPkbXK6gg7e8AAAAASUVORK5CYII="

readonly offIcon="iVBORw0KGgoAAAANSUhEUgAAACQAAAAkCAYAAADhAJiYAAAACXBIWXMAABYlAAAWJQFJUiTwAAAGX2lUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPD94cGFja2V0IGJlZ2luPSLvu78iIGlkPSJXNU0wTXBDZWhpSHpyZVN6TlRjemtjOWQiPz4gPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iQWRvYmUgWE1QIENvcmUgNi4wLWMwMDMgNzkuMTY0NTI3LCAyMDIwLzEwLzE1LTE3OjQ4OjMyICAgICAgICAiPiA8cmRmOlJERiB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiPiA8cmRmOkRlc2NyaXB0aW9uIHJkZjphYm91dD0iIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtbG5zOmRjPSJodHRwOi8vcHVybC5vcmcvZGMvZWxlbWVudHMvMS4xLyIgeG1sbnM6cGhvdG9zaG9wPSJodHRwOi8vbnMuYWRvYmUuY29tL3Bob3Rvc2hvcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RFdnQ9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZUV2ZW50IyIgeG1wOkNyZWF0b3JUb29sPSJBZG9iZSBQaG90b3Nob3AgMjIuMSAoTWFjaW50b3NoKSIgeG1wOkNyZWF0ZURhdGU9IjIwMTUtMDMtMjFUMDQ6NTQ6MjIrMDk6MDAiIHhtcDpNb2RpZnlEYXRlPSIyMDIwLTEyLTEwVDEwOjI2OjA2KzA5OjAwIiB4bXA6TWV0YWRhdGFEYXRlPSIyMDIwLTEyLTEwVDEwOjI2OjA2KzA5OjAwIiBkYzpmb3JtYXQ9ImltYWdlL3BuZyIgcGhvdG9zaG9wOkNvbG9yTW9kZT0iMyIgcGhvdG9zaG9wOklDQ1Byb2ZpbGU9InNSR0IgSUVDNjE5NjYtMi4xIiB4bXBNTTpJbnN0YW5jZUlEPSJ4bXAuaWlkOjgxYzg2NGI4LTQ0OTQtNDdiNy1iOGY2LTdkNDNiZjgyNzUxZCIgeG1wTU06RG9jdW1lbnRJRD0iYWRvYmU6ZG9jaWQ6cGhvdG9zaG9wOjEyODQ2OTA3LTBjMjctODk0Ni1iODJlLTgwN2M0NjFkZTVmZCIgeG1wTU06T3JpZ2luYWxEb2N1bWVudElEPSJ4bXAuZGlkOmMwOTBmMjkyLTIwN2EtNDVlYy04Y2ZkLThiMzc0ZjljNDNiMiI+IDx4bXBNTTpIaXN0b3J5PiA8cmRmOlNlcT4gPHJkZjpsaSBzdEV2dDphY3Rpb249ImNyZWF0ZWQiIHN0RXZ0Omluc3RhbmNlSUQ9InhtcC5paWQ6YzA5MGYyOTItMjA3YS00NWVjLThjZmQtOGIzNzRmOWM0M2IyIiBzdEV2dDp3aGVuPSIyMDE1LTAzLTIxVDA0OjU0OjIyKzA5OjAwIiBzdEV2dDpzb2Z0d2FyZUFnZW50PSJBZG9iZSBQaG90b3Nob3AgMjIuMSAoTWFjaW50b3NoKSIvPiA8cmRmOmxpIHN0RXZ0OmFjdGlvbj0iY29udmVydGVkIiBzdEV2dDpwYXJhbWV0ZXJzPSJmcm9tIGFwcGxpY2F0aW9uL3ZuZC5hZG9iZS5waG90b3Nob3AgdG8gaW1hZ2UvcG5nIi8+IDxyZGY6bGkgc3RFdnQ6YWN0aW9uPSJzYXZlZCIgc3RFdnQ6aW5zdGFuY2VJRD0ieG1wLmlpZDo4MWM4NjRiOC00NDk0LTQ3YjctYjhmNi03ZDQzYmY4Mjc1MWQiIHN0RXZ0OndoZW49IjIwMjAtMTItMTBUMTA6MjY6MDYrMDk6MDAiIHN0RXZ0OnNvZnR3YXJlQWdlbnQ9IkFkb2JlIFBob3Rvc2hvcCAyMi4xIChNYWNpbnRvc2gpIiBzdEV2dDpjaGFuZ2VkPSIvIi8+IDwvcmRmOlNlcT4gPC94bXBNTTpIaXN0b3J5PiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PgzdiP0AAAHiSURBVFiF7ZetdoNAEIW/pghEBKIiIgKJRPQBkJGVlX2EPkIfI7KysrIyMiICUVERgYhARCAiEBUVMxsWCklOICSCe86eXWY32cu9sz/AgAHtcGe1XSDUuk/kQKz1npALvACTnskYpMA7kI80EF6RDDp3COBowLYp0dIHfC17Dk7NoARY9MEGiCgIATCqHXZFDISOweTQgv7y5iBuTqGbI2Qsi7QAZMjO+aMlvwYhG56WQJ9jJL+yHvicZFkIvFIoeFHca50h9sTadoFxZayPqLamOxt9ip06ARJDKFcimXaslJxL+dAdI4qtgd0lCB2yLAM+gTmS5AbmquJ1QOgfjEKRThIhijgWiR3wjahj1HKQN1u1nN+nwTK74wHJlRBRaQv8IjnmWaRMjiVdEjpkmQc8A09W7IuyfREdW1ddZSny5vYKmyB5s0aU2gCPVr+rvz0HPkdW2QbJixyYUmycUyW7RXLKo7BuAiyVbGtCTZYt0Uu3FZtZ7UVlfEBHMIQi4A3JGU9jaWViD72IU5x3nROqnmUBIuFcJ11S/iIJkA0TJG9s22xEJ87vW22vjhBIks6AD32OKeyylUiqf3YGIRspNB+uQXXghZGiyhuFEpqvsFlDX1OcA/E6lD6lBwxoiz93TGyVG5zbNAAAAABJRU5ErkJggg=="



# Run app

if [ "$1" = "start" ]; then
	# Must use -Z to keep CPU under control
	# & runs in background so plugin can refresh
	"$path$processName" -l 1000:2000 -Z &
	exit
fi



# Exit app

if [ "$1" = "stop" ]; then
	pid=$(pgrep "$processName")
	kill -s $2 $pid
	# Give the plugin time to wait for the app process to end
	sleep 1
	exit
fi



# Check if app script is running

running=false
ps cax | grep airupnp-osx-multi > /dev/null

if [ $? = 0 ]; then
	running=true
fi



# Show menu bar item

if [ "$running" = true ]; then
	echo "| templateImage=$onIcon"
else
	echo "| templateImage=$offIcon"
fi
echo "---"



# Check that the app can be located and only show help if not

test -f "$path$processName"

if [ $? != 0 ]; then
	echo "$app Not Found"
	echo "Refresh | refresh=true"
	echo "Help"
	echo "-- Set path and filename in .sh file"
	echo "-- Open Plugin Folder… | href=file://${0%/*}/"
	echo "-----"
	echo "-- Download and install $app binary"
	echo "-- Open GitHub Page… | href=https://github.com/philippe44/AirConnect"
	exit
fi




# Show full menu (if app is properly located)

if [ "$running" = true ]; then
	# Running
	echo "Running"
	echo "Stop $app | bash='$0' param1=stop param2=TERM terminal=false refresh=true"
	# Hold opt key to force quit
	echo "Force Quit $app | alternate=true bash='$0' param1=stop param2=KILL terminal=false refresh=true"
else
	# Not running
	echo "Not Running"
	echo "Start $app | bash='$0' param1=start terminal=false refresh=true"
fi

```
5. 接着在插件配置界面左上角点击刷新按钮。
6. 在通知栏里找到 xbar 图标，点击 “start Airconnect” 即可开始使用！


