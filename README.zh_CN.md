# vite-plugin-imagemin-lts

**中文** | [English](./README.md)

一个压缩图片资产的 vite 插件，Forked 自[vite-plugin-imagemin](https://github.com/vbenjs/vite-plugin-imagemin)，原作者已经弃坑了，只能独立发包。

## 安装 (yarn or npm)

**node version:** >=12.0.0

**vite version:** >=2.0.0

```
yarn add vite-plugin-imagemin-lts -D
```

or

```
npm i vite-plugin-imagemin-lts -D
```

### 中国安装注意

由于 imagemin 在中国不好安装。现提供几个解决方案

1. 使用 yarn 在 package.json 内配置(推荐)

```json
"resolutions": {
    "bin-wrapper": "npm:bin-wrapper-china"
  },

```

2. 使用 npm,在电脑 host 文件加上如下配置即可

```bash

199.232.4.133 raw.githubusercontent.com
```

3. 使用 cnpm 安装(不推荐)

## 使用

- vite.config.ts 中的配置插件

```ts
import viteImagemin from 'vite-plugin-imagemin-lts'

export default () => {
  return {
    plugins: [
      viteImagemin({
        gifsicle: {
          optimizationLevel: 7,
          interlaced: false,
        },
        optipng: {
          optimizationLevel: 7,
        },
        mozjpeg: {
          quality: 20,
        },
        pngquant: {
          quality: [0.8, 0.9],
          speed: 4,
        },
        svgo: {
          plugins: [
            {
              name: 'removeViewBox',
            },
            {
              name: 'removeEmptyAttrs',
              active: false,
            },
          ],
        },
      }),
    ],
  }
}
```

### 配置说明

| 参数     | 类型                                  | 默认值  | 说明                                                        |
| -------- | ------------------------------------- | ------- | ----------------------------------------------------------- |
| verbose  | `boolean`                             | `true`  | 是否在控制台输出压缩结果                                    |
| filter   | `RegExp or (file: string) => boolean` | -       | 指定哪些资源不压缩                                          |
| disable  | `boolean`                             | `false` | 是否禁用                                                    |
| skipLargerFile  | `boolean`                             | `false` | 是否跳过让文件变大的处理（同时维持原文件）   |
| svgo     | `object` or `false`                   | -       | 见 [Options](https://github.com/svg/svgo/#what-it-can-do)   |
| gifsicle | `object` or `false`                   | -       | 见 [Options](https://github.com/imagemin/imagemin-gifsicle) |
| mozjpeg  | `object` or `false`                   | -       | 见 [Options](https://github.com/imagemin/imagemin-mozjpeg)  |
| optipng  | `object` or `false`                   | -       | 见 [Options](https://github.com/imagemin/imagemin-optipng)  |
| pngquant | `object` or `false`                   | -       | 见 [Options](https://github.com/imagemin/imagemin-pngquant) |
| webp     | `object` or `false`                   | -       | 见 [Options](https://github.com/imagemin/imagemin-webp)     |

## 维护

### 安装

```
cd packages/core && yarn install
```

### 构建

在 `packages/core` 下执行 `yarn build`

