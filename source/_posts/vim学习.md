title: vim多行编辑
author: Halfopen
tags:
  - vim
categories:
  - linux
date: 2018-07-26 09:48:00
---
# 多行编辑

## 自带方式

1. ctrl+v 然后上下移动光标选中多行

	![upload successful](/assets/images/vim多行编辑/pasted-0.png)

2. shift+i 或者shift+A 插入内容

	![upload successful](/assets/images/vim多行编辑/pasted-1.png)

3. 按下esc 
	![upload successful](/assets/images/vim多行编辑/pasted-2.png)

## vim-multiple-cursors 插件

.vimrc中添加　Bundle 'terryma/vim-multiple-cursors'

:BundleInstall安装插件
如何在123456后面同时添加789（这里可以要求不对齐）

1. v模式下选中123456
	![upload successful](/assets/images/vim多行编辑/pasted-3.png)

2. ctrl+n 一直按，要选多少个按多少次，这里是3次
	![upload successful](/assets/images/vim多行编辑/pasted-4.png)

3. A开始批量编辑
	![upload successful](/assets/images/vim多行编辑/pasted-5.png)

	![upload successful](/assets/images/vim多行编辑/pasted-6.png)