[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

A [Metalsmith](http://www.metalsmith.io/) plugin for generating a [JSON Feed](https://jsonfeed.org/) from a [collection](https://github.com/segmentio/metalsmith-collections).

`npm install --save metalsmith-json-feed`
or
`yarn add metalsmith-json-feed`

Heavily inspired by [metalsmith-feed](https://github.com/hurrymaplelad/metalsmith-feed).

## Usage

### Basic

```es6
const Metalsmith = require('metalsmith')
const collections = require('metalsmith-collections')
const jsonfeed = require('metalsmith-json-feed')

Metalsmith('example')
  .use(collections({
    posts: '*.html'
  }))
  .use(jsonfeed({
    collection: 'posts',
    title: 'Example feed'
  }))
```

### Using metadata

If your site has `title`, `url` or `author` metadata, they will be used (you can override them by setting options, see below).

```es6
const Metalsmith = require('metalsmith')
const collections = require('metalsmith-collections')
const jsonfeed = require('metalsmith-json-feed')

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
  }))
  .use(jsonfeed({
    collection: 'posts'
  }))
```

### Item metadata

Items get their `url` field from the file's path by default. To direct links elsewhere, you can override the URL by providing a `link` metadata entry for a file:

```
---
link: http://example.com
---
This post is an external link.
```

## Options & their defaults

```es6
Metalsmith('example')
  .use(collections({
    posts: '*.html'
  }))
  .use(jsonfeed({
    collection: undefined,
    // (Required)
    // You must set this to the name of the collection you want to generate the feed from ('posts' in this example)

    title: undefined,
    // (Required, unless you supply site.title in metadata - see Metadata example above)
    // The title of your feed.

    destination: 'feed.json',
    // (Optional)
    // The file name you want to generate.

    limit: 20
    // (Optional)
    // Limit the number of items in the feed to the last n

    json: {}
    // (Optional)
    // Any extra JSON Feed fields you want to set manually.
    // Anything set here will override title, url or author values found in metadata.
    // See https://jsonfeed.org/version/1 for the full list.
    // (Don't set `items` though - that's what you're using this plugin to generate)
  }))
```
