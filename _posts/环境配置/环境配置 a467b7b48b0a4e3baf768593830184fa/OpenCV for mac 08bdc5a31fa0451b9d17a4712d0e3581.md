# OpenCV for mac

# Mac

# [homebrew](%E5%9B%BD%E5%86%85%E5%AE%89%E8%A3%85homebrew%20ba3a4edfe1074f48b769251ee2a53225.md)安装opencv

```
brew install opencv
```

# 2. 测试是否安装成功

测试是否安装成功

```
pkg-config --cflags --libs opencv
```

# 3. 配置clion cmakelist

CLion里面去配置创建一个新项目，修改cmakeLists

下面案例中项目名称为c__，修改为自己项目名称即可

```
cmake_minimum_required(VERSION 3.12)

project(c__)

set(CMAKE_CXX_STANDARD 11)

find_package(OpenCV REQUIRED)

include_directories(${OpenCV_INCLUDE_DIRS})
set(CMAKE_CXX_STANDARD 11)

add_executable(c__ main.cpp)

target_link_libraries(c__ ${OpenCV_LIBS})

```

# No package 'opencv' found

安装好后opencv后执行下面这条语句的时候出错：

```
pkg-config --cflags opencv
```

```
Package opencv was not found in the pkg-config search path.
Perhaps you should add the directory containing `opencv.pc'
to the PKG_CONFIG_PATH environment variable
No package 'opencv' found
```

经过网上详细查询资料后，是缺失了opencv.pc这个配置信息文件，故解决方法就是添加这个文件然后将其导入到环境变量中，具体操作如下：

首先创建opencv.pc文件，这里要注意它的路径信息：

```
cd /usr/local/lib
sudo mkdir pkgconfig
cd pkgconfig
sudo touch opencv.pc

```

然后在opencv.pc中添加以下信息，注意这些信息需要与自己安装opencv时的库路径对应：

```
prefix=/usr/local
exec_prefix=${prefix}
includedir=${prefix}/include
libdir=${exec_prefix}/lib

Name: opencv
Description: The opencv library
Version:4.0.1
Cflags: -I${includedir}/opencv4
Libs: -L${libdir} -lopencv_shape -lopencv_stitching -lopencv_objdetect -lopencv_superres -lopencv_videostab -lopencv_calib3d -lopencv_features2d -lopencv_highgui -lopencv_videoio -lopencv_imgcodecs -lopencv_video -lopencv_photo -lopencv_ml -lopencv_imgproc -lopencv_flann  -lopencv_core
~

```

保存退出，然后将文件导入到环境变量：

```
export  PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
```

至此就配置好opencv.pc啦～

再执行 pkg-config --cflags --libs opencv时输出结果如下：

```
-I/usr/local/include/opencv4 -L/usr/local/lib \
-lopencv_shape -lopencv_stitching -lopencv_objdetect \
-lopencv_superres -lopencv_videostab -lopencv_calib3d \
 -lopencv_features2d -lopencv_highgui -lopencv_videoio \
 -lopencv_imgcodecs -lopencv_video -lopencv_photo -lopencv_ml \
 -lopencv_imgproc -lopencv_flann -lopencv_core
```