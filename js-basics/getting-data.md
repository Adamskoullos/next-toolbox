## Getting Data

Next allows us to use a mix of build time rendering, runtime server-side rendering and client-side data rendering.

On pages that use data that does not change we can get this data at build time and render a static page with the data ready to be served. This is the fastest way to fully load a page to the user.

For pages that use changing data we can either fetch the data at run time on the server and add to the html before the page is served or serve the html and then fetch the data on the client. The most effective approach here is to quickly serve the pre-rendered html and show loaders while fetching the data on the client.

s

## getStaticProps

The `getStaticProps` is a method that can be exported from within specific `page` components in order to get the data required for that page. This function is run at build time and is only available on the server.

This pre-fetches the data before build time rendering, allowing static files to be served with the required Data.

```js

function SomePage(props){
    return <h1>{props.title}</h1>
}

export async function getStaticProps(){
    // Get data from API
    return: {
        props: {
            title: data.title
        }
    }
}

export default SomePage;
```
