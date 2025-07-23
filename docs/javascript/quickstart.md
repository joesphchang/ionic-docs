---
title: Ionic JavaScript Quickstart
sidebar_label: Quickstart
---

<head>
  <title>Intro to Ionic React Quickstart Using Ionic CLI: React Basics</title>
  <meta
    name="description"
    content="Intro to React Quickstart covers the basics of React and Ionic, including any Ionic-specific features. Learn how to build React apps using the Ionic CLI."
  />
</head>

## What is Ionic Framework?

First off, if you're new here, welcome! Ionic is a free and open source component library for building apps that run on iOS, Android, Electron, and the Web. You write your app once using familiar technologies (HTML, CSS, JavaScript) and deploy to any platform.

Along with the UI components, Ionic also provides a command line tool for creating new apps, as well as deploying to the various platforms we support.

In this guide, we'll go over the basics of both JavaScript and Ionic, including any Ionic specific features. If you're familiar with React, enjoy the guide and learn something new about Ionic. If you're not familiar with either, no worries! This guide will cover the basics and provide enough information to get an app up and running.

# Creating a Project with Vite and Ionic

### Create a new Vite project using the vanilla template:
To begin, we'll leverage Vite to scaffold our project, then add Ionic.

```shell
npm create vite@latest myApp -- --template vanilla
```

This command creates a new directory named myApp with a basic Vite setup for a vanilla JavaScript project.

### Navigate into your new project directory and install dependencies:

```shell
cd myApp
npm install
```

### Install `@ionoic/core` and `ionicons`:

```shell
npm install @ionic/core && npm install ionicons
```

`@ionic/core` provides the core Ionic Web Components that are framework-agnostic and work perfectly with vanilla JavaScript.

### Start your development server: 

```shell
npm run dev
```

Your project should now be running in your browser, typically at http://localhost:5173.

## A look at a JavaScript Project

The heart of our app will be in the src directory. Vite's default setup uses main.js as the entry point. Let's open `src/main.js`. You'll typically see something like this:

```js
import './style.css'
import javascriptLogo from './javascript.svg'
import viteLogo from '/vite.svg'
import { setupCounter } from './counter.js'

document.querySelector('#app').innerHTML = `
  <div>
    <a href="https://vite.dev" target="_blank">
      <img src="${viteLogo}" class="logo" alt="Vite logo" />
    </a>
    <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript" target="_blank">
      <img src="${javascriptLogo}" class="logo vanilla" alt="JavaScript logo" />
    </a>
    <h1>Hello Vite!</h1>
    <div class="card">
      <button id="counter" type="button"></button>
    </div>
    <p class="read-the-docs">
      Click on the Vite logo to learn more
    </p>
  </div>
`

setupCounter(document.querySelector('#counter'))
```

To integrate Ionic, we'll need to import the core Ionic styles and potentially register Ionic components if your setup requires explicit registration (though often, simply importing the core library makes them globally available).

Let's modify `src/main.js` to include basic Ionic setup and a simple Ionic component.

```js
import './style.css';
import '@ionic/core/css/core.css';
import '@ionic/core/css/display.css';
import '@ionic/core/css/flex-utils.css';
import '@ionic/core/css/float-elements.css';
import '@ionic/core/css/normalize.css';
import '@ionic/core/css/padding.css';
import '@ionic/core/css/structure.css';
import '@ionic/core/css/typography.css';
import { defineCustomElements } from '@ionic/core/loader';

defineCustomElements(window);

document.querySelector('#app').innerHTML = `
  <ion-app>
    <ion-header>
      <ion-toolbar>
        <ion-title>My Ionic Vite App</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      Hello from Ionic and Vite!
      <ion-button>Click Me</ion-button>
    </ion-content>
  </ion-app>
`;
```

## Building a Component with Style and Interactivity

Now let's create a more involved "page" with some interactive elemnts. We'll simulate a simple to-do list item. 

First, let's create a new file `src/home.js` for our main content:

```js
export function createHomePage() {
  const page = document.createElement('ion-page');
  page.innerHTML = `
    <ion-header>
      <ion-toolbar>
        <ion-title>Ionic Tasks</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ion-list>
        <ion-item>
          <ion-checkbox label-placement="end" justify="start">
            <h1>Create Idea</h1>
            <ion-note>Run Idea by Brandy</ion-note>
          </ion-checkbox>
          <ion-badge color="success" slot="end">
            5 Days
          </ion-badge>
        </ion-item>
      </ion-list>

      <ion-fab vertical="bottom" horizontal="end" slot="fixed">
        <ion-fab-button id="new-item-button">
          <ion-icon name="add"></ion-icon>
        </ion-fab-button>
      </ion-fab>
    </ion-content>
  `;

  // Attach event listener for the FAB button
  page.addEventListener('ionRouterDidPresent', () => {
    const newItemButton = page.querySelector('#new-item-button');
    if (newItemButton) {
      newItemButton.addEventListener('click', () => {
        // This is where we'd handle navigation, e.g., to a new-item page
        console.log('FAB button clicked! Should navigate to a new item page.');
        // For now, we'll just log. We'll set up navigation properly later.
      });
    }
  });


  return page;
}
```

