# SimpleRelay proposal


```js
const APISchema = {
  author: {
    id: 'string',
    name: 'string'
  },
  comment: {
    id: 'number',
    title: 'string',
    author: 'author'
  },
  article: {
    id: 'number',
    title: 'string',
    comments: ['comment']
  }
};
```

Relay will create some cache with structure like this:


```js
const APICache = {
  'author-1234': {
    name: 'PanJarda'
  },
  'comment-1234': {
    title: 'Hello',
    author: 1234
  },
  'article-1345': {
    title: 'Hello',
    comments: [1234, 435435, 6456464]
  }
}
```

Cache will be saved in indexedDB for persistence.

There will be caching strategies and fetching strategies

```js
const fetchingStrateg = {
  article: 'embed', // will embed all subresources
  comment: 'cascade' // will wait for ids of subresources and Then
  // look to cache and fetch only missing resources
};

const cachingStrategy = {
  article: 'indexedDB', // save to indexedDB
  comment: 'memory' // save to in memory cache object
}
```

And syncing cache state with server on regular basis.

```js
Relay.get('update', {
  article: {
    // <id>: <timestamp or revision number>
    1234: 12312313123,
    1231:12312312123
  }
})
```

Then api will answer with newly update objects:

```js
// api response:
{
  article: [
    {
      id: 1234,
      title: 'Hello there',
      author: 2131421
    }
  ]
}
```
