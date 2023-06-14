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
没啥可配置的，下载完成重启电脑就是
![msvc-cpp](../dev-env/img/msvc-cpp.png)

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

使用vscode打开你的项目，新建一个.vscode文件夹

### 配置launch.json
在.vscode文件夹下，新建launch.json文件，并复制以下内容进去    
然后看注释修改两个地方   

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Build Plugin",
            // 注意修改  BDS路径
            "program": "C:\\Server\\Beta\\bedrock_server_mod.exe",
            "type": "cppvsdbg",
            "request": "launch",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceRoot}",
            "environment": [],
            // 调试控制台  internalConsole使用VSC内置控制台  externalTerminal外部控制台
            "console": "externalTerminal",
            "preLaunchTask": "build",
            "logging": {
                "moduleLoad": false
            }
        },
        // 附加调试
        {
            "name": "(vsdbg) 附加",
            "type": "cppvsdbg",
            "request": "attach",
            "processId": "${command:pickProcess}",
            "logging": {
                "moduleLoad": false,
                "trace": true
            },
            // 注意修改  附加PDB
            "visualizerFile":"D:\\Repo\\test-c\\build\\Release\\plugin.pdb"
        }
    ]
}
```

### 配置tasks.json
在.vscode文件夹下，新建tasks.json文件，并复制以下内容进去    

```json
{
    "version": "2.0.0",
    "tasks": [
		{
			"type": "shell",
			"label": "cmake",
			"command": "cmake -B ./build ."
		},
		{
			"type": "shell",
			"label": "make",
			"command": "cmake --build ./build --config=Debug"
		},
		{
			"label": "build",
			"dependsOrder": "sequence",
			"dependsOn": [
				"cmake",
				"make"
			]
		}
	]
}
```

配置完以上两个文件, 按F5尝试编译   
为什么叫尝试？ 因为100%不行，还要配置一点东西   

