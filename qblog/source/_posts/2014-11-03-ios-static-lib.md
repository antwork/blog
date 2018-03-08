---
date: 2014-11-03 22:30:12
layout: post
title: iOS static lib使用备忘
categories: 日志
tags: ios
---

关于怎么创建和使用,可以参考这个教程[createing a static library in ios tutorial](http://www.raywenderlich.com/41377/creating-a-static-library-in-ios-tutorial)   
		

几点备忘:
-------  

1. 新建之后不要删除默认生成的xx.h, xx.m,否则编译会出错
2. 默认已经添加了-ObjC(貌似是从某个xcode就自动添加了)
3. 注意直接从外面复制文件到静态库中的话需要检查.m的target是否静态库的target,还是测试的target,是测试的target会导致undefined symbols for architecture 
4. 记得将文件添加到copy file中
5. 静态库内部.h文件的引用**不需要**使用`#import<XXLib/AClass.h>`,直接使用`#import "AClass.h"`就可以了
6. 在Product下的libXX.a右击在Finder中显示,找到外界使用需要引入的.a和头文件文件夹

新建步骤参考:
----------   

1. 新建项目,选择static lib,命名XXLib(注意XXLib.h XXLib.m不要删除   
2. 新增文件(*注意target*)   
3. 将新增文件的头文件添加到XXLib.h中  	
4. 将文件添加到copy file中,在target的setting里	
5. 新增一个aggregate,同时编译模拟器和真机的.a并且通过lipo指令合并,方式是新增target的Build Phases中添加Run Script(**记得替换其中的TGKit文字为自己的lib名称**) 	

# define output folder environment variable
UNIVERSAL_OUTPUTFOLDER=${BUILD_DIR}/TGKit

# Step 1. Build Device and Simulator versions
xcodebuild -target TGKit ONLY_ACTIVE_ARCH=NO -configuration ${CONFIGURATION} -sdk iphoneos  BUILD_DIR="${BUILD_DIR}" BUILD_ROOT="${BUILD_ROOT}"
xcodebuild -target TGKit -configuration ${CONFIGURATION} -sdk iphonesimulator -arch i386 BUILD_DIR="${BUILD_DIR}" BUILD_ROOT="${BUILD_ROOT}"

# make sure the output directory exists
mkdir -p "${UNIVERSAL_OUTPUTFOLDER}"

# Step 2. Create universal binary file using lipo
lipo -create -output "${UNIVERSAL_OUTPUTFOLDER}/lib${PROJECT_NAME}.a" "${BUILD_DIR}/${CONFIGURATION}-iphoneos/lib${PROJECT_NAME}.a" "${BUILD_DIR}/${CONFIGURATION}-iphonesimulator/lib${PROJECT_NAME}.a"

# Last touch. copy the header files. Just for convenience
cp -R "${BUILD_DIR}/${CONFIGURATION}-iphoneos/include" "${UNIVERSAL_OUTPUTFOLDER}/"

6. 选择aggregate target进行,run
7. 打开Product中的.a,找到相关的.a, inclue文件夹


使用步骤参考:
有两种使用方式:
1. 使用项目方式:
2. 使用.a和include文件

使用项目方式:
直接将静态库项目的TGKit.xcodeproj拖入目标项目中,在link lib中添加.a,在depend lib中添加.a

使用.a和include文件,直接拖入项目中