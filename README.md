# ytlabel

**语言 / Language：** [简体中文](README.md) | [English](README_en.md)

开源（MIT）图像标注工具：**标准标注 + 数据集导出**。基于 Python + Flask，跨平台支持 Windows / Linux / Mac。模型训练不在本工具内，请使用专用训练工具 [ytstudio](https://github.com/yuturuishi/ytstudio)。

- 官网：https://www.yuturuishi.com ｜ 微信：yuturuishi
- Gitee：https://gitee.com/yuturuishi/ytlabel ｜ GitHub：https://github.com/yuturuishi/ytlabel

---

## 功能

- **标注**：矩形、多边形等多种类型；支持图片、视频、LabelMe 数据集导入
- **AI 自动标注**：对接你自行配置的大模型 API（LMStudio、vLLM、ollama、阿里云等）
- **数据集导出**：YOLO 格式，可自定义训练 / 验证 / 测试比例
- **文件管理**：内置文件浏览、上传、下载
- **离线部署**：全部静态资源本地化，支持内网离线运行
- **模型训练**：不在本工具内，请使用 [ytstudio](https://github.com/yuturuishi/ytstudio)

**快捷键**：`Ctrl+S` 保存标注 ｜ `Ctrl+Shift+D` 清除标注

---

## 软件截图

<img width="720" alt="1" src="https://raw.giteeusercontent.com/yuturuishi/images/raw/master/xclabel/v3.0/1.png">
<img width="720" alt="2" src="https://raw.giteeusercontent.com/yuturuishi/images/raw/master/xclabel/v3.0/2.png">
<img width="720" alt="3" src="https://raw.giteeusercontent.com/yuturuishi/images/raw/master/xclabel/v3.0/3.png">
<img width="720" alt="4" src="https://raw.giteeusercontent.com/yuturuishi/images/raw/master/xclabel/v3.0/4.png">
<img width="720" alt="5" src="https://raw.giteeusercontent.com/yuturuishi/images/raw/master/xclabel/v3.0/5.png">
<img width="720" alt="6" src="https://raw.giteeusercontent.com/yuturuishi/images/raw/master/xclabel/v3.0/6.png">

---

## 快速开始

环境要求：Python 3.9+（实测 3.10）、现代浏览器。

```bash
# 创建并激活虚拟环境
python -m venv venv
venv\Scripts\activate           # Windows
# source venv/bin/activate      # Linux / Mac

# 安装依赖
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

# 启动服务
python app.py --host 0.0.0.0 --port 9924
```

浏览器访问 http://127.0.0.1:9924 即可。

---

## 项目结构

```
ytlabel/
├── app.py                 # 主应用
├── AiUtils.py             # AI 自动标注工具类
├── requirements.txt       # 依赖列表
├── config.json            # 应用配置
├── settings.json          # 界面设置
├── language-*.json        # 多语言文案
├── ytlabel.spec           # PyInstaller 打包配置
├── logo.ico               # 应用图标
├── static/                # 静态资源（图标、样式、脚本、Socket.IO 本地库）
├── templates/             # 页面模板：index.html（标注主页）/ ai_config.html / file_manager.html
└── uploads/               # 上传存储（运行时自动创建）
    ├── annotations/       # 标注数据
    ├── config/            # 配置文件
    └── samples/           # 标注图片
```

---

## 技术栈

Flask + Flask-SocketIO ｜ HTML/CSS/JS ｜ OpenCV/PIL ｜ Socket.IO

---

## 版本历史

### v4.0 (当前版本) — 2026/10/04
- **移除内置模型训练**：专注「数据标注 + 数据集导出」，训练改用 [ytstudio](https://github.com/yuturuishi/ytstudio)
- **彻底移除 Ultralytics 依赖**：删除 `pre_models/` 目录与全部官方 YOLO 预训练权重，仓库零 ultralytics 残留
- **项目更名**：xclabel → ytlabel（含 `ytlabel.spec`、页面标题、本地设置项）
- **批量删除优化**：消除标注表 O(N²) 反复读写，新增全局加载遮罩
- **文档整合**：CHANGELOG 并入 README；设置面板精简；合规说明更新

### v3.0 — 2026/05/19
- 新增独立训练面板：YOLO11 训练全流程、断点续训、模型测试与下载
- 训练状态持久化：页面刷新 / SocketIO 重连后自动恢复进度
- 预训练模型目录迁移至 `pre_models`；Socket.IO 本地化，支持离线部署

### v2.x
- **v2.7** — 2026/01/05：标注文件迁移至 `uploads/annotations/`，API 配置迁移至 `uploads/config/`
- **v2.6** — 2026/01/04：新增 AI 自动标注（大模型 / 阿里云）
- **v2.4** — 2026/01/03：优化 RTSP 流与 SocketIO 断连处理；修复打包运行报错
- **v2.3** — 2025/12/30：新增文件管理系统（导航、预览、批量下载/删除、上传）
- **v2.2** — 2025/12/30：标注完成后原图 / 渲染图对比，支持点击放大
- **v2.1** — 2025/12/01：新增 YOLO11 集成；优化标注工具、标签管理与数据集导出
- **v2.0** — 2025/11/29：从 Django 迁移到 Flask，支持视频帧提取、LabelMe 导入、YOLO 导出

### v1.0 — 2025/02/17
- 基础图像标注（矩形、多边形），Python + Django
- v1.0 分支：https://gitee.com/yuturuishi/ytlabel/tree/v1.0

---

## 授权协议

本项目自有代码使用 **MIT** 协议，保留版权信息即可自由使用；第三方库遵循其各自协议。

- **AI 自动标注**：通过你自行配置的大模型 API（LMStudio、vLLM、ollama、阿里云等本地 / 私有服务）完成，**不依赖 Ultralytics 库**。
- **网络请求**：仅与本机服务及你配置的本地 / 私有大模型 API 通信，**不向任何外部服务器回传数据、标注内容或运行信息**。
- **免责**：部署环境、所用模型与数据的合法性由使用者自行负责。ytlabel 按「现状」提供，不作任何担保。
