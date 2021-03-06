---
title: React Icon（图标）组件
components: Icon, SvgIcon
---

# Icons（图标）

<p class="description">一些在 Material-UI 中使用图标的建议和指导。</p>

Material-UI provides icons support in three ways:

1. Standardized [Material Design icons](#material-icons) exported as React components (SVG icons).
1. With the [SvgIcon](#svgicon) component, a React wrapper for custom SVG icons.
1. With the [Icon](#icon-font-icons) component, a React wrapper for custom font icons.

## Material Icons

Material Design has standardized over 1,000 official icons, each in five different "themes" (see below). For each SVG icon, we export the respective React component from the `@material-ui/icons` package. You can search the full list of these icons in our [built-in search page](/components/material-icons/).

### 使用

Install `@material-ui/icons`. Import icons using one of these two options:

- Option 1:

  ```jsx
  import AccessAlarmIcon from '@material-ui/icons/AccessAlarm';
  import ThreeDRotation from '@material-ui/icons/ThreeDRotation';
  ```

- Option 2:

  ```jsx
  import { AccessAlarm, ThreeDRotation } from '@material-ui/icons';
  ```

The safest is Option 1 but Option 2 can yield the best developer experience. Make sure you follow the [minimizing bundle size guide](/guides/minimizing-bundle-size/#option-2) before using the second approach. The configuration of a Babel plugin is encouraged.

Each icon also has a "theme": `Filled` (default), `Outlined`, `Rounded`, `Two tone` and `Sharp`. If you want to import the icon component with a "theme" different than default, append the "theme" name to the icon name. For example `@material-ui/icons/Delete` icon with:

- `Filled` "theme" (default) is exported as `@material-ui/icons/Delete`,
- `Outlined` "theme" is exported as `@material-ui/icons/DeleteOutlined`,
- `Rounded` "theme" is exported as `@material-ui/icons/DeleteRounded`,
- `Two tone` "theme" is exported as `@material-ui/icons/DeleteTwoTone`,
- `Sharp` "theme" is exported as `@material-ui/icons/DeleteSharp`.

Note: The Material Design specification names the icons using "snake_case" naming (for example `delete_forever`, `add_a_photo`), while `@material-ui/icons` exports the respective icons using "PascalCase" naming (for example `DeleteForever`, `AddAPhoto`). There are three exceptions to this naming rule: `3d_rotation` exported as `ThreeDRotation`, `4k` exported as `FourK`, and `360` exported as `ThreeSixty`.

{{"demo": "pages/components/icons/SvgMaterialIcons.js"}}

## SvgIcon（Svg 图标）

If you need a custom SVG icon (not available in Material Icons) you should use the `SvgIcon` wrapper. The `SvgIcon` component takes the SVG `path` element as its child and converts it to a React component that displays this SVG icon, and allows the icon to be styled and respond to mouse events. SVG elements should be scaled for a 24x24px viewport.

The resulting icon can be used as is, or included as a child for other Material-UI components that use icons. 默认情况下，一个图标会继承使用当前的文本颜色。 您也可以选择使用以下任何一个主题颜色属性来设置图标的颜色：`primary`，`secondary`，`action`，`error` 以及 `disabled`。

{{"demo": "pages/components/icons/SvgIcons.js"}}

### Libraries

#### Material Design (recommended)

Material Design has standardized over [1,000 official icons](#material-icons).

#### MDI

[materialdesignicons.com](https://materialdesignicons.com/) provides over 2,000 icons. For the wanted icon, copy the SVG `path` they provide, and use it as the child of the `SvgIcon` component.

Note: [mdi-material-ui](https://github.com/TeamWertarbyte/mdi-material-ui) has already wrapped each of these SVG icons with the `SvgIcon` component, so you don't have to do it yourself.

## Icon (Font icons)

对于支持连字的任何图标字体，`Icon` 组件能够将其显示为一个图标。 作为先决条件，您必须在项目中包括一个 [Material icon font](https://google.github.io/material-design-icons/#icon-font-for-the-web)，举例来说，您可以由 Google Web Fonts 引入：

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />
```

`Icon` will set the correct class name for the Material icon font. For other fonts, you must supply the class name using the Icon component's `className` property.

若想要使用图标，您只需把图标名（字体连字）和 `Icon` 组件包装到一起，例如：

```jsx
import Icon from '@material-ui/core/Icon';

<Icon>star</Icon>
```

默认情况下，一个图标会继承使用当前的文本颜色。 您也可以选择使用以下任何一个主题颜色属性来设置图标的颜色：`primary`，`secondary`，`action`，`error` 以及 `disabled`。

### Font Material 图标

{{"demo": "pages/components/icons/Icons.js"}}

### Font Awesome

如下是一个同时使用[Font Awesome](https://fontawesome.com/icons) 与 `Icon` 的示例：

{{"demo": "pages/components/icons/FontAwesome.js", "hideEditButton": true}}

## Font vs SVG. Which approach to use?

这两种方法都能管用，然而，它们之间还是有着一些微妙的差异，特别当涉及到整体性能和渲染质量。 我们推荐尽可能选择 SVG，因为它允许代码分割、支持更多图标、而且渲染得更快、更好。

若您想了解更多细节，请查看 [ 为什么 GitHub 从字体图标迁移到 SVG 图标](https://github.blog/2016-02-22-delivering-octicons-with-svg/)这篇文章。

## 可访问性

图标可以传达各种各样有意义的信息，所以将他们传递给尽可能多的受众是至关重要的。 There are two use cases you’ll want to consider:
- **Decorative Icons** are only being used for visual or branding reinforcement. If they were removed from the page, users would still understand and be able to use your page.
- **Semantic Icons** are ones that you’re using to convey meaning, rather than just pure decoration. This includes icons without text next to them used as interactive controls — buttons, form elements, toggles, etc.

### 装饰 SVG 图标

If your icons are purely decorative, you’re already done! The `aria-hidden=true` attribute is added so that your icons are properly accessible (invisible).

### 语义 SVG 图标

如果您的图标带有语义，您只需要包含 `titleAccess =“含义”` 属性。 The `role="img"` attribute and the `<title>` element are added so that your icons are properly accessible.

对于那些可聚焦的交互式元素，譬如与一个图标按钮一起使用时，您可以使用 `aria-label` 属性：

```jsx
import IconButton from '@material-ui/core/IconButton';
import SvgIcon from '@material-ui/core/SvgIcon';

// ...

<IconButton aria-label="delete">
  <SvgIcon>
    <path d="M20 12l-1.41-1.41L13 16.17V4h-2v12.17l-5.58-5.59L4 12l8 8 8-8z" />
  </SvgIcon>
</IconButton>
```

### 装饰形的字体图标

If your icons are purely decorative, you’re already done! The `aria-hidden=true` attribute is added so that your icons are properly accessible (invisible).

### 语义字体图标

如果您的图标具有语义含义，您则需要提供一个对协助的技术可见的文本替代方法。

```jsx
import Icon from '@material-ui/core/Icon';
import Typography from '@material-ui/core/Typography';

// ...

<Icon>add_circle</Icon>
<Typography variant="srOnly">创建一个用户</Typography>
```

### 参考

- https://developer.paciellogroup.com/blog/2013/12/using-aria-enhance-svg-accessibility/
