# 编写“Hello World”程序


下方将展示如何在单板上运行第一个应用程序，其中包括新建应用程序、编译、烧写、运行等步骤，最终输出“Hello World！”。


## 示例目录

示例完整目录如下：


  
```
applications/sample/hello
│── BUILD.gn
│── include
│   └── helloworld.h
│── src
│   └── helloworld.c
├── bundle.json
│
│── test
│   └── moduletest
│   └── unittest
│
productdefine/common
└── products
    └── Hi3516DV300.json
```


## 开发步骤

请在源码目录中通过以下步骤创建“Hello World”应用程序：


1. 创建目录，编写业务代码。
   新建applications/sample/hello/src/helloworld.c目录及文件，代码如下所示，用户可以自定义修改打印内容（例如：修改World为OH）。其中helloworld.h包含字符串打印函数HelloPrint的声明。当前应用程序可支持标准C及C++的代码开发。

     
   ```
   #include <stdio.h>
   #include "helloworld.h"
   
   int main(int argc, char **argv)
   {
       HelloPrint();
       return 0;
   }
   
   void HelloPrint()
   {
       printf("\n\n");
       printf("\n\t\tHello World!\n");
       printf("\n\n");
   }
   ```

   再添加头文件applications/sample/hello/include/helloworld.h，代码如下所示。

     
   ```
   #ifndef HELLOWORLD_H
   #define HELLOWORLD_H
   #ifdef __cplusplus
   #if __cplusplus
   extern "C" {
   #endif
   #endif
   
   void HelloPrint();
   
   #ifdef __cplusplus
   #if __cplusplus
   }
   #endif
   #endif
   #endif // HELLOWORLD_H
   ```

2. 新建编译组织文件。
   1. 新建applications/sample/hello/BUILD.gn文件，内容如下所示：
         
       ```
       import("//build/ohos.gni")  # 导入编译模板
       ohos_executable("helloworld") { # 可执行模块
         sources = [       # 模块源码
           "src/helloworld.c"
         ]
         include_dirs = [  # 模块依赖头文件目录
           "include" 
         ]
         cflags = []
         cflags_c = []
         cflags_cc = []
         ldflags = []
         configs = []
         deps =[]    # 部件内部依赖
       
         part_name = "sample"    # 所属部件名称，必选
         install_enable = true  # 是否默认安装（缺省默认不安装），可选
       }
       ```
   2. 新建applications/sample/bundle.json文件，添加sample部件描述，内容如下所示。
         
       ```
       {
           "name": "@ohos/hello",
           "description": "Hello world example.",
           "version": "3.1",
           "license": "Apache License 2.0",
           "publishAs": "code-segment",
           "segment": {
               "destPath": "applications/sample/hello"
           },
           "dirs": {},
           "scripts": {},
           "component": {
               "name": "hello",
               "subsystem": "applications",
               "syscap": [],
               "features": [],
               "adapted_system_type": [
                   "mini",
                   "small",
                   "standard"
               ],
               "rom": "10KB",
               "ram": "10KB",
               "deps": {
                   "components": [],
                   "third_party": []
               },
               "build": {
                   "sub_component": [
                       "//applications/sample/hello:helloworld"
                   ],
                   "inner_kits": [],
                   "test": [
                       "//applications/sample/hello/test:moduletest",
                       "//applications/sample/hello/test:unittest"
                   ]
               }
           }
       }
       ```

       bundle.json文件包含两个部分，第一部分说明该子系统的名称，component定义该子系统包含的部件，要添加一个部件，需要把该部件对应的内容添加进component中去。添加的时候需要指明该部件包含的模块sub_component，假如有提供给其它部件的接口，需要在inner_kits中说明，假如有测试用例，需要在test中说明，inner_kits与test没有也可以不添加。

3. 修改产品配置文件。
   在productdefine\common\products\Hi3516DV300.json中添加对应的hello部件，直接添加到原有部件后即可。

     
   ```
       "usb:usb_manager_native":{},
       "applications:prebuilt_hap":{},
       "applications:hello":{},
       "wpa_supplicant-2.9:wpa_supplicant-2.9":{},
   ```
