# eslint 설정

아래 eslint는 Next.js & airbnb의 기준으로 작성하였습니다.

## eslint-config-next

eslint-config-next는 Next.js 제공하는 eslint입니다.  
Next.js에서 즉시 사용 가능한 Lint 환경이 포함되어 있습니다.  
Next.js를 설치하면 기본으로 구성되어 있습니다.

eslint-config-next에는 eslint-plugin-next이 포함되어 있습니다.
아래 링크에서 lint 항목을 살펴볼 수 있습니다.  
[Next.js 공식문서](https://nextjs.org/docs/pages/building-your-application/configuring/eslint#additional-configurations)

```js
// .eslintrc.json
{
  "extends": "next/core-web-vitals"
}
```

## eslint-config-airbnb

eslint-config-airbnb는 가장 많이 사용하고 있는 대표적인 eslint입니다.

airbnb를 사용하기 위해서는 Dependencies들도 함께 설치해야 합니다.
아래 명령어를 통해 eslint-config-airbnb의 Dependencies 목록을 볼 수 있습니다.

```
npm info "eslint-config-airbnb@latest" peerDependencies
```

```js
// eslint-plugin-import
// eslint-plugin-jsx-a11y
// eslint-plugin-react
// eslint-plugin-react-hooks
```

아래 명령어를 통해 eslint-config-airbnb와 Dependencies 목록을 함께 설치할 수 있습니다.

```
npx install-peerdeps --dev eslint-config-airbnb
```

설치 후 .eslintrc.json 파일을 아래처럼 세팅해줘야 합니다.

```js
  {
    "extends": ["airbnb"]
  }
```

Dependencies 목록들은 extends에 추가할 필요가 없습니다.  
airbnb에 모두 포함되어 있습니다. (airbnb/hooks, eslint:recommended도 마찬가지)

## eslint-config-airbnb-typescript

airbnb의 typescript를 위한 eslint 입니다.
airbnb-typescript도 dependencies 항목이 있습니다.

```
npm install eslint-config-airbnb-typescript \
            @typescript-eslint/eslint-plugin@^6.0.0 \
            @typescript-eslint/parser@^6.0.0 \
            --save-dev

yarn add --dev eslint-config-airbnb-typescript  @typescript-eslint/eslint-plugin@^6.0.0  @typescript-eslint/parser@^6.0.0
```

설치 후 .eslintrc.json 파일을 아래처럼 세팅해줘야 합니다.

```js
  {
     "plugins": [
        "@typescript-eslint",
      ],
    "extends": ["airbnb", "airbnb-typescript"],
    "parserOptions": {
        "project": "./tsconfig.json"
    }
  }
```

## eslint-plugin-simple-import-sort (선택)

import 부분 정리해주는 eslint 입니다.  
필수는 아니고 선택 설치입니다.

```
 yarn add --dev eslint-plugin-simple-import-sort
```

```js

  {
   "plugins": [
     "simple-import-sort",
    ],
    "rules": {
      "simple-import-sort/imports": "error",
      "simple-import-sort/exports": "error",
    },
  }

```

# prettier 설정

## prettier

아래 명령어를 통해 설치해줍니다.

```
yarn add --dev prettier
```

## eslint-config-prettier & eslint-plugin-prettier

아래 명령어를 통해 설치해줍니다.

```
yarn add --dev eslint-config-prettier eslint-plugin-prettier
```

그 후 eslintrc에서 추가해줍니다.

```js
{
  "extends": ["next/core-web-vitals", "prettier","plugin:prettier/recommended"],
   "rules": {
    "prettier/prettier": [
      "error",
      {
        "singleQuote": true,
        "endOfLine": "auto"
      }
    ] // airbnb eslint와의 충돌을 피하기 위해 설정해줍니다.
  },
}
```

--

# husky & lint-staged

husky와 lint-staged를 이용하면, commit 단계에서 eslint와 prettier 검사를 한 후 commit을 할 수 있습니다.

아래 명령어를 통해 설치해줍니다.

```
yarn add --dev husky lint-staged
```

그 후 아래 명령어를 차례대로 실행합니다.

```
npx husky install
npx husky add .husky/pre-commit "yarn lint"
```

마지막으로 package.json에 lint-staged 명령어를 추가합니다.

```js
  "lint-staged": {
    "*.{js,jsx.ts,tsx}": [
      "eslint --fix",
      "prettier --write",
      "git add"
    ]
  }
```

메뉴 / 페이지별로 주차별로 끊어서 진행

큰 덩어리로 나누고

- 그 안에서 작게 쪼개기
- 관련 애들끼리 묶기
- 분량을 찢어서
- 작업자 5명
- 공통을 만들 수 있을 만들기
