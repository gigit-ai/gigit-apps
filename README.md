# Gigit Apps

Gigit Apps is a collection of React components designed to enhance your e-commerce store experience. The package includes **QAWidget**, **Highlights**, and **SmartMenu** components, each requiring minimal configuration to integrate seamlessly with your store.

## Installation

### NPM

To install the package with authentication:

```sh
npm install @gigit-ai/gigit-apps --//registry.npmjs.org/:_authToken=YOUR_ACCESS_TOKEN ----legacy-peer-deps
```

To avoid specifying the access token in every command, set it globally:

```sh
npm config set '//registry.npmjs.org/:_authToken' "YOUR_ACCESS_TOKEN"
npm install @gigit-ai/gigit-apps --legacy-peer-deps
```

To update the package to the latest compatible version:

```sh
npm install @gigit-ai/gigit-apps --legacy-peer-deps
```

To install the latest available version, including major updates:

```sh
npm install @gigit-ai/gigit-apps@latest --legacy-peer-deps
```

### YARN

To install the package with authentication:

```bash
yarn add @gigit-ai/gigit-apps --//registry.npmjs.org/:_authToken=YOUR_ACCESS_TOKEN
```

To avoid specifying the access token in every command, set it globally for `npm` (`yarn` will use the same config):

```bash
npm config set "//registry.npmjs.org/:_authToken" "YOUR_ACCESS_TOKEN"
yarn add @gigit-ai/gigit-apps
```

To update the package to the latest compatible version:

```bash
yarn add @gigit-ai/gigit-apps
```

To install the latest available version, including major updates:

```bash
yarn add @gigit-ai/gigit-apps@latest
```

### CI/CD

For using an NPM access token in a CI/CD workflow, refer to the official documentation:
[Using private packages in a CI/CD workflow](https://docs.npmjs.com/using-private-packages-in-a-ci-cd-workflow).

## Components

### 1. QAWidget

A widget that enables chat with AI to answer common questions on your store.

#### Usage

```jsx
import { QAWidget } from '@gigit-ai/gigit-apps'

const MyComponent = () => (
    <QAWidget shop="my-shop.com" productTitle="My Product" />
)
```

##### For NextJS Pages Router, you may need to dynamically import the components.

```jsx
import dynamic from 'next/dynamic'
const QAWidget = dynamic(
    () => import('@gigit-ai/gigit-apps').then((module) => module.QAWidget),
    {
        ssr: false,
    }
)
```

#### Props

| Prop         | Type   | Required | Description                                                                        |
| ------------ | ------ | -------- | ---------------------------------------------------------------------------------- |
| shop         | string | ✅       | The domain of your store URL (e.g., `my-shop.com`).                                |
| productTitle | string | Optional | The name of the product. Required if used on a product page.                       |
| productId    | string | Optional | The id of the product. Required if used on a product page.                         |
| test         | bool   | Optional | If set to `true`, interactions with this widget will not be included in analytics. |

### 2. Highlights

A component that showcases key product features relevant to users browsing the page. This should be used on a product page.

#### Usage

```jsx
import { Highlights } from '@gigit-ai/gigit-apps'

const MyComponent = () => (
    <Highlights shop="my-shop.com" productTitle="My Product" />
)
```

#### Props

| Prop         | Type   | Required | Description                                                                        |
| ------------ | ------ | -------- | ---------------------------------------------------------------------------------- |
| shop         | string | ✅       | The domain of your store URL (e.g., `my-shop.com`).                                |
| productTitle | string | ✅       | The name of the product.                                                           |
| test         | bool   | Optional | If set to `true`, interactions with this widget will not be included in analytics. |

### 3. SmartMenu

A navigation menu that improves user experience.

#### Usage

```jsx
import { SmartMenu } from '@gigit-ai/gigit-apps'

const MyComponent = () => <SmartMenu shop="my-shop.com" />
```

#### Props

| Prop | Type   | Required | Description                                                                        |
| ---- | ------ | -------- | ---------------------------------------------------------------------------------- |
| shop | string | ✅       | The domain of your store URL (e.g., `my-shop.com`).                                |
| test | bool   | Optional | If set to `true`, interactions with this widget will not be included in analytics. |

## License

This is a private library. Unauthorized distribution or modification is prohibited.

## Support

For issues or feature requests, please email us at info@gigit.ai.
