# 白 · QQ 陪伴角色工程

一个跑在 AstrBot 上的 QQ 陪伴机器人「白」的工程备份：人设、日程、生图提示词、表情包与 ComfyUI 工作流。

## 目录

| 目录 | 内容 |
|---|---|
| `persona/` | 角色人设全文（世界观、说话方式、边界规则） |
| `prompts/` | 生图提示词基底、穿搭思路、Q 版表情包提示词 |
| `schedule/` | 角色日常日程设定（作息、突发事件池、衣柜） |
| `stickers/` | Q 版表情包 13 张（300×300 透明 PNG） |
| `workflows/` | ComfyUI 工作流（SDXL / anima 两套） |

## 技术栈

- **运行时**：AstrBot 4.x + NapCat（QQ 协议端）
- **绘图**：ComfyUI（本地 RTX 4060）
  - `bai_qwen.json`：anima-base（Qwen-Image 系，16 通道），画风细腻
  - `bai_txt2img.json`：Illustrious-XL + 角色 LoRA（纯 SDXL 系）
  - `bai_photo.json` / `bai_sdxl.json`：homochiXL + 风格 LoRA
- **人格注入**：lorebook + system prompt

## 已知坑（踩过的）

1. **LoRA 不能混底模**：anima 系模型只能配 anima 专用 LoRA，挂 Illustrious 系 LoRA 会崩色（黄脸/霓虹）。
2. **负向提示词里不要写颜色名**：写 `cyan`/`magenta` 反而会让模型画出该颜色。
3. **两段式工作流要四个提示词节点一起写**：只改第一段，第二段 denoise 0.8 会把内容洗掉。
4. **透明背景 PNG 在部分相册里显示为黑块**：那是相册用黑底渲染透明区域，不是文件损坏。
5. **抠图不要把角色身上的白色当背景**：只去除「从图像四角泛洪可连通」的区域。

## 表情包

`stickers/` 下 13 款，300×300 透明 PNG，可直接导入 QQ：

```
01 困倦  02 打哈欠  03 发呆  04 大哭  05 得意
06 惊讶  07 疑惑    08 委屈  09 暴怒  10 无语
11 开心  12 爱心    13 思考超载
```

## 说明

本仓库为个人项目备份，不含任何 API Key、账号密码或模型权重文件。
