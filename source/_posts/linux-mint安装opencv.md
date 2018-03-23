title: linux mint安装opencv
author: Halfopen
tags:
  - opencv
categories: []
date: 2018-03-21 11:11:00
---
## 依赖安装
```shell
[compiler] sudo apt-get install build-essential`
[required] sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
[optional] sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
```


## 下载源码
```shell
cd ~/<my_working _directory>
git clone https://github.com/opencv/opencv.git
```
或者直接从官网下载

	https://codeload.github.com/opencv/opencv/zip/3.4.1

## 编译源码


```shell
cd ~/opencv
mkdir release
cd release
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_QT=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D WITH_OPENGL=ON ..

```
.. 表示上一级目录

## 安装

```shell
make -j4 # 4代表cpu内核个数，可以加快编译速度
sudo make install
```


## 
```cpp
#include <iostream>
#include <opencv2/opencv.hpp>
using namespace std;
using namespace cv;

int main()
{
    Mat srcImage = imread("lena.jpg");
    imshow("srcIMage",srcImage);

    waitKey(0);

    return 0;
}
```
注：你需要保证lena.jpg位于当前目录下。
![upload successful](/assets/images/linux mint安装opencv/lena.jpeg)

    1）执行g++ `pkg-config opencv --cflags` opencv.cpp  -o opencv `pkg-config opencv --libs`   
    2）./opencv  # 运行结果
    
 
![upload successful](/assets/images/linux mint安装opencv/pasted-0.png)
 
 ## 可能出现的错误
 ### 错误1：无法编译通过
 ```
 //home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucnv_compareNames_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucal_close_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucnv_getAvailableName_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucal_openTimeZoneIDEnumeration_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucal_open_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucol_setAttribute_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucal_openTimeZones_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `uenum_close_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucnv_countAliases_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucol_close_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucol_getSortKey_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucal_get_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `uenum_next_58'
//home/h/anaconda3/lib/libQt5Core.so.5: undefined reference to `ucnv_toUnicode_58'
collect2: error: ld returned 1 exit status

 ```
 https://www.cnblogs.com/guiguzhixing/p/6347602.html?utm_source=itdadao&utm_medium=referral
 
安装qt5
 
 export LD_LIBRARY_PATH=/home/h/Qt5.10.1/5.10.1/gcc_64/lib/
 export PATH="$PATH:$LD_LIBRARY_PATH"
 ### 错误2：编译通过，无法执行
 ```
 This application failed to start because it could not find or load the Qt platform plugin "xcb"
 ```
 export LD_LIBRARY_PATH=/home/h/Qt5.10.1/5.10.1/gcc_64/
 export PATH="$PATH:$LD_LIBRARY_PATH"