and update `src/main.js` to render this home page: 

```js
import './style.css';
import '@ionic/core/css/core.css';
import '@ionic/core/css/display.css';
import '@ionic/core/css/flex-utils.css';
import '@ionic/core/css/float-elements.css';
import '@ionic/core/css/normalize.css';
import '@ionic/core/css/padding.css';
import '@ionic/core/css/structure.css';
import '@ionic/core/css/typography.css';
import { defineCustomElements } from '@ionic/core/loader';
import { createHomePage } from './home';

defineCustomElements(window);

const appEl = document.querySelector('#app');
if (appEl) {
  const homePage = createHomePage();
  appEl.appendChild(homePage);
}
```

## Simple Navigation (Manual)

For a simple JavaScript app, you might manage navigation manually by showing and hiding pages or dynamically appending/removing them from the DOM. Let's a simulate this for a "New Item" page.

### Create `src/newItem.js`:

```js
export function createNewItemPage() {
	const page = document.createElement('ion-page');
	page.innerHTML = `
      <ion-header>
        <ion-toolbar>
          <ion-buttons slot="start">
            <ion-back-button default-href="/"></ion-back-button>
          </ion-buttons>
          <ion-title>New Item</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content class="ion-padding">
        <p>This is the new item page!</p>
        <ion-button expand="block" id="save-item-button">Save Item</ion-button>
      </ion-content>
    `;

	return page;
}

```

### Update `src/home.js` for updated routing logic:
```js
export function createHomePage() {
	const page = document.createElement('ion-page');
	page.innerHTML = `
      <ion-header>
        <ion-toolbar>
          <ion-title>Ionic Tasks</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content class="ion-padding">
        <ion-list>
          <ion-item>
            <ion-checkbox label-placement="end" justify="start">
              <h1>Create Idea</h1>
              <ion-note>Run Idea by Brandy</ion-note>
            </ion-checkbox>
            <ion-badge color="success" slot="end">
              5 Days
            </ion-badge>
          </ion-item>
        </ion-list>
      </ion-content>

      <ion-fab vertical="bottom" horizontal="end" slot="fixed">
        <ion-fab-button id="new-item-button">
          <ion-icon name="add"></ion-icon>
        </ion-fab-button>
      </ion-fab>
    `;
	return page;
}
```

### Update `src/main.js` for basic routing logic: 

We'll use a very simple apporach for navigation here for demonstration. For complex apps, consider a dedicated client-side router library.

```js
import './style.css';
import '@ionic/core/css/core.css';
import '@ionic/core/css/display.css';
import '@ionic/core/css/flex-utils.css';
import '@ionic/core/css/float-elements.css';
import '@ionic/core/css/normalize.css';
import '@ionic/core/css/padding.css';
import '@ionic/core/css/structure.css';
import '@ionic/core/css/typography.css';
import { defineCustomElements } from '@ionic/core/loader';
import { createHomePage } from './home';
import { createNewItemPage } from './newItem';

defineCustomElements(window);

if (window.Ionicons) {
	window.Ionicons.config({
		resourcesUrl: '/node_modules/ionicons/dist/ionicons/',
	});
}

const appEl = document.querySelector('#app');
const ionAppEl = document.createElement('ion-app');
appEl.appendChild(ionAppEl);

const ionRouterOutlet = document.createElement('ion-router-outlet');
ionAppEl.appendChild(ionRouterOutlet);

const pages = {
	'/': createHomePage(),
	'/new': createNewItemPage(),
};

function navigate(path) {
	while (ionRouterOutlet.firstChild) {
		ionRouterOutlet.removeChild(ionRouterOutlet.firstChild);
	}

	let currentPageElement;
	if (path === '/') {
		currentPageElement = pages['/'];
		const newItemButton = currentPageElement.querySelector('#new-item-button');
		if (newItemButton) {
			const oldClickListener = newItemButton.__listener;
			if (oldClickListener) {
				newItemButton.removeEventListener('click', oldClickListener);
			}
			const newClickListener = () => {
				history.pushState({}, '', '/new');
				navigate('/new');
			};
			newItemButton.addEventListener('click', newClickListener);
			newItemButton.__listener = newClickListener;
		}
	} else if (path === '/new') {
		currentPageElement = pages['/new'];
		const backButton = currentPageElement.querySelector('ion-back-button');
		if (backButton) {
			const oldBackListener = backButton.__listener;
			if (oldBackListener) {
				backButton.removeEventListener('click', oldBackListener);
			}
			const newBackListener = () => {
				history.back();
			};
			backButton.addEventListener('click', newBackListener);
			backButton.__listener = newBackListener;
		}
		const saveButton = currentPageElement.querySelector('#save-item-button');
		if (saveButton) {
			const oldSaveListener = saveButton.__listener;
			if (oldSaveListener) {
				saveButton.removeEventListener('click', oldSaveListener);
			}
			const newSaveListener = () => {
				console.log('Item saved!');
				history.back();
			};
			saveButton.addEventListener('click', newSaveListener);
			saveButton.__listener = newSaveListener;
		}
	} else {
		currentPageElement = pages['/'];
		console.warn(`Route not found: ${path}. Navigating to home.`);
	}

	if (currentPageElement) {
		ionRouterOutlet.appendChild(currentPageElement);
	}
}

window.addEventListener('popstate', () => {
	navigate(location.pathname);
});

navigate(location.pathname === '/new' ? '/new' : '/');
```

