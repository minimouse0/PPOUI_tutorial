# VSCode + MSVC + CMake 开发环境配置   

## 所需工具
1. 一个聪明的大脑
2. 一台电脑

好了不开玩笑了

> [!warning]
> 您的电脑系统必须为Windows 10/11 x64  

1. [Git]()
2. [VSCode]()
3. [MSVC 2022编译器]()
4. [CMake]()
5. [Minecraft Bedrock Server]() + [Liteloader BDS]() 
6. [GitHub DeskTop]() (可选)

### VSCode扩展
1. C/C++
2. C/C++ Themes
3. C/C++ Extension Pack
4. CMake
5. CMake Tools
6. CMake Language Support(可选)

## 配置MSVC


## 安装&配置CMake

没什么重要的配置，版本我下的是3.27-rc2，最新的就行

一路下一步, 直到这个页面
![cmake](../dev-env/img/cmake.png)

建议选择第二个，省去很多麻烦

安装完成，打开cmd，输入cmake，看看cmake环境变量是否正常
![cmake-path-err](../dev-env/img/cmake-path-err.png)
如果和我一样，显示不是内部或外部命令，就代表cmake环境变量不正常，需要手动添加cmake环境变量

右键 计算机 > 属性 > 高级系统设置 > 环境变量 > 系统变量 > Path

如果没有看到cmake字样代表环境变量缺失，需要手动添加环境变量   
进入你的cmake安装目录，我这里是默认路径，所以是C:\Program Files\CMake\bin    
![cmake-path-err-add](../dev-env/img/cmake-path-err-add.png)
把这个路径添加到环境变量中，然后重启系统即可   

## VScode配置
确保你以按前面要求安装了所需的vscode扩展，再阅读下面的教程  

### 配置launch.json


### 配置tasks.json



