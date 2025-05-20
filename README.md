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

### 1A. QAWidget

A widget that enables chat with AI to answer common questions on your store.

#### Usage

```jsx
import { QAWidget } from '@gigit-ai/gigit-apps'

const MyComponent = () => (
    <QAWidget shop="my-shop.com" productTitle="My Product" />
)
```

For NextJS and SSR, you may need to dynamically import the component:

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

| Prop                | Type   | Required | Description                                                                        |
| ------------------- | ------ | -------- | ---------------------------------------------------------------------------------- |
| shop                | string | ✅       | The domain of your store URL (e.g., `my-shop.com`).                                |
| productTitle        | string | Optional | The name of the product. Required if used on a product page.                       |
| productId           | string | Optional | The id of the product. Required if used on a product page.                         |
| productSpecificChat | bool   | Optional | If set to `true`, each product will have its own chat channel.                     |
| test                | bool   | Optional | If set to `true`, interactions with this widget will not be included in analytics. |

### 1B. QAWidgetEntrypoint

A CTA that will scroll to the QA Widget when clicked.

#### Usage

```jsx
import { QAWidgetEntrypoint } from '@gigit-ai/gigit-apps'

const MyComponent = () => (
    <QAWidgetEntrypoint shop="my-shop.com" productTitle="My Product" />
)
```

For NextJS and SSR, you may need to dynamically import the component:

