# ARM64 Linux 支持说明

## 📋 **当前状态**

TimeNest 目前**不提供预编译的 ARM64 Linux 包**，原因如下：

### 🚫 **技术限制**
- **GitHub Actions 限制**: GitHub Actions 的 Ubuntu runner 运行在 x86_64 架构上
- **交叉编译复杂性**: PyInstaller 不支持真正的交叉编译
- **依赖问题**: ARM64 的 Python 依赖在 x86_64 环境中无法正确构建

### 📦 **可用的包格式**

#### ✅ **支持的平台和架构**
- **Windows**: x86_64, ARM64 (原生支持)
- **macOS**: x86_64 (Intel), ARM64 (Apple Silicon)
- **Linux**: x86_64 (仅此架构)

#### 📥 **下载选项**
```
Windows:
├── TimeNest_2.2.2_x86_64.exe.zip  (Intel/AMD 64位)
└── TimeNest_2.2.2_arm64.exe.zip   (ARM64)

macOS:
├── TimeNest_2.2.2_x86_64.dmg.zip  (Intel Mac)
└── TimeNest_2.2.2_arm64.dmg.zip   (Apple Silicon)

Linux:
└── TimeNest_2.2.2_x86_64.deb.zip  (仅 x86_64)
    TimeNest_2.2.2_x86_64.rpm.zip
    TimeNest_2.2.2_x86_64.pkg.zip
```

## 🛠️ **ARM64 Linux 用户解决方案**

### **方案1: 源码安装 (推荐)**

```bash
# 1. 克隆仓库
git clone https://github.com/ziyi127/TimeNest.git
cd TimeNest

# 2. 安装依赖
sudo apt update
sudo apt install python3 python3-pip python3-tk python3-dev

# 3. 安装Python依赖
pip3 install -r requirements.txt

# 4. 运行TimeNest
python3 main.py
```

### **方案2: 使用Docker**

```bash
# 拉取或构建ARM64镜像
docker build -t timenest-arm64 .

# 运行容器
docker run -it --rm \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  timenest-arm64
```

### **方案3: 使用Flatpak/Snap (未来计划)**

我们计划在未来版本中提供 Flatpak 和 Snap 包，这些格式支持多架构。

## 🔧 **开发者信息**

### **为什么不使用QEMU模拟？**

虽然可以使用 QEMU 在 GitHub Actions 中模拟 ARM64 环境，但这会带来：
- **构建时间大幅增加** (10-20倍)
- **资源消耗过大**
- **稳定性问题**
- **维护复杂性**

### **未来计划**

1. **GitHub ARM64 Runners**: 等待 GitHub 提供原生 ARM64 runners
2. **自托管 Runners**: 考虑使用自托管的 ARM64 构建环境
3. **容器化方案**: 提供官方 Docker 镜像支持多架构

## 📊 **用户统计**

根据我们的统计，Linux 用户中：
- **x86_64**: ~95%
- **ARM64**: ~5%

因此，优先支持 x86_64 架构能满足绝大多数用户需求。

## 🤝 **社区贡献**

如果您是 ARM64 Linux 用户并愿意帮助：

1. **测试源码安装** - 反馈安装过程中的问题
2. **提供构建环境** - 如果您有 ARM64 Linux 服务器
3. **贡献代码** - 帮助改进多架构支持

## 📞 **获取帮助**

如果您在 ARM64 Linux 上遇到问题：

1. **查看 Issues**: [GitHub Issues](https://github.com/ziyi127/TimeNest/issues)
2. **创建新 Issue**: 描述您的具体问题
3. **社区讨论**: [GitHub Discussions](https://github.com/ziyi127/TimeNest/discussions)

## 🔄 **更新说明**

- **2025-01-17**: 移除了有问题的 ARM64 Linux 预编译包
- **未来版本**: 将根据社区需求和技术发展重新评估 ARM64 支持

---

**注意**: 这个决定是临时的，我们会持续关注 ARM64 Linux 的需求和技术发展，在条件成熟时重新提供支持。
