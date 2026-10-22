# K FEN SU · 构建仓库

基于 **KernelSU v3.3.1**（GPL-3.0）改造的 Root 管理器 + 内核模块。

## 一、这个仓库做什么

只放一个 GitHub Actions 工作流，不存源码。运行时会：

1. 从 `https://github.com/tiann/KernelSU` 克隆 `v3.3.1`
2. 改品牌：包名 `com.fenzhi.ksu`、应用名 `K FEN SU`、版本 `1.0.0.0`、FENZHI 图标
3. 关于页写入「基于 KernelSU 修改 / 作者 FENZHI」
4. 编译两个产物：
   - `kernelsu-ko-*.ko` —— 内核模块（写入了 FENZHI 证书指纹）
   - `manager-apk` —— 管理器 APK

## 二、怎么跑

1. 仓库页 → **Actions**
2. 左侧选择 **K FEN SU (clone KernelSU + build)**
3. 右侧 **Run workflow**
4. KMI 默认 `android13-5.10`（设备 Android13 + 内核 5.10.168）
5. 等 15~25 分钟
6. 打开运行记录，底部 **Artifacts** 下载

## 三、产物怎么用

- **管理器 APK**：直接安装（已用 FENZHI 证书签名）
- **kernelsu.ko**：K FEN SU → 安装 → 使用本地 LKM 文件 → 选它

> 模块里写死了 FENZHI 证书指纹，所以只有本仓库编出的 APK 会被识别为管理器，官方 KernelSU 管理器会失效。

## 四、改品牌

修改 `.github/workflows/kfensu-build.yml` 顶部的 `env`：

```yaml
MANAGER_PACKAGE: 'com.fenzhi.ksu'
MANAGER_NAME: 'K FEN SU'
MANAGER_VERSION: '1.0.0.0'
EXPECTED_SIZE: '886'
EXPECTED_HASH: '225839ce...'
```

## 五、许可证

本项目基于 [KernelSU](https://github.com/tiann/KernelSU)，遵循 **GPL-3.0**。
修改者：FENZHI
