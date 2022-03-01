# Adding eslint & prettier

## Install

- Run the following comand and install eslint and @angular-eslint/schematics

```bash
ng lint
```

## Installing eslint plugin, prettier and stylelint

```bash
npm i -D eslint-plugin-import eslint-plugin-simple-import-sort prettier 
```

## Create a file `.eslintignore`

```bash
package.json
package-lock.json
dist
e2e/**
node_modules/**
```

## Create a file `.prettierrc`

```bash
{
   "arrowParens": "always",
   "bracketSameLine": false,
   "bracketSpacing": true,
   "embeddedLanguageFormatting": "auto",
   "htmlWhitespaceSensitivity": "css",
   "insertPragma": false,
   "jsxSingleQuote": false,
   "printWidth": 80,
   "proseWrap": "preserve",
   "quoteProps": "as-needed",
   "requirePragma": false,
   "semi": true,
   "singleQuote": true,
   "tabWidth": 2,
   "trailingComma": "es5",
   "useTabs": false,
   "vueIndentScriptAndStyle": false
}
```

## Create a file `.prettierignore`

```bash
dist
e2e/**
node_modules/**
build
coverage
```


## Adding extra rules to eslint

.eslintrc.json 
- Don't forget to chnge the prefix name from mf-nav to yours

```json
{
  "root": true,
  "ignorePatterns": ["projects/**/*"],
  "plugins": ["simple-import-sort", "import"],
  "globals": {
    "setTimeout": "readonly",
    "setInterval": "readonly",
    "clearTimeout": "readonly",
    "clearInterval": "readonly",
    "exports": "readonly",
    "console": "readonly",
    "process": "readonly",
    "window": "readonly",
    "describe": "readonly",
    "it": "readonly",
    "beforeEach": "readonly",
    "afterEach": "readonly",
    "beforeAll": "readonly",
    "afterAll": "readonly",
    "jest": "readonly",
    "expect": "readonly",
    "require": "readonly",
    "module": "readonly",
    "__dirname": "readonly",
    "__filename": "readonly",
    "__webpack_public_path__": "readonly"
  },
  "rules": {
    "no-dupe-args": "error",
    "no-func-assign": "error",
    "for-direction": "error",
    "no-dupe-else-if": "error",
    "no-empty": [
      "error",
      {
        "allowEmptyCatch": true
      }
    ],
    "no-debugger": "error",
    "no-console": "error",
    "no-sparse-arrays": "error",
    "no-unreachable": "error",
    "no-template-curly-in-string": "error",
    "no-cond-assign": ["error", "except-parens"],
    "no-constant-condition": "error",
    "no-undef": "warn",
    "no-unused-expressions": "error",
    "no-unused-labels": "error",
    "no-useless-escape": "error",
    "no-useless-return": "error",
    "no-void": "error",
    "no-with": "error",
    "no-dupe-class-members": "error",
    "no-empty-character-class": "error",
    "no-ex-assign": "error",
    "no-extra-boolean-cast": "error",
    "valid-typeof": "error",
    // End of line
    "comma-style": ["warn", "last"],
    "semi": ["warn", "always"],
    "semi-spacing": "warn",
    "no-extra-semi": "warn",
    "comma-dangle": ["warn", "always-multiline"],
    // Comments
    "no-unexpected-multiline": "error",
    "multiline-comment-style": ["error", "starred-block"],
    "spaced-comment": "warn",
    // // Imports
    "simple-import-sort/imports": "warn",
    "simple-import-sort/exports": "warn",
    "import/newline-after-import": "warn",
    "import/first": "warn",
    "import/no-duplicates": "warn",
    // Braces
    "brace-style": "warn",
    "space-before-blocks": "warn"
  },
  "overrides": [
    {
      "files": ["*.js"],
      "parserOptions": {
        "ecmaVersion": "latest",
        "sourceType": "module"
      },
      "env": {
        "es6": true
      },
      "rules": {
        "no-console": "off"
      }
    },
    {
      "files": ["*.ts"],
      "parserOptions": {
        "project": ["tsconfig.json"],
        "createDefaultProgram": true,
        "ignoreConfigFiles": true
      },
      "extends": [
        "plugin:@angular-eslint/recommended",
        "plugin:@angular-eslint/template/process-inline-templates"
      ],
      "rules": {
        "@angular-eslint/directive-selector": [
          "error",
          {
            "type": "attribute",
            "prefix": "mf-nav",
            "style": "camelCase"
          }
        ],
        "@angular-eslint/component-selector": [
          "error",
          {
            "type": "element",
            "prefix": "mf-nav",
            "style": "kebab-case"
          }
        ]
      }
    },
    {
      "files": ["*.html"],
      "extends": ["plugin:@angular-eslint/template/recommended"],
      "rules": {}
    }
  ]
}
```

## Add script to package.json

```json
{
  "lint": "npx eslint \"**/*.{js,ts,tsx,css}\" --quiet --fix",
  "prettier": "npx prettier --write .",
}
```


## Optional

- Add lint-staged

```bash
npm install -D lint-staged
```

- In package.json
```bash
"lint-staged": {
    "*.{js,ts,tsx,css}": "eslint --cache --fix",
    "*.*": "prettier --write --ignore-unknown"
  }
```
- Add script in package.json
```bash
"pre-commit": "npx lint-staged",
```

