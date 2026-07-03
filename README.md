# Fuck Claude - Are You a Claude "China User"?

English | [中文](#中文)

A lightweight, bilingual Astro joke site that scans browser-visible locale signals
and gives a 0-100 "China user" score. Everything runs locally in the browser.

Built with **Claude Fable 5**.

This fork credits the original idea and source at
[LinXiaoTao/FuckClaude](https://github.com/LinXiaoTao/FuckClaude), removes the
sponsor ads, and deploys on **Cloudflare Pages** instead of Vercel so users in
China can open it more smoothly.

This site is purely for entertainment. It is not an official Claude or Anthropic
result, not advice, and not a real detection verdict.

## How It Works

The page checks six browser-visible signals:

| Signal | Weight | How it is detected |
| --- | --- | --- |
| System timezone | 30 | `Intl.DateTimeFormat().resolvedOptions().timeZone` vs. China timezones |
| Browser language | 24 | `navigator.language(s)`; `zh-CN` / `zh-Hans` scores highest |
| Installed Chinese fonts | 20 | Canvas width-probing for SC/TC fonts |
| Intl locale | 10 | Browser date/number locale |
| Timezone offset | 8 | `getTimezoneOffset() === -480` |
| Emoji rendering style | 8 | OS-vendor guess from platform/UA |

The score is an estimate for the gag UI only. Low is `0-30`, Medium is `31-60`,
and High is `61-100`.

## Tech Stack

- [Astro](https://astro.build) `7.x`, static output
- Built-in i18n: English at `/`, Chinese at `/zh/`
- No UI framework; scan/scoring logic lives in `src/scripts/detect.ts`
- Fun voice feedback: one Fish Audio generated MP3 for low risk, browser speech
  synthesis fallback for other bands
- Deployed to Cloudflare Pages at `https://fuck-claude.01mvp.com`

## Develop

```bash
pnpm install
pnpm dev
pnpm build
pnpm preview
```

## Deploy

```bash
pnpm build
npx wrangler pages deploy dist --project-name fuck-claude --branch master
```

The production domain is configured in `astro.config.mjs` and `public/robots.txt`.

---

<a id="中文"></a>

# Fuck Claude - 你是「Claude 中国用户」吗

[English](#fuck-claude---are-you-a-claude-china-user) | 中文

一个轻量、中英双语的 Astro 整活网站，会扫描浏览器可见的区域/语言/字体信号，然后给出
0-100 的「Claude 中国用户」分数。所有检测都在浏览器本地完成。

本网站使用 **Claude Fable 5** 开发。

这个 fork 保留并鸣谢原始创意：
[LinXiaoTao/FuckClaude](https://github.com/LinXiaoTao/FuckClaude)。当前版本移除了
赞助广告，并部署在 **Cloudflare Pages**，不使用 Vercel，主要是为了让国内用户访问更顺。

本站纯属娱乐，不代表 Claude 或 Anthropic 的真实检测结果，不构成任何建议，也不代表真实
封号/风控判断。

## 检测内容

| 信号 | 权重 | 检测方式 |
| --- | --- | --- |
| 系统时区 | 30 | `Intl.DateTimeFormat().resolvedOptions().timeZone` 对比中国时区 |
| 浏览器语言 | 24 | `navigator.language(s)`；`zh-CN` / `zh-Hans` 得分最高 |
| 已安装中文字体 | 20 | canvas 宽度探测简/繁中文字体 |
| Intl 区域设置 | 10 | 浏览器日期/数字 locale |
| 时区偏移 | 8 | `getTimezoneOffset() === -480` |
| Emoji 渲染风格 | 8 | 根据 platform/UA 粗略推断系统 |

分数只是整活 UI 的估计值：低风险 `0-30`，中风险 `31-60`，高风险 `61-100`。

## 技术栈

- [Astro](https://astro.build) `7.x`，静态输出
- 内置 i18n：英文 `/`，中文 `/zh/`
- 不依赖 UI 框架；扫描和打分逻辑在 `src/scripts/detect.ts`
- 趣味语音反馈：低风险使用 Fish Audio 生成的 MP3，其他分档使用浏览器语音合成兜底
- 部署到 Cloudflare Pages：`https://fuck-claude.01mvp.com`

## 本地开发

```bash
pnpm install
pnpm dev
pnpm build
pnpm preview
```

## 部署

```bash
pnpm build
npx wrangler pages deploy dist --project-name fuck-claude --branch master
```

生产域名配置在 `astro.config.mjs` 和 `public/robots.txt`。
