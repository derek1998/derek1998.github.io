---
layout: post
title:  ubuntu管理员常用命令
date:   2020-11-4
author:     Leo
header-img: img/post_bao_yan.jpg
catalog: true
tags:
    - ubuntu
---

## 用户添加与删除
添加用户lihua：
`$adduser lihua`，用户名必须为小写。
修改lihua的密码：

`$passwd lihua`

若要修改当前登陆用户本人的密码，直接使用`$passwd`。

删除用户lihua：

`$userdel -r lihua`

## 赋予用户root权限

`$sudo vim /etc/sudoers` 打开文件后找到下面一段代码，

```python
# Allow members of group sudo to execute any command

%sudo ALL=(ALL:ALL) ALL
```
添加`lihua ALL=(ALL) ALL`，赋予lihua root权限。

## 设置不同用户的home目录互相不可见

输入`$ls -ld /home/lihua`，输出

`drwxr-xr-x lihua lihua 4096 3月 14 16:18 /home/lihua`

`$sudo chmod 0700 /home/lihua` 0700表示除用户自己外其他用户都不可见，不可编辑。如果换成0777那么就是所有用户都可见，也可编辑。