## Adding Icons

Ionic comes with [Ionicons](https://ionic.io/ionicons/) pre-installed. You can use them directly in your HTML with the `name` attribute on the `<ion-icon>` component. 

For example, to use the `camera` icon: 

```html
<ion-button>
  <ion-icon name="camera"></ion-icon>
  Take Picture
</ion-button>
```

You can also specify different icons based on the platform mode (`ios` or `md`): 

```html
<ion-button>
  <ion-icon ios="logo-apple" md="logo-android"></ion-icon>
</ion-button>
```


## Build a Native App with Capacitor 

The real power of Ionic lies in its ability to deploy to native platforms. We use Capacitor, Ionic's official cross-platform app runtime, to achieve this. Capacitor provides a consistent, web-focused set of APIs that let your app access rich native device features while staying as close to web standards as possible.

### Add Capacitor to your project: 

```shell
npm install @capacitor/core @capacitor/cli
npx capacitor init
```

### Install Capacitor iOS & Android: 

```shell
npm install @capacitor/ios
npm install @capacitor/android
```

Follow the prompts to set up your Capacitor project. 

### Build your web project:

```shell
npm run build
```

### Copy web assets to Capacitor and add your platform of choice: 

```shell
npx capacitor add ios
npx capacitor add android
```

### Open the native projects in their IDEs:

```shell
npx capacitor open ios
npx capacitor open android 
```

This will open Xcode for your iOS project and Android Studio for your Android project, allowing you to build, run, and debug your native app. 

## Using Native Device Features (Example: Camera API)

Capacitor makes it simple to access native device features. Let's integrate the Camera API into our `home.js` page. 

First, install the camera plugin:

```shell
npm install @capacitor/camera
npx capacitor sync
```

Now, modify `src/home.js` to incldue camera functionality: 

```js
import { Camera, CameraResultType } from '@capacitor/camera';
export function createHomePage() {
  const page = document.createElement('ion-page');
  page.innerHTML = `
    <ion-header>
      <ion-toolbar>
        <ion-title>Ionic Tasks</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ion-list>
        <ion-item>
          <ion-checkbox label-placement="end" justify="start">
            <h1>Create Idea</h1>
            <ion-note>Run Idea by Brandy</ion-note>
          </ion-checkbox>
          <ion-badge color="success" slot="end">
            5 Days
          </ion-badge>
        </ion-item>
      </ion-list>

      <img id="captured-image" style="width: 100%; display: none;" />
      <ion-button expand="block" id="take-photo-button">Take Photo</ion-button>

      <ion-fab vertical="bottom" horizontal="end" slot="fixed">
        <ion-fab-button id="new-item-button">
          <ion-icon name="add"></ion-icon>
        </ion-fab-button>
      </ion-fab>
    </ion-content>
  `;

  page.addEventListener('ionViewDidEnter', async () => {
    const newItemButton = page.querySelector('#new-item-button');
    if (newItemButton) {
      newItemButton.addEventListener('click', () => {
        const event = new CustomEvent('navigate', { detail: '/new' });
        document.dispatchEvent(event);
      });
    }

    const takePhotoButton = page.querySelector('#take-photo-button');
    const capturedImage = page.querySelector('#captured-image');

    if (takePhotoButton && capturedImage) {
      takePhotoButton.addEventListener('click', async () => {
        try {
          const image = await Camera.getPhoto({
            quality: 90,
            allowEditing: true,
            resultType: CameraResultType.Uri,
          });
          capturedImage.src = image.webPath;
          capturedImage.style.display = 'block'; 
        } catch (error) {
          console.error('Error taking photo:', error);
        }
      });
    }
  });

  return page;
}
```

> Note: For the navigation to work coorectly with event listeners attached within `createHomePage`, you'll need a global event system or a more robust routing mechanism in your `main.js`. For simplicity, the `take-photo-button` is demonstrated directly within this file. 

## Where to Go From Here
You've now got the basics of an Ionic JavaScript app powered by Vite and are ready to deploy natively with Capacitor.

- Dive Deeper into Components: Explore Ionic's comprehensive component [API pages](https://ionicframework.com/docs/components) to build stunning UIs.
- Capacitor APIs: Discover all the native functionalities available in the [Capacitor docs](https://capacitorjs.com/docs/apis), including file system access, geolocation, and more.
- Vite Documentation: For advanced build configurations and optimizations, check out the [Vite documentation](https://vite.dev/guide/).
- JavaScript Best Practices: Continue to refine your JavaScript skills for building robust and maintainable applications.

Happy app building! 🎉
