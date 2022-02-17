## Pages Routing Structure

Setting up the router via folders and files within `pages`. `[ ]` symbolizes a dynamic path and can be used on both folders and files:

```
/pages
    index.jsx
    /news
        index.jsx
        [id].jsx
    /[coin]
        index.jsx
        chart.jsx
```

Accessing dynamic route params within components > `/news/[id]`:

```js
import { useRouter } from "next/router";

// Within the component

const router = useRouter();
const articleId = router.query.id;
```

Dynamic routing using `Link` > `/[coin]/chart.jsx`:

```js
import Link from 'next/link'

// Within the component

<Link href=`/${token.symbol}/chart` >
    {token.symbol}
</Link>

```

Using a URL object:

```js
import Link from "next/link";

// Within the component

<Link
  href={{
    pathname: "[coin]/chart",
    query: { coin: token.symbol },
  }}
>
  {token.symbol}
</Link>;
```

Programmatic routing:

```js
import { useRouter } from "next/router";

// within component
const router = useRouter();

function handleRoute() {
  router.push(`/news/${article.id}`);
}
```
