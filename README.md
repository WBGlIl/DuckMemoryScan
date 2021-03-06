# DuckMemoryScan
一个简单寻找无文件落地后门的工具,由huoji花了1天编写,编写时间2021-02-24

# 运行截图
![image](https://raw.githubusercontent.com/huoji120/DuckMemoryScan/master/%E6%BC%94%E7%A4%BA%E5%9B%BE%E7%89%87.png)

# 功能列表
1. HWBP hook检测 检测线程中所有疑似被hwb挂钩
2. 内存免杀shellcode检测(metasploit,Cobaltstrike完全检测)
3. 可疑进程检测(主要针对有逃避性质的进程[如过期签名与多各可执行区段])
4. 无文件落地木马检测(检测所有已知内存加载木马)
5. 简易rootkit检测(检测证书过期/拦截读取/证书无效的驱动)

# 免杀木马检测原理:
所有所谓的内存免杀后门大部分基于"VirtualAlloc"函数申请内存 之后通过各种莫名其妙的xor甚至是aes加密去混淆shellcode达到"免杀"效果.
本工具通过线程堆栈回溯方法(StackWalkEx函数)遍历线程,寻找系统中在VirtualAlloc区域执行代码的区域,从而揪出"免杀木马"
当然也会存在误报,多常见于加壳程序也会申请VirtualAlloc分配内存.

# 无文件落地木马检测原理:
所有无文件落地木马都是一个标准PE文件被映射到内存中,主要特征如下:
1. 内存区段有M.Z标志
2. 线程指向一个NOIMAGE内存
本工具将会通过第一种特征检测出所有"无文件落地木马"

# 使用方式
编译 运行 得到信息列表

# 追踪这个项目
https://key08.com