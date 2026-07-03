# 呈派号卡-运营商海报模板制作工具

一个基于 HTML Canvas 的运营商号卡海报制作工具。项目用于快速生成中国电信、中国移动、中国联通、中国广电四类运营商的头图海报和详情长图海报，适合号卡分销、产品上架、推广物料制作等场景。

项目是纯前端静态页面，不依赖后端服务。上传到服务器后即可运行。

## 功能特点

- 支持四个运营商模板切换：电信、移动、联通、广电。
- 支持两类海报：
  - 头图海报：800 x 800
  - 详情长图：800 x 1800
- 支持在线编辑海报文案，包括卡名、价格、流量、通话、年龄、首充说明、套餐说明等。
- 预览区实时渲染，输入内容后立即更新画面。
- 支持保存为图片。
- 导出图片自动控制体积：
  - 头图海报控制在 250KB 以内
  - 详情长图控制在 450KB 以内
- 导出文件名会根据运营商、卡名、价格、流量和类型自动生成。
- 详情图中部分固定项目保留模板内容，避免误改关键说明。
- 页面底部包含项目跳转入口。

## 实现原理

项目核心由 `index.html` 和 `assets` 目录组成。

页面加载后，会先读取对应运营商的模板图片，再通过 Canvas 将用户填写的文字绘制到固定位置。不同运营商的颜色、字体大小、文字坐标和默认文案都在 `index.html` 中配置。

保存图片时，程序会将 Canvas 内容转成图片 Blob，并按大小限制自动选择合适的导出格式和压缩质量。优先保证画面清晰度，在超过限制时再逐步压缩。

整体流程：

```text
选择海报类型和运营商
        ↓
加载对应模板底图
        ↓
读取输入框文案
        ↓
Canvas 绘制文字和辅助图形
        ↓
实时预览
        ↓
导出为图片并控制文件大小
```

## 目录结构

```text
.
├── index.html
├── README.md
└── assets
    ├── telecom-template.png
    ├── mobile-template.png
    ├── unicom-template.png
    ├── broadnet-template.png
    ├── detail-telecom-blank.png
    ├── detail-mobile-blank.png
    ├── detail-unicom-blank.png
    ├── detail-broadnet-blank.png
    └── ...
```

主要文件说明：

- `index.html`：页面结构、样式、模板配置、Canvas 绘制逻辑和图片导出逻辑。
- `assets/telecom-template.png`：电信头图模板。
- `assets/mobile-template.png`：移动头图模板。
- `assets/unicom-template.png`：联通头图模板。
- `assets/broadnet-template.png`：广电头图模板。
- `assets/detail-*-blank.png`：四个运营商的详情长图空模板。

## 使用方式

直接用浏览器打开 `index.html` 即可使用。

如果本地浏览器限制图片导出，建议启动一个本地静态服务，例如：

```bash
python -m http.server 8000
```

然后访问：

```text
http://127.0.0.1:8000
```

## 部署方式

这是一个静态项目，部署时上传整个文件夹即可。

必须保持以下结构：

```text
index.html
assets/
```

可以部署到任意静态网站环境，例如：

- Nginx
- Apache
- 宝塔面板静态站点
- GitHub Pages
- Cloudflare Pages
- Vercel
- Netlify

## 模板替换

如果需要替换模板图片，请保持图片尺寸一致：

- 头图模板：800 x 800
- 详情长图模板：800 x 1800

推荐使用以下文件名替换：

```text
assets/telecom-template.png
assets/mobile-template.png
assets/unicom-template.png
assets/broadnet-template.png
assets/detail-telecom-blank.png
assets/detail-mobile-blank.png
assets/detail-unicom-blank.png
assets/detail-broadnet-blank.png
```

替换图片后刷新页面即可生效。

## 自定义文案

默认文案配置在 `index.html` 中的模板对象里：

- `heroTemplates`：头图海报默认文案和颜色配置。
- `detailTemplates`：详情长图默认文案和颜色配置。

每个运营商都有独立配置，可以按需要调整默认卡名、月租价格、流量说明、首充说明等。

## 注意事项

- 请保持模板图片和 `index.html` 的相对路径不变。
- 如果部署到服务器，请确保 `assets` 目录内图片可以被正常访问。
- 不同浏览器对 WebP/JPEG 压缩支持略有差异，建议使用 Chrome、Edge 或其他现代浏览器。
- 导出图片大小限制是为了适配常见平台上传要求，若需要更高清图片，可以在代码中调整 `heroExportMaxBytes` 和 `detailExportMaxBytes`。
- 开源前请确认模板图片、LOGO、文案和品牌素材的授权范围。

## 开源说明

本项目适合作为运营商海报模板制作工具的前端示例。你可以根据自己的业务场景继续扩展：

- 增加更多运营商或地区模板。
- 增加更多字段控制。
- 增加批量生成。
- 增加模板导入功能。
- 增加服务端图片压缩或素材管理。

