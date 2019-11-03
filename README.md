# gatsby-transformer-remark-chinese-word-count

Reference project for the solution mentioned in the article [修复gatsby-transformer-remark插件中文词数统计错误问题](https://ddadaal.me/articles/fix-gatsby-transformer-remark-chinese-word-count). 

View the article for **solutions** for wrong Chinese word count in [gatsby-transformer-remark](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-transformer-remark) and the **reasons why this package is NOT going to be published to npm**.

This plugin adds a new `Int` field `wordCountChinese` onto each node of the GraphQL query.

Theoretically, it counts each Chinese character and each part splitted by space char (`\s`) as a word. 

The resulting value is **close to and usually more than** the result from Microsoft Word.

| Article | Language | Result of `wordCount.words` from original plugin | Result from this plugin | Result from Microsoft Word |
| -- | -- | -- | -- | -- |
| https://ddadaal.me/articles/playing-with-linux-from-machine-to-win10 | Chinese | 587 | 5232 | 5211 |
| https://ddadaal.me/articles/a-react-form-comp-pref-optimization-with-profiler | English | 1532 | 1939 | 1653 |


# Install and Usage

1. Download the files of this project to `plugins/gatsby-transformer-remark-chinese-word-count` directory of your project. Mkdir if any doesn't exist.

2. Use `gatsby-transformer-remark-chinese-word-count` wherever `gatsby-transformer-remark` is used, for example, `gatsby-config.js`.

3. Query `wordCountChinese` field on each node of `allMarkdownRemark` to get the result.

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

# How it works?

The only modified file is [extend-node-type.js](extend-node-type.js).

This plugins uses lodash's `words` to calculate the wordCount with the pattern `/[\s\p{sc=Han}]/gu`, which should match all Chinese characters as an individual word, and also matches an English words as a word.

# Further Reading

[修复gatsby-transformer-remark插件中文词数统计错误问题](https://ddadaal.me/articles/fix-gatsby-transformer-remark-chinese-word-count)


# License

MIT