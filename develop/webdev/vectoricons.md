<script setup>
import { Home, Activity } from 'lucide-vue-next'
</script>

# Lucide图标库

<Activity />

如果你在页面中看到了 `<Home />` 这样的代码并想自己使用，这里告诉你如何操作。Lucide 图标已经集成在项目中，你只需要通过简单的步骤就能插入并使用它们。

> 💡 所有可用图标名称请参考 [Lucide 图标库官网](https://lucide.dev/icons/)（点击图标复制Vue名称）。

## **1. 在页面中插入图标**

你可以在文件顶部的 `<script setup>` 中导入需要的图标：

```vue
<script setup>
import { MousePointer2, Home, User } from 'lucide-vue-next'
</script>

<MousePointer2 />
<Home color="blue" />
<User :size="28" />
```

## **2. 自定义图标外观**

所有图标都支持以下常用属性，你可以像给 HTML 标签加属性一样来调整它们：

| 属性名            | 说明                                     | 示例                              |
| ----------------- | ---------------------------------------- | --------------------------------- |
| `:size`           | 图标宽高（像素），默认 24                 | `<Camera :size="32" />`           |
| `color`           | 图标颜色，默认继承父元素文字颜色           | `<Camera color="#ff6b6b" />`      |
| `stroke-width`    | 线条粗细，默认 2                          | `<Camera stroke-width="1.5" />`   |
| `fill`            | 填充色（部分图标支持）                    | `<Camera fill="lightblue" />`     |
| `class`           | 自定义 CSS 类名                           | `<Camera class="my-icon" />`      |

你也可以绑定任何标准 SVG 属性或事件：
```html
<Camera @click="handleClick" style="margin: 0 8px;" />
```

## **3. 让图标可以被屏幕阅读器识别**

默认图标对读屏软件是隐藏的（`aria-hidden="true"`）。如果图标承载了重要含义（如按钮中的“完成”图标），请添加 `aria-label`：

```html
<Check aria-label="任务已完成" color="green" />
```

## **4. 注意事项**

- **按需使用**：只导入你用到的图标，避免项目体积过大。
- **名称大小写**：图标组件名使用 **PascalCase**（首字母大写），例如 `mouse-pointer` 对应 `<MousePointer />`。
- **修改颜色**：如果希望图标跟随文字颜色变化，可以不传 `color` 或设为 `color="currentColor"`。