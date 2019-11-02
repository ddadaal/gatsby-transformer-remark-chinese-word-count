# gatsby-transformer-remark-chinese-word-count

A fork of [gatsby-transformer-remark](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-transformer-remark) which approximately counts Chinese characters.

This plugin adds a new `Int` field `wordCountChinese` onto each node of the GraphQL query.

Theoretically, it counts each Chinese character and each part splitted by space char (`\s`) as a word. 

The resulting value is **close to and usually more than** the result from Microsoft Word.

| Article | Language | Result of `wordCount.words` from original plugin | Result from this plugin | Result from Microsoft Word |
| -- | -- | -- | -- | -- |
| https://ddadaal.me/articles/playing-with-linux-from-machine-to-win10 | Chinese | 587 | 5232 | 5211 |
| https://ddadaal.me/articles/a-react-form-comp-pref-optimization-with-profiler | English | 1532 | 1939 | 1653 |

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        wordCountChinese
      }
    }
  }
}
```
# Install 

Not yet released

`npm install --save gatsby-transformer-remark-chinese-word-count`

or

`yarn add --save gatsby-transformer-remark-chinese-word-count`

# How it works?

The only modified file is [extend-node-type.js](extend-node-type.js).

This plugins uses lodash's `words` to calculate the wordCount with the pattern `/[\s\p{sc=Han}]/gu`, which should match all Chinese characters as an individual word, and also matches an English words as a word.

# Cohesion with Upstream

Until the upstream has solved the problem (which seems unlikely according to the status of [the original issue of remark](https://github.com/wooorm/remark/issues/251#issuecomment-296731071)), this project will merge updates from upstream [gatsby-transformer-remark](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-transformer-remark) when **I think it is needed**. An automated process might be established in the future. Current upstream version can be checked from the [CHANGELOG](CHANGELOG.md).

# License

MIT