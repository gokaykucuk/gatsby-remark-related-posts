# gatsby-remark-related-posts

[![npm version](https://badge.fury.io/js/gatsby-remark-related-posts.svg)](https://badge.fury.io/js/gatsby-remark-related-posts)

Calculate the similarity between posts and make it available from graphql.

To calculate the similarity, this plugin using [tf-idf](https://en.wikipedia.org/wiki/Tf%E2%80%93idf) and [Cosine similarity](https://en.wikipedia.org/wiki/Cosine_similarity).

## Installation

`npm i --save gatsby-remark-related-posts`

## Usage

In your `gatsby-config.js`:

```javascript
{
  resolve: "gatsby-remark-related-posts",
  options: {
    posts_dir: `${__dirname}/posts`,
    doc_lang: "ja",
  },
},
```

| option      | description                                                                  |
| :---------- | :--------------------------------------------------------------------------- |
| `posts_dir` | directory that includes your markdown files.                                 |
| `doc_lang`  | ISO 639-1 language code of your post. This supports `en` and `ja` currently. |

This creates a new `relatedFileAbsolutePaths` field on each `MarkdownRemark` node, like this:

```javascript
// query
query {
  allMarkdownRemark {
    nodes {
      fileAbsolutePath
      fields {
        relatedFileAbsolutePaths
      }
    }
  }
}
```

```javascript
// result
{
  "data": {
    "allMarkdownRemark": {
      "nodes": [
        {
          "fileAbsolutePath": "/home/user/blog/posts/markdown1.md",
          "fields": {
            "relatedFileAbsolutePaths": [
              "/home/user/blog/posts/markdown4.md",
              "/home/user/blog/posts/markdown2.md",
              "/home/user/blog/posts/markdown3.md"
            ]
          }
        },
        ...
      ]
    }
  }
}
```

These paths are sorting by similarity. In this example, first "/home/user/blog/posts/markdown4.md" is the most related to "/home/user/blog/posts/markdown1.md".

## Licence

MIT
