A [Metalsmith](http://www.metalsmith.io/) plugin for generating a [JSON Feed](https://jsonfeed.org/) from a [collection](https://github.com/segmentio/metalsmith-collections).

Heavily inspired by [metalsmith-feed](https://github.com/hurrymaplelad/metalsmith-feed).

## Usage

### Basic

```es6
const Metalsmith = require('metalsmith')
const collections = require('metalsmith-collections')
const jsonfeed = require('metalsmith-feed')

Metalsmith('example')
  .use(collections({
    posts: '*.html'
  })
  .use(jsonfeed({
    collection: 'posts',
    title: 'Example feed'
  })
```

### Using metadata

If your site has `title`, `url` or `author` metadata, they will be used (you can override them by setting options, see below).

```es6
const Metalsmith = require('metalsmith')
const collections = require('metalsmith-collections')
const jsonfeed = require('metalsmith-feed')

Metalsmith('example')
  .metadata({
    site: {
      title: 'Example Blog',
      url: 'https://blog.example.biz',
      author: 'Josephine Examplesmith'
    }
  })
  .use(collections({
    posts: '*.html'
  })
  .use(jsonfeed({
    collection: 'posts'
  })
```

## Options & their defaults

```es6
Metalsmith('example')
  .use(collections({
    posts: '*.html'
  })
  .use(jsonfeed({
    // Required.
    // You must set this to the name of the collection you want to generate the feed from ('posts' in this example)
    collection: undefined,

    // Required if you don't supply site.title in metadata (see above).
    // The title of your feed.
    title: undefined,

    // The file name you want to generate.
    destination: 'feed.json',

    // Limit the number of items in the feed to the last n
    limit: 20

    // Any extra JSON Feed fields you want to set manually.
    // Anything set here will override title, url or author set in site metadata.
    // See https://jsonfeed.org/version/1 for the full list.
    // Don't set `items` though - that's what you're using this plugin for.
    json: {}
  })
```
