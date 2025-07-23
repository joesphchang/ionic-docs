---
title: 'Ionic JavaScript Overview'
sidebar_label: Overview
---

<head>
  <title>Ionic JavaScript Overview | JavaScript Version Support and Tooling</title>
  <meta
    name="description"
    content="@ionic/javascript combines the Ionic experience with the tooling and APIs tailored to React developers. Learn more about version support and resources in our React Overview."
  />
</head>

import DocsCard from '@components/global/DocsCard';
import DocsCards from '@components/global/DocsCards';

`@ionic/javascript` offers a powerful way to build cross-platform applications using JavaScript, and it integrates seamlessly with modern tooling like Vite. This combination allows you to leverage your existing JavaScript knowledge and the efficiency of Vite to create high-quality, performant apps with Ionic's extensive UI library and native capabilities.

## JavaScript Version Support

Ionic JavaScript, when used with Vite, supports the latest versions of JavaScript, ensuring you can use modern language features in your projects.

## JavaScript Tooling

Ionic JavaScript is designed to work hand-in-hand with the JavaScript CLI and popular tooling. When you choose Vite as your build tool, you gain access to its incredibly fast development server and optimized build process. You can continue to use your favorite JavaScript libraries for state management, testing, and more within this ecosystem.

## Native Tooling

[Capacitor](https://capacitorjs.com) is the official cross-platform runtime for Ionic JavaScript, enabling your apps to run natively on iOS, Android, and the web with a single codebase.

## Installation

```shell-session
$ npm create vite@latest myApp -- --template vanilla
$ npm install && npm install @ionic/core
$ npm run dev
```

## Resources

<DocsCards>

<DocsCard header="Getting Started" href="quickstart" icon="/icons/guide-quickstart-icon.png">
  <p>Quickly set up your first Ionic React app and learn the basics of the framework and CLI.</p>
</DocsCard>

<DocsCard header="Build Your First App" href="your-first-app" icon="/icons/logo-react-icon.png">
  <p>Build a real Photo Gallery app with Ionic React and native device features.</p>
</DocsCard>

<DocsCard header="Navigation" href="navigation" icon="/icons/component-navigation-icon.png">
  <p>Master navigation in Ionic React using React Router.</p>
</DocsCard>

<DocsCard header="Components" href="/docs/components" icon="/icons/guide-components-icon.png">
  <p>Explore Ionic’s rich library of UI components for building beautiful apps.</p>
</DocsCard>

</DocsCards>