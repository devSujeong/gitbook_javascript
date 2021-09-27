# eslint 설정

## vscode에서 eslint 자동 포맷팅 기능까지 사용하려면

settings\(`cmd` + `,`\)에서 아래 내용 작성

```javascript
{
    "eslint.alwaysShowStatus": true, 
    "editor.codeActionsOnSave": { "source.fixAll.eslint": true }, 
    "editor.formatOnSave": true,
}
```

## Creation

```bash
npx eslint --init
```

## eslintrc

{% code title=".eslintrc.js" %}
```javascript
module.exports = {
  env: {
    browser: true,
    es2021: true
  },
  extends: [
    'plugin:react/recommended',
    'standard',
    'plugin:@typescript-eslint/recommended',
    'next',
    'next/core-web-vitals'
  ],
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaFeatures: {
      jsx: true
    },
    ecmaVersion: 12,
    sourceType: 'module'
  },
  plugins: [
    'react',
    '@typescript-eslint',
    'react-hooks', 'import', 'jsx-a11y'
  ],
  rules: {
    indent: ['error', 2],
    'linebreak-style': ['error', 'unix'],
    quotes: [2, 'single', {avoidEscape: true, allowTemplateLiterals: true}],
    semi: ['error', 'always'],
    'comma-dangle': ['error', 'never'],
    'max-len': [
      'error',
      {
        code: 80,
        ignoreComments: true,
        ignoreTrailingComments: true,
        ignoreUrls: true,
        ignoreStrings: true,
        ignoreTemplateLiterals: true,
        ignoreRegExpLiterals: true,
      },
    ],
    'array-bracket-spacing': ['error', 'never'],
    'space-before-function-paren': ['error', 'never'],
    'arrow-parens': ['error', 'always'],
    'react/react-in-jsx-scope': 'off',
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': [
      'error',
      {
        enableDangerousAutofixThisMayCauseInfiniteLoops: true,
      },
    ],
  }
};
```
{% endcode %}



