## Config

`next.config.js` core structure when using `phases` to manage settings depending on the environment:

```js
const {
  PHASE_DEVELOPMENT_SERVER,
  PHASE_PRODUCTION_BUILD,
} = require("next/constants");

module.exports = (phase) => {
  const isDev = phase === PHASE_DEVELOPMENT_SERVER;
  const isStaging =
    phase === PHASE_PRODUCTION_BUILD && process.env.STAGING === "1";
  const isProd =
    phase === PHASE_PRODUCTION_BUILD && process.env.STAGING !== "1";

  const env = {
    customKey: (() => {
      if (isDev) return "My dev value";
      if (isStaging) return "My staging value";
      if (isProd) return "My prod value";
    })(),
  };

  return {
    env,
  };
};
```

### Environment Variables:

A dynamic environment pattern is above and the standard pattern below:

```js
env: {
    customKey: 'my-value',
  },
```

Within components:

```js
<h1>The value of customKey is: {process.env.customKey}</h1>
```

### Redirects

```js
const redirects = () => {
  return [
    {
      source: "/home",
      destination: "/",
      permanent: true,
    },
  ];
};
```

### Custom Headers

We can set custom `response` headers for specific paths:

```js
const headers = () => {
  return [
    {
      source: "/",
      headers: [
        {
          key: "x-custom-header-1",
          value: "my custom header 1",
        },
      ],
    },
  ];
};
```

### Asset Prefix

We can set base domains for assets:

```js
const assetPrefix = isProd ? "https://cdn.mydomain.com" : "";
```
