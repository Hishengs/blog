---
title: 在 Git 代码提交前执行 ESLint 检查
date: 2018-02-12 18:26:35
tags:
- git
- eslint
---

之前一直想做的一个 Git 前端代码检查操作，今天终于把它弄好了。具体操作如下：

<!-- more -->

### 安装 ESLint 以及相关库
```js
npm i –save-dev eslint eslint-config-bitpower eslint-plugin-html eslint-plugin-import eslint-plugin-vue
```

### 创建 pre-commit
在项目的 .git/hooks 目录下，创建文件，命名为 `pre-commot`（无后缀）：
```shell
#!/bin/sh

STAGED_FILES=$(git diff --cached --name-only --diff-filter=ACM | grep ".jsx\{0,1\}$")

ESLINT="$(git rev-parse --show-toplevel)/node_modules/.bin/eslint"

if [[ "$STAGED_FILES" = "" ]]; then
  exit 0
fi

PASS=true

echo "Validating Javascript:"

# Check for eslint
which eslint &> /dev/null
# if [[ "$?" == 1 ]]; then
if [[ ! -x "$ESLINT" ]]; then
  echo "\t\033[41mPlease install ESlint\033[0m"
  exit 1
fi

for FILE in $STAGED_FILES
do
#  eslint "$FILE"
  "$ESLINT" "$FILE"

  if [[ "$?" == 0 ]]; then
    echo "\t\033[32mESLint Passed: $FILE\033[0m"
  else
    echo "\t\033[41mESLint Failed: $FILE\033[0m"
    PASS=false
  fi
done

echo "Javascript validation completed!"

if ! $PASS; then
  echo "\033[41mCOMMIT FAILED:\033[0m Your commit contains files that should pass ESLint but do not. Please fix the ESLint errors and try again."
  exit 1
else
  echo "\033[42mCOMMIT SUCCEEDED\033[0m"
fi

exit $?
```

### 检查测试
ok，现在改动一下你的代码，然后提交它，看看是否有 ESLint 检查提示或者报错。