```jsx
import dynamic from 'next/dynamic'
const QAWidgetEntrypoint = dynamic(
    () =>
        import('@gigit-ai/gigit-apps').then(
            (module) => module.QAWidgetEntrypoint
        ),
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

For NextJS and SSR, you may need to dynamically import the component:

```jsx
import dynamic from 'next/dynamic'
const Highlights = dynamic(
    () => import('@gigit-ai/gigit-apps').then((module) => module.Highlights),
    {
        ssr: false,
    }
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

For NextJS and SSR, you may need to dynamically import the component:

```jsx
import dynamic from 'next/dynamic'
const SmartMenu = dynamic(
    () => import('@gigit-ai/gigit-apps').then((module) => module.SmartMenu),
    {
        ssr: false,
    }
)
```

#### Props

| Prop | Type   | Required | Description                                                                        |
| ---- | ------ | -------- | ---------------------------------------------------------------------------------- |
| shop | string | ✅       | The domain of your store URL (e.g., `my-shop.com`).                                |
| test | bool   | Optional | If set to `true`, interactions with this widget will not be included in analytics. |

## **Tracking Events in React & Next.js**

The `trackEvent` function from `@gigit-ai/gigit-apps` enables event tracking. This guide explains **where and how to call `trackEvent`**, covering both **React.js** and **Next.js (Pages Router & App Router)**.

---

### **1. Tracking Page Views**

#### **For React.js (Using React Router)**

If you're using **React.js with React Router**, place `trackEvent` inside a separate `PageViewTracker` component and use `useLocation()` to detect route changes.

##### **Step 1: Create a Page View Tracker Component**

```tsx
import { useEffect } from 'react'
import { useLocation } from 'react-router-dom'
import { trackEvent } from '@gigit-ai/gigit-apps'

export default function PageViewTracker() {
    const location = useLocation()

    useEffect(() => {
        trackEvent('PAGE_VIEWED', { url: location.pathname })
    }, [location])

    return null
}
```

##### **Step 2: Add It to Your Main App Component**

```tsx
import { BrowserRouter, Route, Routes } from 'react-router-dom'
import PageViewTracker from './PageViewTracker'
import HomePage from './HomePage'
import ProductPage from './ProductPage'

export default function App() {
    return (
        <BrowserRouter>
            <PageViewTracker />
            <Routes>
                <Route path="/" element={<HomePage />} />
                <Route path="/product/:id" element={<ProductPage />} />
            </Routes>
        </BrowserRouter>
    )
}
```

---

#### **For Next.js**

##### **Using Pages Router (`pages/` directory)**

In Next.js (Pages Router), track navigation changes using `useRouter` inside `_app.tsx`:

```tsx
import { useEffect } from 'react'
import { useRouter } from 'next/router'
import { trackEvent } from '@gigit-ai/gigit-apps'

export default function App({ Component, pageProps }) {
    const router = useRouter()

    useEffect(() => {
        const handleRouteChange = () => {
            trackEvent('PAGE_VIEWED')
        }

        router.events.on('routeChangeComplete', handleRouteChange)
        return () => {
            router.events.off('routeChangeComplete', handleRouteChange)
        }
    }, [router])

    return <Component {...pageProps} />
}
```

---

##### **Using App Router (`app/` directory)**

For the **Next.js App Router**, follow the **official Next.js guide** by composing `usePathname` and `useSearchParams`.

**Step 1: Create a `NavigationEvents` Component**

```tsx
'use client'

import { useEffect } from 'react'
import { usePathname, useSearchParams } from 'next/navigation'

export function NavigationEvents() {
    const pathname = usePathname()
    const searchParams = useSearchParams()

    useEffect(() => {
        const track = async () => {
            const { trackEvent } = await import('@gigit-ai/gigit-apps')
            trackEvent('PAGE_VIEWED')
        }
        track()
    }, [pathname, searchParams])

    return null
}
```

**Step 2: Include It in `layout.tsx`**

```tsx
import { Suspense } from 'react'
import { NavigationEvents } from './components/NavigationEvents'

export default function RootLayout({ children }) {
    return (
        <html lang="en">
            <body>
                {children}

                <Suspense fallback={null}>
                    <NavigationEvents />
                </Suspense>
            </body>
        </html>
    )
}
```

### **2. Tracking Add to Cart Events**

#### **Option 1: Button Click (For JavaScript-Based Cart Handling)**

```tsx
'use client'

export default function AddToCartButton() {
    const handleAddToCart = async () => {
        const { trackEvent } = await import('@gigit-ai/gigit-apps')

        trackEvent('ADD_TO_CART', {
            productId: '123456789',
            productTitle: 'Example Product',
            quantity: 2,
            totalPrice: 39.98,
            currency: 'USD',
        })
    }

    return <button onClick={handleAddToCart}>Add to Cart</button>
}
```

---

#### **Option 2: Tracking Form Submission (For Form-Based Carts)**

If your cart system **relies on form submissions**, attach `trackEvent` to `onSubmit`:

```tsx
'use client'

export default function AddToCartForm() {
    const handleSubmit = async (event: React.FormEvent<HTMLFormElement>) => {
        event.preventDefault()

        const formData = new FormData(event.currentTarget)
        const quantity = Number(formData.get('quantity')) || 1
        const productId = formData.get('productId') as string
        const productTitle = formData.get('productTitle') as string
        const totalPrice = quantity * 19.99 // Example price calculation

        const { trackEvent } = await import('@gigit-ai/gigit-apps')
        trackEvent('ADD_TO_CART', {
            productId,
            productTitle,
            quantity,
            totalPrice,
            currency: 'USD',
        })

        event.currentTarget.submit()
    }

    return (
        <form onSubmit={handleSubmit}>
            <input type="hidden" name="productId" value="123456789" />
            <input type="hidden" name="productTitle" value="Example Product" />
            <input type="number" name="quantity" min="1" defaultValue="1" />
            <button type="submit">Add to Cart</button>
        </form>
    )
}
```

| **Prop**       | **Type** | **Required?** | **Description**                                           |
| -------------- | -------- | ------------- | --------------------------------------------------------- |
| `productId`    | `string` | ✅ Yes        | The unique identifier for the product (e.g., variant ID). |
| `productTitle` | `string` | ✅ Yes        | The name of the product.                                  |
| `quantity`     | `number` | ✅ Yes        | The number of items added to the cart.                    |
| `totalPrice`   | `number` | ✅ Yes        | The total cost of the items added (price × quantity).     |
| `currency`     | `string` | ✅ Yes        | The currency code (e.g., `"USD"`).                        |
| `custom`       | `any`    | Optional      | Any additional custom data to track with this event.      |

---

### **3. Tracking Checkout Completion**

Call `trackEvent` **after checkout is completed**, usually on the **order confirmation page**. Alternatively, instead of calling this function on the checkout success page, you can also call it when your checkout API returns a successful response.

```tsx
'use client'

import { useEffect } from 'react'

export default function CheckoutSuccessPage() {
  useEffect(() => {
    const sendTracking = async () => {
      const { trackEvent } = await import('@gigit-ai/gigit-apps')
      trackEvent('CHECKOUT_COMPLETED', {
        currencyCode: 'USD',
        totalPrice: 59.99,
        email: 'user@example.com',
        phone: '+1234567890',
        order: {
          id: 'order123',
          customerId: 'customer-12345',
        },
        lineItems: [
          {
            productId: 'abc1235',
            productTitle: 'Example Product',
            quantity: 2,
            price: 29.99,
          },
        ],
      })
    }

    sendTracking()
  }, [])

  return <h1>Thank you for your purchase!</h1>
}

}
```

| **Prop**                   | **Type** | **Required?** | **Description**                                      |
| -------------------------- | -------- | ------------- | ---------------------------------------------------- |
| `order.id`                 | `string` | ✅ Yes        | The id of the order                                  |
| `order.customerId`         | `string` | Optional      | The id of the customer                               |
| `currencyCode`             | `string` | ✅ Yes        | The currency used for the checkout (e.g., `"USD"`).  |
| `totalPrice`               | `number` | ✅ Yes        | The total amount for the checkout.                   |
| `lineItems`                | `array`  | ✅ Yes        | A list of items included in the checkout.            |
| `lineItems[].productId`    | `string` | ✅ Yes        | The product ID for each item in the order.           |
| `lineItems[].productTitle` | `string` | ✅ Yes        | The name of the product.                             |
| `lineItems[].quantity`     | `number` | ✅ Yes        | The quantity purchased.                              |
| `lineItems[].price`        | `number` | Optional      | The price of the product.                            |
| `email`                    | `string` | Optional      | The email of the user who completed the checkout.    |
| `phone`                    | `string` | Optional      | The phone number of the user.                        |
| `custom`                   | `any`    | Optional      | Any additional custom data to track with this event. |

## License

This is a private library. Unauthorized distribution or modification is prohibited.

## Support

For issues or feature requests, please email us at info@gigit.ai.
