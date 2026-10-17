# momo-texture-library

Momo Texture Forge 的静态远程图形库。资源目录、ZIP 和缩略图一起发布，可通过图形编辑器订阅。

## 文件结构

- `index.json`：资源ID、版本、下载地址、SHA-256与缩略图地址。
- `resources/`：完整资源 ZIP，含公式或图片及依赖。
- `thumbnails/`：从资源包提取的独立预览图片。
- `index.html`：图库浏览、搜索及下载页面。
- `.nojekyll`：让 GitHub Pages 直接发布静态文件。

## 发布到 GitHub Pages

提交并推送这些文件，在仓库 **Settings → Pages** 中选择 **Deploy from a branch → main → /(root)** 并保存。

部署完成后的图库首页：

```text
https://fgh23387736.github.io/momo-texture-library/
```

在 Momo Texture Forge 的“图形库 → 远程图库”中添加：

```text
https://fgh23387736.github.io/momo-texture-library/index.json
```

以上地址在 Pages 成功部署后生效；首次发布后需验证目录与资源可以正常读取。

## 更新资源

从编辑器导出资源 ZIP，然后使用 Momo Texture Forge 提供的打包工具。以下命令在本仓库目录执行，先替换两处路径占位符：

```text
node "<TextureForge工具目录>/build-remote-library.mjs" --input "<导出的资源ZIP路径>" --out "." --name "Momo Texture Library"
```

继续使用同一目录可保留图库身份并合并新资源和更高版本；未涉及的条目与旧资源文件保留。相同ID和版本不可对应不同的资源内容。打包后提交并推送，等待 Pages 完成部署。

缩略图从资源包已有的预览提取；原包没有预览时，当前工具不会自动渲染补图。图库浏览页始终读取最新的 `index.json`，无需逐个手工维护卡片。
