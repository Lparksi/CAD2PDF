# CAD2PDF - 命令行DXF转换工具

> 精简版LibreCAD，专注于DXF/DWG文件到PDF/PNG/SVG的命令行转换

## 🎯 项目特点

- ✅ **纯命令行**：无GUI依赖，适合服务器和自动化脚本
- ✅ **轻量级**：相比完整LibreCAD减少约100MB代码和资源
- ✅ **多格式支持**：DXF/DWG → PDF/PNG/JPG/SVG
- ✅ **跨平台**：支持Windows/Linux/macOS
- ✅ **高质量输出**：保留LibreCAD核心渲染引擎

## 📦 安装

### 从GitHub Actions下载
访问 [Releases](https://github.com/你的用户名/CAD2PDF/releases/tag/cli-latest) 下载最新构建：
- **Linux**: `CAD2PDF-Linux-x64.tar.gz`
- **macOS**: `CAD2PDF-macOS-arm64.tar.gz`
- **Windows**: `CAD2PDF-Windows-x64.zip`

### 从源码编译
```bash
# 依赖: CMake 3.28+, Qt 6.4+, Boost 1.55+
cmake -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build
```

## 🚀 使用方法

### DXF转PDF
```bash
# 基础用法
dxf2pdf drawing.dxf

# 指定输出文件
dxf2pdf input.dxf -o output.pdf

# 自动适配A4纸张并居中
dxf2pdf drawing.dxf -a -c -p A4

# 黑白模式，自定义纸张尺寸（单位：mm）
dxf2pdf drawing.dxf -m -p 297x420 -o output.pdf

# 指定比例（如1:100）
dxf2pdf drawing.dxf -s 0.01 -o output.pdf
```

**常用参数**：
- `-a, --fit` - 自动适配页面大小
- `-c, --center` - 居中放置图形
- `-m, --monochrome` - 黑白模式
- `-k, --grayscale` - 灰度模式
- `-p, --paper <size>` - 纸张尺寸（A0-A4, B0-B5, Letter, Legal, 或 宽x高）
- `-r, --resolution <dpi>` - 输出分辨率（默认300）
- `-s, --scale <ratio>` - 输出比例（如 0.01 表示 1:100）
- `-o, --outfile <file>` - 输出文件名

### DXF转PNG
```bash
# 默认分辨率（2000x1000）
dxf2png drawing.dxf

# 自定义分辨率
dxf2png drawing.dxf -r 4000x2000 -o output.png

# 指定输出文件
dxf2png input.dxf -o high-res.png
```

**参数**：
- `-r, --resolution <WxH>` - 图片尺寸（像素）
- `-o, --outfile <file>` - 输出文件名

### DXF转SVG
```bash
# 转换为矢量SVG
dxf2svg drawing.dxf -o output.svg
```

### 批量转换
```bash
# Linux/macOS
for file in *.dxf; do
    dxf2pdf -a -c -p A4 "$file" -o "${file%.dxf}.pdf"
done

# Windows PowerShell
Get-ChildItem *.dxf | ForEach-Object {
    .\dxf2pdf.exe -a -c -p A4 $_.FullName -o "$($_.BaseName).pdf"
}
```

## 📋 支持的格式

### 输入格式
- **DXF**: AutoCAD R12-R2018 (所有版本)
- **DWG**: AutoCAD R12-R2018 (通过libdxfrw)
- **JWW**: JW_CAD格式

### 输出格式
- **PDF**: 矢量PDF（适合打印）
- **SVG**: 矢量图形（适合网页）
- **PNG/JPG**: 位图（适合预览）

## 🛠️ 技术栈

- **核心引擎**: LibreCAD 2.2.2 (CAD引擎和渲染器)
- **DXF库**: libdxfrw 0.5.11 (DXF/DWG读写)
- **GUI框架**: Qt 6.4+ (仅Core/PrintSupport/Svg模块)
- **数学库**: muParser, Boost
- **构建系统**: CMake 3.28+

## 📐 示例

### 工程图纸转PDF
```bash
# 工程标准：A3横向，黑白，300 DPI
dxf2pdf blueprint.dxf -m -p A3 -r 300 -a -c -o blueprint.pdf
```

### 高清预览图
```bash
# 生成4K预览图
dxf2png complex-drawing.dxf -r 3840x2160 -o preview.png
```

### 网页展示
```bash
# 转换为SVG供网页使用
dxf2svg floor-plan.dxf -o plan.svg
```

## 🔄 与完整LibreCAD的区别

| 特性 | CAD2PDF CLI | 完整LibreCAD |
|------|-------------|--------------|
| 文件大小 | ~20MB | ~120MB |
| GUI界面 | ❌ | ✅ |
| 命令行转换 | ✅ | ✅ |
| 绘图编辑 | ❌ | ✅ |
| 插件支持 | ❌ | ✅ |
| 服务器部署 | ✅ | ❌ |
| 批量处理 | ✅ | 有限 |

## 🤝 贡献

本项目基于 [LibreCAD](https://github.com/LibreCAD/LibreCAD) 精简而来，保留核心转换功能。

## 📄 许可证

GPL-2.0 - 与LibreCAD相同的许可证

## 🔗 相关链接

- [LibreCAD官网](https://librecad.org/)
- [LibreCAD GitHub](https://github.com/LibreCAD/LibreCAD)
- [问题反馈](../../issues)
