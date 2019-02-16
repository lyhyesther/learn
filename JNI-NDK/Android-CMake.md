 https://developer.android.com/studio/projects/add-native-code
 https://developer.android.com/studio/projects/configure-cmake

# Android Grade和CMake编译流程
<pre>
1、Gradle 首先调用本地构建脚本CMakeLists.txt （该文件是CMake Project的入口）
2、CMake根据构建脚本中的命令编译C++源文件到一个共享的对象库中(.so文件)，然后Gradle将该文件打包进APK中
3、运行时，通过 System.loadLibrary()来加载本地库文件，加载之后，本地库函数就对java层可用了。
</pre>

# CMake 分模块管理
<pre>
app
|-CMakeLists.txt
|-src
   |-main
      |-cpp
         |-subCppModuleOne
             |-src
             |-CMakeLists.txt
         |-subCppModuleTwo
             |-src
             |-CMakeLists.txt

入口CMakeLists.txt
cmake_minimum_required(VERSION 3.4.1)
add_subdirectory(src/main/cpp/subCppModuleOne)
add_subdirectory(src/main/cpp/subCppModuleTwo)

模块
subCppModuleOne的CMakeLists.txt
cmake_minimum_required(VERSION 3.4.1)
add_library(
        subCppModuleOne 
        
        SHARED
        
        src/native-lib.cpp)
find_library(
        log-lib
        
        log)
target_link_libraries( 
        subCppModuleOne
        
        ${log-lib})
        
subCppModuleTwo的CMakeLists.txt
cmake_minimum_required(VERSION 3.4.1)
add_library(
        subCppModuleTwo 
        
        SHARED
        
        src/native-lib-two.cpp)
find_library(
        log-lib
        
        log)
target_link_libraries( 
        subCppModuleOne
        
        ${log-lib})
</pre>
