# 1st_homework

第一次作业，包含 CMake 多模块构建和 Shell 脚本练习。

## 项目结构

```
.
├── CMake_Test/          # CMake 多模块 C++ 项目
│   ├── CMakeLists.txt   # 顶层 CMake 配置
│   ├── main.cpp         # 入口文件
│   ├── common/          # 公共库
│   │   ├── kalman/      # 基于 cv::Matx 的高性能卡尔曼滤波器
│   │   └── math/        # 数学工具库（距离/角度计算、PnP、坐标变换等）
│   └── modules/         # 功能模块
│       ├── M1/          # 模块1：组合 Lidar、Camera、Planning
│       ├── M2/          # 模块2：组合卡尔曼滤波器与数据队列
│       ├── A1/          # 子模块：传感器抽象（Lidar/Camera/Planning）
│       └── A2/          # 子模块：双端队列封装
└── shell/               # Shell 脚本练习
    ├── task_2_1.sh      # 文件与目录操作脚本
    └── linux_practice/  # 练习用目录结构
```

## CMake_Test

### 依赖

- CMake >= 3.10
- OpenCV >= 4.5.3
- C++14 编译器

### 构建与运行

```bash
cd CMake_Test
mkdir build && cd build
cmake ..
make -j6
./test
```

### 预期输出

```
M1 construct
I'm M1
I'm Lidar
I'm camera
I'm planning
M2: I'm camera
size = 1
dis = 28.2843
M1 destruct
```

### 模块说明

| 模块 | 描述 |
|------|------|
| **kalman** | 基于 `cv::Matx` 的模板卡尔曼滤波器，相比 OpenCV 原版 `cv::KalmanFilter` 使用栈内存分配，运行时性能更高。支持无控制量与带控制量两种模式。 |
| **math** | 机器人常用数学库，包含两点距离、水平/垂直夹角、角度差、相机-装甲板坐标变换（PnP 相关）、三角函数扩展等。 |
| **M1** | 聚合 A1 子模块，演示多传感器（激光雷达、相机、规划）组合调用。 |
| **M2** | 组合卡尔曼滤波器（KalmanFilter44）与 A2 数据队列，演示滤波器与数据结构的集成。 |

## shell

Shell 脚本基础练习，涵盖目录创建、文件操作、权限设置等。

### task_2_1.sh

```bash
bash shell/task_2_1.sh
```

执行流程：
1. 创建 `linux_practice/docs` 和 `linux_practice/backup` 目录
2. 生成文件并清理临时文件
3. 写入内容并追加日期
4. 备份 `.txt` 文件并设为只读
