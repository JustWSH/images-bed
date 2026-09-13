# 📷 GitHub + jsDelivr 图床

基于 GitHub 仓库 + jsDelivr CDN 的免费图床方案，图片上传后自动生成全球加速的 CDN 链接。

> 仓库地址：[github.com/JustWSH/images-bed](https://github.com/JustWSH/images-bed)

## 🚀 如何使用

### 方式一：告诉 AI 助手（推荐）

如果你使用了 [DeepSeek Harness](https://github.com/JustWSH/images-bed) 并配置了 `image-hosting` 技能，直接告诉 AI：

```
把 C:\Users\你的用户名\Desktop\photo.jpg 上传到图床
```

AI 会自动完成：复制图片 → git 提交推送 → 生成 CDN 链接，你只需复制粘贴即可。

### 方式二：手动操作

**1. 克隆仓库（首次）**

```bash
git clone git@github.com:JustWSH/images-bed.git
```

**2. 复制图片到仓库目录**

```bash
cp /path/to/your/image.jpg D:\Git\images-bed\
```

**3. 提交并推送**

```bash
cd D:\Git\images-bed
git add .
git commit -m "upload: image.jpg"
git push origin main
```

> ⚠️ 访问 GitHub 需要开 VPN，如果 push 失败请检查网络代理配置。

**4. 生成 CDN 链接**

推送成功后，图片的 CDN 地址格式为：

```
https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/{文件名}
```

例如仓库中的 `张家界大峡谷玻璃桥.jpg`，对应的链接是：

```
https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/张家界大峡谷玻璃桥.jpg
```

## 📝 使用示例

| 用途 | 语法 |
|------|------|
| **Markdown** | `![描述](https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/图片.jpg)` |
| **HTML** | `<img src="https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/图片.jpg" />` |
| **直接访问** | 浏览器打开 `https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/图片.jpg` |

### 效果预览

![张家界大峡谷玻璃桥](https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/张家界大峡谷玻璃桥.jpg)

## 🌐 CDN 加速原理

```
本地图片 → GitHub 仓库存储 → jsDelivr CDN 全球节点分发 → 用户高速访问
```

- **GitHub** 提供免费的文件存储（单文件建议 ≤ 20MB）
- **jsDelivr** 是免费的公共 CDN，在国内有节点，访问速度快
- 图片链接长期有效，只要仓库不删除即可

## 📂 已有图片

| 图片 | 链接 |
|------|------|
| 金鞭溪景区导览图.png | [查看](https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/金鞭溪景区导览图.png) |
| 天门山导览图.jpg | [查看](https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/天门山导览图.jpg) |
| 张家界大峡谷玻璃桥.jpg | [查看](https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/张家界大峡谷玻璃桥.jpg) |
| 张家界大峡谷路线图.jpg | [查看](https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/张家界大峡谷路线图.jpg) |
| 张家界国家森林公园手绘图.jpg | [查看](https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/张家界国家森林公园手绘图.jpg) |

## ⚠️ 注意事项

1. **文件名规范**：建议使用英文或数字命名，避免中文文件名在某些场景下出现编码问题
2. **文件大小**：单文件建议不超过 20MB（GitHub 限制 100MB，但大文件会影响 CDN 缓存速度）
3. **更新延迟**：jsDelivr 有缓存机制，更新图片后可能需要等待几分钟才能生效，或使用 `@版本号` 强制刷新：
   ```
   https://cdn.jsdelivr.net/gh/JustWSH/images-bed@最新commit哈希/图片.jpg
   ```
4. **隐私安全**：此仓库为公开仓库，**不要上传敏感图片**（身份证、密码截图等）

## 📜 License

MIT
