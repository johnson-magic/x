本文参考文档:
[vscode官方文档](https://code.visualstudio.com/docs/cpp/config-linux)
- [一、常用快捷键](#一、常用快捷键)
- [二、重要配置文件](#二、重要配置文件)

# 一、常用快捷键
|快捷键|作用|
|------|------|
|ctrl + shift + x|打开EXTENSIONS, 寻找插件|
|code . |在当前文件夹下打开vscode|
|ctrl + shift + p|打开输入指令窗口|

# 二、重要配置文件
|配置文件|如何生成|作用|
|------|------|------|
|tasks.json|第一次运行的时候自动生成至.vscode文件夹内|存储build配置|
|launch.json|不会自动生成;点击左侧DEBUG三角按钮，"create a launch.json file"|存储debug配置文件|
|c_cpp_properties.json|不会自动生成;'ctrl+shift+p', 选择"c/c++: Edit Configurations(JSON)"|配置的内容基本与task.json文件内容类似|

配置文件中有各种的变量，例如${file}，如果需要查阅这些变量的具体含义，可以查看[这里](https://code.visualstudio.com/docs/editor/variables-reference)。

# 三、实际例子
## 1. 编译并运行一个含有多个文件夹和文件的代码工程
* [multifiles_project](demo/multifiles_project)

tasks.json文件中的
```
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
```
替换为：
```
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}", "${fileDirname}/math/*.cpp",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
```

## 2. 编译并运行一个依赖第三方库的代码工程
以静态库为例,执行以下指令，生成静态库fun.a

```g++ -c fun.cpp```
```ar -crs fun.a fun.o```
* [multifiles_project_base_lib](demo/multifiles_project_base_lib)
tasks.json文件中的
```
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
```
替换为：
```
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}", "${fileDirname}/math/fun.a",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
```
