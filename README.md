# eslint-config-htmlacademy

ESLint [shareable config](http://eslint.org/docs/developer-guide/shareable-configs.html) for the [HTML Academy](http://htmlacademy.ru) courses

## Installation

```bash
npm install --save-dev eslint-config-htmlacademy
```

Package requires `eslint`. You must install it manually.

## Usage

Once the `eslint-config-htmlacademy` package is installed, you can use it by specifying `htmlacademy` in the [`extends`](http://eslint.org/docs/user-guide/configuring#extending-configuration-files) section of your [ESLint configuration](http://eslint.org/docs/user-guide/configuring).

For validating **Vanilla JS** project use `vanilla` version:

```json
{
  "parserOptions": {
    "ecmaVersion": 2023,
    "sourceType": "module"
  },
  "env": {
    "es2023": true,
    "browser": true
  },
  "extends": "htmlacademy/vanilla",
  "rules": {
    // Additional rules...
  }
}
```

For validating **React** project use `react` version (`htmlacademy/react` includes `react/recommended`):

```json
{
  "parserOptions": {
    "ecmaVersion": 2019,
    "sourceType": "module"
  },
  "env": {
    "es2017": true,
    "browser": true
  },
  "extends": "htmlacademy/react",
  "rules": {
    // Additional rules...
  }
}
```

For validating **React** project with TypeScript use `react-typescript` version (`htmlacademy/react-typescript` includes `react/recommended`, `@typescript-eslint/recommended` and `@typescript-eslint/recommended-requiring-type-checking`).

Before using `eslint-config-htmlacademy` make sure you have TypeScript, `@typescript-eslint/parser`, `@typescript-eslint/eslint-plugin` installed:

```bash
$ npm i --save-dev typescript @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

```json
{
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "parserOptions": {
    "ecmaVersion": 2020,
    "sourceType": "module",
    "project": [
      "tsconfig.json" // path to your tsconfig file
    ]
  },
  "env": {
    "es2017": true,
    "browser": true
  },
  "extends": "htmlacademy/react-typescript",
  "rules": {
    // Additional rules...
  }
}
```

Caution! `htmlacademy/react` and `htmlacademy/react-typescript` doesn't include `react-hooks/rules-of-hooks` and `react-hooks/exhaustive-deps` because in our courses we use CRA (Create React App) which includes these plugins out of box. Install them yourself if necessary.

Caution! If you're wanting to use `toBeCalled` and similar matches in jest tests, you can use next option for `eslintConfig`:

```json
"eslintConfig": {
  "overrides": [
    {
      "files": ["*test*"], // regExp to answer the question "How to find your tests?"
      "rules": {
        "@typescript-eslint/unbound-method": "off",
        "jest/unbound-method": "error"
      }
    }
  ]
}
```

Why this is necessary, you can read on the [next page](https://github.com/jest-community/eslint-plugin-jest/blob/main/docs/rules/unbound-method.md).

For validating **Node** project use `node` version (`htmlacademy/node` includes `htmlacademy/vanilla`, `plugin:@typescript-eslint/recommended` and `plugin:node/recommended`).

Before using `eslint-config-htmlacademy` make sure you have TypeScript and `@typescript-eslint/parser` installed:

```bash
$ npm i --save-dev typescript @typescript-eslint/parser
```

Then install the plugin:

```bash
$ npm i --save-dev @typescript-eslint/eslint-plugin
```

```json
{
  "env": {
    "es2021": true,
    "node": true
  },
  "parserOptions": {
    "ecmaVersion": 2021,
    "sourceType": "module"
  },
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "extends": "htmlacademy/node",
  "rules": {
    // Additional rules...
  }
}
```

Caution!
- `htmlacademy/node` aimed at using Typescript.
- `htmlacademy/node` recommends a use of the "engines" field of package.json, because our package includes `plugin:node/recomended`. The "engines" field is used by `node/no-unsupported-features/*` rules.
- `htmlacademy/node` uses ES6 modules and the rules are aimed precisely at this approach of connecting modules.
