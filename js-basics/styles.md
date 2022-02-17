## Styles

As well as using utility classes from a component library, we can also add those extra bits of styling with either `styled jsx` or `css/sass modules`:

Styled JSX:

Directly within the component, inside the root element.

```js
<style jsx>{`
  h1 {
    color: ${color};
  }
`}</style>
```

CSS Modules:

**Note**: to use SCSS instead we just need to add SASS: `npm install sass`

```
/components
  /News
    index.jsx
    News.module.css
```

`/news`:

```js
import styles from "./News.modules.css";

// within component

<section className={styles.container}></section>;
```
