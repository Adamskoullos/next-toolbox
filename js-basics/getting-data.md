## Getting Data

Next allows us to use a mix of build time rendering, runtime server-side rendering and client-side data rendering.

On pages that use data that does not change we can get this data at build time and render a static page with the data ready to be served. This is the fastest way to fully load a page to the user.

For pages that use changing data we can either fetch the data at run time on the server and add to the html before the page is served or serve the pre-built html and then fetch the data on the client. The most effective approach here is to quickly serve the pre-rendered html and show loaders while fetching the data on the client.

- [getStaticProps](#getStaticProps)
- [getStaticPaths](#getStaticPaths)
- [getServerSideProps](#getServerSideProps)

---

## getStaticProps

**Use if data changes every minute, not if data changes every second**

The `getStaticProps` is a method that can be exported from within specific `page` components in order to get the data required for that page. This function is run at build time.

This pre-fetches the data at build time, rendering html and data so fully built pages are ready to be served.

`getStaticProps` is only run on the server and is not accessible on the client. This means we can run server-side code within the method.

**Note**:

`incremental static generation` can be added as an option by adding the `revalidate` prop and giving it a value in `seconds`. In the example below the page is rebuilt on the server every 60 seconds each time refetching the data. this allows static pages to be used in situations where changing data is used.

> The `context` gives us access to the params, ex: `context.params.id`

```js

function SomePage(props){
    return <h1>{props.article.title}</h1>
}

export async function getStaticProps(context){
  // The custom function includes any database logic and has the collection passed in
  // this would include making and closing a connection to Mongo and everything in between
    const data = await customGetDataFunction(collection);
    return: {
        props: {
            article: {
              title: data.title,
              id: data._id.toString()
            }
        }
        revalidate: 60
    }
}

export default SomePage;
```

Example when `data` is an array:

```js
  const data = await customGetDataFunction(collection);
  return: {
      props: {
          articles: data.map(article => ({
            title: article.title,
            id: article._id.toString()
          }))
      }
      revalidate: 60
  }

```

---

## getStaticPaths

`getStaticPaths` is used when dynamic pages are being statically built. First we need to get the query params for each dynamic path. Then create an array and return that array as the value of `paths`. The `fallback` prop allows us to tell Next to statically generate known pages but if need be, on the fly create dynamic pages at run time if the path does not exist in the paths array.

```js
export async function getStaticPaths(){
    const paramsArray = getPaths();

    return: {
        paths: paramsArray,
        fallback: true
    }
}
```

The paths array is structured like this:

```js
[
  {
    params: {
      someId: 1,
    },
  },
  {
    params: {
      someId: 2,
    },
  },
];
```

> So for dynamic pages we use both `getStaticPaths` and then `getStaticProps`

---

## getServerSideProps

This method is also used within specific page components and only runs on the server but at run time (every time a user goes to the page).

The request must be received and html and data rendered to the page before the page is served. This increases time-to-first-byte.

> However we get access to the `context` making the `req` and `res` objects available and this can be used for server-side authentication.

```js

function SomePage(props){
    return <h1>{props.title}</h1>
}

export async function getStaticProps(context){
    const data = await customGetDataFunction();
    return: {
        props: {
            title: data.title
        }
    }
}

export default SomePage;
```
