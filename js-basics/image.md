## Image

The Next `Image` feature automatically does the following:

1. Compresses image size
2. Lazy loads images
3. Resizes the image for each device screen size

For images with url based src (on the cloud) we ned to add the domain to the images whitelist within `next.config.js`:

```js
module.exports = {
  images: {
    domains: ["image-source-domain.com"],
  },
};
```

```js
import Image from "next/image";

// component code
<Image src="" width={1080} height={720} />;
```

The `Image` element needs one of the below:

- `width & Height`
  or
- `Layout`:
  - `responsive` > Scales up and down > parent needs to have `display: block`
  - `fill` > Fits to parent element, can use prop: `objectFit` > Parent needs to have `position: relative`
  - `intrinsic` > scales down but not up
  - `fixed`
