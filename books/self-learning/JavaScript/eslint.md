# eslint の導入方法

# [airbnb(es6 のみ)](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb) 追加参考例

```bash
$ npm install --save-dev eslint eslint-plugin-import eslint-config-airbnb-base
```

```json:package.json
"scripts": {
    "lint": "eslint ./scripts/*.js",
    "fix": "eslint --fix ./scripts/*.js"
}
"devDependencies": {
    "eslint": "^6.8.0",
    "eslint-config-airbnb-base": "^14.1.0",
    "eslint-plugin-import": "^2.20.2"
  }
```

```json:.eslintrc
{
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },
  "extends": [
    "airbnb-base"
  ],
  "rules": {
    "indent": ["error", 2],
    "quotes": ["error", "double"],
    "semi": ["error","never"]
  }
}
```

# eslint + prettier 参考例

この辺は会社ルールがあるといいのかもしれない。

```json:.eslintrc.json
{
  "extends": [
    "eslint:recommended",
    "plugin:prettier/recommended"
  ],
  "env": {
    "node": true,
    "es6": true,
    "jest/globals": true
  },
  "plugins": [
    "jest"
  ],
  "rules": {
    "no-console": "off",
    "prettier/prettier": [
      "error",
      {
        "singleQuote": true,
        "trailingComma": "es5",
        "semi": false
      }
    ]
  }
}
```

```json:package.json
    "eslint": "^5.9.0",
    "eslint-config-google": "^0.11.0",
    "eslint-config-prettier": "^3.3.0",
    "eslint-config-standard": "^12.0.0",
    "eslint-plugin-import": "^2.14.0",
    "eslint-plugin-jest": "^22.0.0",
    "eslint-plugin-node": "^8.0.0",
    "eslint-plugin-prettier": "^3.0.0",
    "eslint-plugin-promise": "^4.0.1",
    "eslint-plugin-standard": "^4.0.0",
```

```js:User Settings
    // 抜粋
    "eslint.alwaysShowStatus": true,
    "eslint.enable": true,
    "eslint.options": {
        "configFile": ".eslintrc.json"
    },
    "prettier.eslintIntegration": true,
```

これで、vscode で Alt+Shift+F とかでフォーマットするといい感じになる。保存時にやってないのは現状は実行すると diff 大量になるため、、、プロジェクトの最初からであれば問題ないと思う。
