---
name: image-hosting
description: 将本地图片上传到 GitHub + jsDelivr 图床。当用户提到"上传图片"、"图床"、"图片链接"、"CDN图片"、"jsDelivr"、"GitHub图床"、"生成图片链接"时使用此技能。适用于需要将本地图片转为在线可访问URL的场景。
---

# Image Hosting - GitHub + jsDelivr 图床

将本地图片上传到 GitHub 仓库，通过 jsDelivr CDN 生成全球加速的图片链接。

## 工作流程

### 1. 验证输入

确认用户提供的是有效的本地图片路径：
- 检查文件是否存在
- 检查是否为常见图片格式（jpg, jpeg, png, gif, webp, svg, bmp, ico）

### 2. 复制图片到仓库

```powershell
$sourcePath = "用户提供的图片路径"
$destinationDir = "D:\Git\images-bed"
$imageName = [System.IO.Path]::GetFileName($sourcePath)
$destinationPath = Join-Path $destinationDir $imageName

# 复制文件
Copy-Item -Path $sourcePath -Destination $destinationPath -Force
```

### 3. Git 提交和推送

使用代理配置访问 GitHub：

```powershell
Set-Location "D:\Git\images-bed"

# 配置代理（访问 GitHub 必需）
$env:https_proxy="http://127.0.0.1:33210"
$env:http_proxy="http://127.0.0.1:33210"
$env:all_proxy="socks5://127.0.0.1:7890"

# 添加、提交、推送
git add $imageName
git commit -m "upload: $imageName"
git push origin main
```

### 4. 生成 CDN 链接

推送成功后，生成 jsDelivr CDN 链接：

```
https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/{图片文件名}
```

### 5. 返回结果

向用户返回：
- ✅ 上传成功确认
- 📎 jsDelivr CDN 图片链接
- 📋 可直接复制的 Markdown 图片语法：`![图片描述](链接)`

## 错误处理

| 情况 | 处理方式 |
|------|----------|
| 文件不存在 | 提示用户检查路径 |
| 非图片格式 | 警告但仍继续（用户可能有意上传） |
| 文件名冲突 | 提示是否覆盖，或建议重命名 |
| Git push 失败 | 检查代理配置，提示用户确认 VPN 开启 |
| 同名文件已存在 | 提示用户确认覆盖或添加时间戳后缀 |

## 代理配置说明

访问 GitHub 需要配置代理（前提：用户已开启 VPN）：

```powershell
$env:https_proxy="http://127.0.0.1:33210"
$env:http_proxy="http://127.0.0.1:33210"
$env:all_proxy="socks5://127.0.0.1:7890"
```

⚠️ 如果 push 失败，优先排查：
1. VPN 是否开启
2. 代理端口是否正确（33210/7890）
3. GitHub SSH key 是否配置正确

## 使用示例

**用户说**：把 `C:\Users\nicef\Desktop\photo.jpg` 上传到图床

**执行结果**：
```
✅ 图片上传成功！

📎 CDN 链接：
https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/photo.jpg

📋 Markdown 语法：
![photo](https://cdn.jsdelivr.net/gh/JustWSH/images-bed@main/photo.jpg)
```

## 批量上传

如果用户提供多张图片或一个文件夹：

1. 遍历所有图片文件
2. 逐个复制到 `D:\Git\images-bed`
3. 使用一个 commit 提交所有图片
4. 为每个图片生成对应的 CDN 链接

```powershell
# 批量复制
Get-ChildItem -Path $sourceDir -Include *.jpg,*.png,*.gif,*.webp -Recurse | ForEach-Object {
    Copy-Item $_.FullName -Destination "D:\Git\images-bed\" -Force
}

# 一次性提交
Set-Location "D:\Git\images-bed"
git add .
git commit -m "upload: batch upload images"
git push origin main
```
