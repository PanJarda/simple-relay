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
    comments: ['comment']
  }
};
```

bude se cachovat do indexeddb


```js
const APICache = {
  'author-1234': {
    name: 'Jarda'
  },
  'comment-1234': {
    title: 'Ahoj',
    author: 1234
  },
  'article-1345': {
    comments: [1234, 435435, 6456464]
  }
}
```

```js
const CacheStrategy = {
  article: 'embed',
  comment: 'cascade'
}
```

comments 43543 and 6456464 not found in cache
then
get /api/comment/?id=43535,6456464
-> save to cache
Relay.get('article', 1234)

```js
Relay.updateCache();
// specialni endpoint
Relay.get('update', {
  article: {
    1234: 12312313123,
    1231:12312312123
  }
})
```
