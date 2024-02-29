# 前端开发规范

> 本文档旨在提供使用Vue 3框架进行前端开发的设计规范，以确保代码的一致性、可维护性及高效性。



## 1. 项目结构规范

- **目录结构**：
  - `components/`：存放可复用的Vue组件。
  - `views/`：存放与路由对应的Vue页面组件。
  - `router/`：定义应用的路由配置。
  - `store/`：状态管理，使用Vuex。
  - `assets/`：存放静态资源，如样式、图片、字体等。
  - `utils/`：存放工具函数或服务。
  - `api/`：存放API请求相关的函数。
- **文件命名**：
  - 组件文件使用大驼峰命名（PascalCase），如`UserProfile.vue`。
  - 非组件的js文件、样式文件使用小写字母，单词间用连字符（kebab-case），如`user-api.js`、`global-styles.css`。



## 2. 组件设计规范

- **单文件组件**：每个Vue组件应该是一个单文件组件（.vue文件），包含`<template>`、`<script>`和`<style>`三部分。
- **组件命名**：组件名应该反映其功能或用途，尽量简洁明了。
- **Props定义**：使用`props`传递数据时，应该明确指定类型，必要时指定默认值或验证。
- **事件命名**：自定义事件名应使用kebab-case，如`@click="handleClick"`。



## 3. 样式规范

- **CSS预处理器**：推荐使用SCSS或LESS等CSS预处理器，增强样式编写的功能性和可维护性。
- **类名命名**：使用BEM（块(Block)、元素(Element)、修饰符(Modifier)）命名约定，以确保样式的模块化和可重用性。
- **样式作用域**：尽量使用组件的局部样式（`<style scoped>`），避免全局样式污染。



## 4. 路由和状态管理

- **路由配置**：使用Vue Router进行路由管理，路由配置应清晰定义，包括路径、组件和子路由等。
- **状态管理**：对于复杂应用，使用Vuex进行状态管理，合理划分模块，明确状态树结构。



## 5. 代码风格和质量

- **代码风格**：遵循[ESLint](https://eslint.org/)的Vue官方推荐规则，确保代码风格一致性。「不做强制性要求，但是请开发者尽量按照标准风格开发以提高协作开发效率」
- **组件大小**：保持组件大小适中，过大的组件应考虑拆分成更小的组件。
- **代码复用**：通过混入（mixins）、自定义指令（directives）等机制复用代码。



## 6. 性能优化

- **懒加载**：对于大型应用，采用路由级的懒加载，减少首屏加载时间。
- **异步组件**：使用异步组件分割代码，按需加载。
- **资源优化**：优化图片资源，使用现代图片格式（如WebP），减少应用的总体大小。



## 7. 示例代码

```vue
<template>
  <div class="user-profile">
    <h1>{{ userName }}</h1>
    <p>{{ userBio }}</p>
  </div>
</template>

<script>
export default {
  name: 'UserProfile',
  props: {
    userName: String,
    userBio: String,
  },
};
</script>

<style scoped>
.user-profile {
  /* 样式内容 */
}
</style>
```

