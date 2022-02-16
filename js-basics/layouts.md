## Layouts

```
/components
    /layout
        Layout.jsx
        Layout.module.css
        TopNav.jsx
        TopNav.module.css
```

A layout component can be created including any structural components like nav, footer, header etc..
This layout component accepts a `children` props object:

`/components/layout/Layout.jsx`:

```jsx
import TopNav from './TopNav';
import classes from './Layout.module.css'

function Layout (props) {
    <>
        <TopNav />
        <main className={classes.main}>{props.children}</main>
    </TopNav>
}

export default Layout;
```

To nest each page within the layout component we can either add the `Layout` to each page or add the Layout to the root of the application within `_app.js`:

```js
import Layout from "../components/layout/Layout";
import "../styles/globals.css";

function MyApp({ Component, pageProps }) {
  return (
    <Layout>
      <Component {...pageProps} />
    </Layout>
  );
}

export default MyApp;
```
