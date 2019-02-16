# https://developer.android.com/studio/projects/add-native-code
# https://developer.android.com/studio/projects/configure-cmake

# Android Grade和CMake编译流程
<pre>
1、Gradle 首先调用本地构建脚本CMakeLists.txt （该文件是CMake Project的入口）
2、CMake根据构建脚本中的命令编译C++源文件到一个共享的对象库中(.so文件)，然后Gradle将该文件打包进APK中
3、运行时，通过 System.loadLibrary()来加载本地库文件，加载之后，本地库函数就对java层可用了。
</pre>
