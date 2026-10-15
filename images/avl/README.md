# Hexo AVL 旋转图 · 宽屏响应式版

用于修复：主题正文宽度较窄、LR / RL 三个步骤无法同屏展示、iframe 高度产生滚动条。

## 1. 替换 HTML

覆盖 Hexo 项目的 `source/image/avl/index.html`。该单文件含所有图、样式、交互脚本，无需额外 SVG。

## 2. 保持原有的 Hexo `_config.yml` 设置

```yaml
skip_render:
  - "image/avl/**"
```

如果 `skip_render` 已存在，只添加该项。

## 3. 把文章中的旧 iframe 换成下面的代码

```html
<div class="avl-wide-embed" style="position:relative;left:50%;transform:translateX(-50%);width:min(1120px,calc(100vw - 40px));max-width:none!important;">
  <iframe src="/image/avl/index.html" title="AVL 平衡树旋转可视化" loading="lazy" style="display:block;width:100%;height:550px;border:0;border-radius:14px;max-width:none;"></iframe>
</div>
```

- 嵌入图宽度上限 1120px，不受文章原来 `width:100%` 的限制。
- 桌面宽度足够时，LR / RL 的三个步骤改成一排；较窄时自动显示两列或一列。
- 子页面会在同源嵌入时自动调整 iframe 高度，不需要在 Markdown 添加 JS；550px 仅为载入前的初始高度。
- 如果文章的父容器启用了 `overflow:hidden`，可能会裁掉超出的部分，需在主题中将文章容器的 `overflow` 改为 `visible`。

## 4. 刷新 Hexo

```bash
npx hexo clean && npx hexo generate && npx hexo server
```

刷新页面时如果浏览器缓存旧 HTML，按 `Ctrl + Shift + R`。

直接打开 `/image/avl/index.html` 也可单独查看图。
