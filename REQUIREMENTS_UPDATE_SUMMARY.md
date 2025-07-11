# TimeNest Requirements 更新总结

## 🎯 更新目标

基于代码分析和最佳实践，对 TimeNest 项目的依赖管理进行全面优化，提高项目的可维护性、安全性和部署便利性。

## 📋 更新内容

### 1. 依赖文件重构

#### 原有结构
- `requirements.txt` - 包含所有依赖（运行时+开发工具）

#### 新结构
- `requirements.txt` - 核心运行时依赖
- `requirements-minimal.txt` - 最小依赖（仅核心功能）
- `requirements-dev.txt` - 开发依赖（测试、构建、文档工具）
- `requirements-prod.txt` - 生产依赖（固定版本）

### 2. 依赖版本更新

| 包名 | 原版本 | 新版本 | 更新原因 |
|------|--------|--------|----------|
| PyQt6 | >=6.4.0 | >=6.6.0 | 性能改进和bug修复 |
| pandas | >=1.5.0 | >=2.0.0 | 重大性能提升 |
| numpy | >=1.21.0 | >=1.24.0 | 安全更新 |
| requests | >=2.28.0 | >=2.31.0 | 安全漏洞修复 |
| Pillow | >=9.0.0 | >=10.0.0 | 安全更新 |
| cryptography | >=3.4.8 | >=41.0.0 | 重要安全更新 |

### 3. 新增依赖

#### 核心依赖
- `psutil>=5.9.0` - 系统信息监控（性能管理器需要）
- `sentry-sdk>=1.32.0` - 错误监控和日志

#### 开发依赖
- `pytest-cov>=4.1.0` - 测试覆盖率
- `pytest-mock>=3.11.0` - 测试模拟
- `isort>=5.12.0` - 导入排序
- `bandit>=1.7.5` - 安全检查
- `safety>=2.3.0` - 依赖安全扫描
- `pre-commit>=3.4.0` - Git钩子
- `memory-profiler>=0.61.0` - 内存分析
- `line-profiler>=4.1.0` - 性能分析

### 4. 移除的依赖

- `pyttsx3>=2.90` - 代码中未实际使用，使用系统原生TTS
- `pygame>=2.1.0` - 代码中未找到使用

## 🔧 安装方式

### 标准用户
```bash
pip install -r requirements.txt
```

### 最小安装
```bash
pip install -r requirements-minimal.txt
```

### 开发者
```bash
pip install -r requirements-dev.txt
```

### 生产环境
```bash
pip install -r requirements-prod.txt
```

### 使用 setup.py
```bash
# 基础安装
pip install .

# 开发环境
pip install .[dev]

# 完整安装
pip install .[dev,build,docs,security]
```

## 🛠️ 新增工具

### 1. 依赖检查脚本
- `check_dependencies.py` - 检查所有依赖是否正确安装

### 2. 依赖更新脚本
- `update_requirements.py` - 自动检查和更新过时的依赖

### 3. 安装指南
- `INSTALL.md` - 详细的安装说明文档

## 📊 优势

### 1. 分层管理
- **清晰分离**: 运行时依赖与开发工具分离
- **按需安装**: 用户可根据需求选择安装级别
- **减少体积**: 生产环境无需安装开发工具

### 2. 版本控制
- **安全更新**: 修复已知安全漏洞
- **性能提升**: 使用最新稳定版本
- **兼容性**: 保持向后兼容

### 3. 开发体验
- **完整工具链**: 包含测试、格式化、检查工具
- **自动化**: 提供自动更新和检查脚本
- **文档完善**: 详细的安装和使用说明

### 4. 生产就绪
- **固定版本**: 生产环境使用确定版本
- **安全扫描**: 集成安全检查工具
- **监控支持**: 集成错误监控

## 🚀 使用建议

### 开发阶段
```bash
# 安装开发依赖
pip install -r requirements-dev.txt

# 运行代码检查
black .
flake8 .
bandit -r .
safety check

# 运行测试
pytest tests/ --cov=.
```

### 部署阶段
```bash
# 生产环境安装
pip install -r requirements-prod.txt

# 依赖检查
python check_dependencies.py
```

### 维护阶段
```bash
# 检查更新
python update_requirements.py

# 安全扫描
safety check
bandit -r .
```

## 🔄 迁移指南

### 从旧版本迁移
1. 备份当前环境：`pip freeze > old_requirements.txt`
2. 创建新虚拟环境：`python -m venv new_env`
3. 激活环境：`source new_env/bin/activate`
4. 安装新依赖：`pip install -r requirements.txt`
5. 测试应用功能
6. 如有问题，参考 `old_requirements.txt` 调试

### 持续集成更新
更新 CI/CD 配置文件，使用新的依赖文件：
```yaml
# 示例 GitHub Actions
- name: Install dependencies
  run: |
    pip install -r requirements.txt
    pip install -r requirements-dev.txt  # 仅测试环境
```

## 📝 注意事项

1. **虚拟环境**: 强烈建议使用虚拟环境隔离依赖
2. **版本锁定**: 生产环境建议使用 `requirements-prod.txt`
3. **定期更新**: 定期运行 `update_requirements.py` 检查更新
4. **安全扫描**: 定期运行 `safety check` 检查安全漏洞
5. **测试验证**: 更新依赖后务必运行完整测试套件

## 🎉 总结

通过这次依赖管理重构，TimeNest 项目获得了：
- ✅ 更清晰的依赖结构
- ✅ 更安全的依赖版本
- ✅ 更完善的开发工具链
- ✅ 更便利的部署方式
- ✅ 更好的维护体验

这为项目的长期发展和维护奠定了坚实的基础。
