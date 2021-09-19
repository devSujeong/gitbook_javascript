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
    'react-hooks/exhaustive-deps': [ 
      'error',
      {
        enableDangerousAutofixThisMayCauseInfiniteLoops: true
      }
    ], // react-hook dev dependency 자동 맞춰주기
    quotes: [2, 'single', { avoidEscape: true, allowTemplateLiterals: true }], // 따옴표 규칙
    indent: ['error', 2], // 들여쓰기 규칙
    semi: ['error', 'always'], // 세미콜론 규칙
    'array-bracket-spacing': ['error', 'never'], // 괄호들의 간격 규칙
    'space-before-function-paren': ['error', 'never'], // 함수 이름 옆 파라미터 간격 규칙
    'arrow-parens': ['error', 'always'], // 화살표 함수 디자인 규칙
    'react/react-in-jsx-scope': 'off',
    'react-hooks/rules-of-hooks': 'error' // Checks rules of Hooks
  }
};
```
{% endcode %}



