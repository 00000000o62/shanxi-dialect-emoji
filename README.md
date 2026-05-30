# 🏮 你是正宗山西人吗？

用 Emoji 猜山西方言的古风 H5 小游戏。纯前端，离线可玩，打开即用。

## 🎮 快速开始

```bash
git clone https://github.com/00000000o62/shanxi-dialect-emoji.git
cd shanxi-dialect-emoji
# 双击 index.html 即可
```

或下载 [ZIP 包](https://github.com/00000000o62/shanxi-dialect-emoji/archive/refs/heads/master.zip) 解压后双击 `index.html`。

## ✨ 功能

- **31 道山西方言题库**，每局随机 10 题，8 秒限时作答
- **AI 语音朗读**，Edge TTS 神经网络合成，259KB 离线可用
- **古风视觉**，宣纸背景 + 志芒行书毛笔字体 + 卷轴弹窗
- **龙凤榜证书**，Canvas 绘制，支持保存分享
- **趣味反馈**，答错动图 + 方言嘲讽台词
- **完全离线**，无网络依赖，纯静态文件

## 📁 项目结构

```
├── index.html          # 主入口
├── assets/
│   ├── bg.jpg          # 背景图
│   ├── bgm.mp3         # BGM
│   ├── correct-sfx.mp3 # 答对音效
│   ├── correct.jpg     # 答对图片
│   ├── low-score.jpg   # 低分彩蛋
│   ├── wrong.mp4       # 答错动图
│   ├── font.woff2      # 志芒行书字体子集
│   └── words/          # 31 个方言词语音
└── README.md
```

## 🛠 技术栈

HTML5 + CSS3 + Vanilla JS，无框架，无构建工具。

## 📄 License

MIT
