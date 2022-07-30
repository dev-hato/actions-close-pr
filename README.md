# actions-close-pr

※本Actionsは <https://github.com/dev-hato/actions-diff-pr-management> と併用することを前提としています。

<https://github.com/dev-hato/actions-diff-pr-management> はPRのブランチに対して、フォーマッタを実行した結果をPRにするGitHub Actionsです。

元のPRを閉じた場合、 <https://github.com/dev-hato/actions-diff-pr-management> が立てたPRは残ります。  

このような場合、本Actionsを併用することで自動的にPRを閉じることができます。

## 使い方
### package.json

```json
{
  "devDependencies": {
    "js-yaml": "4.1.0",
    ...
  },
  ...
}
```

### GitHub Actions

```yaml
on:
  pull_request:
    types:
      - closed

jobs:
  close-pr:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          cache: npm
      - run: npm ci --prefer-offline
      - uses: dev-hato/actions-close-pr@v1
        with:
          github-token: ${{secrets.GITHUB_TOKEN}}
```

## 引数

|          引数名          |                           説明                           | 必須  |
|:---------------------:|:------------------------------------------------------:|:---:|
|     github-token      |                      GitHubのトークン                       |  O  |

## 開発

### 設定

<https://pre-commit.com/> の手順に従って `pre-commit` をインストールします。  
これにより、コミット時にクレデンシャルが含まれていないかの検査が行われるようになります。
