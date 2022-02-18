## Working with API routes

Instead of using Express as a back-end we can think about working with data from more of a Lambda perspective.

The example below uses Mongo from `npm install mongodb`

```
/api
    new-article.js
```

The above folder structure gives us the endpoint: `/api/new-article`

Code in `new-article.js` runs on the server only and can act similar to a traditional controller.

The below example omits error handling for simplicity:

```js
import { MongoClient } from 'mongodb';

async function handler(req, res){
    if(req.method === 'POST){
        const data = req.body;

        // connect to Mongo
        const client = await MongoClient.connect('connection string from Mongo');
        const db = client.db();

        const articlesCollection = db.collection('articles');

        const result = await articlesCollection.insertOne(data);

        client.close();

        res.status(201).json({message: 'article added successfully'});
    }
}

export default handler;

```

## Hitting the API from the app

> We can use `fetch` or `axios` when working with api routes as normal

```js
const createArticle = async (article) => {
  try {
    const response = await fetch("/api/new-article", {
      method: "POST",
      body: JSON.stringify(article),
      headers: { "Content-Type": "application/json" },
    });
    const result = await response.json();

    return result;
  } catch (err) {}
};
```
