# Adding cypress cucumber 

## Install Cypress

```sh
npm i -D cypress
```

## Create cypress config

- Run 
```sh
npx cypress open
```
This will create cypress file configuration and cypress folder on root

## Edit cypress.json

- Move cypress directory if needed and confire that in cypress.json

```json
{
  "integrationFolder": "testing/cypress/integration",
  "supportFile": "testing/cypress/support/index.js",
  "videosFolder": "testing/cypress/videos",
  "screenshotsFolder": "testing/cypress/screenshots",
  "pluginsFile": "testing/cypress/plugins/index.js",
  "fixturesFolder": "testing/cypress/fixtures",
  "baseUrl": "http://localhost:9001/two"
}
```

## Eslint for cypress
- Install `eslint-plugin-cypress`

```sh
  npm i -D eslint-plugin-cypress
```

- Create a `.eslintrc.json` on inside cypress folder

```json
{
  "extends": ["plugin:cypress/recommended", "../../.eslintrc.json"],
  "ignorePatterns": ["!**/*"],
  "overrides": [
    {
      "files": ["*.ts", "*.tsx", "*.js", "*.jsx"],
      "rules": {}
    },
    {
      "files": ["plugins/index.js"],
      "rules": {
        "@typescript-eslint/no-var-requires": "off",
        "no-undef": "off"
      }
    }
  ]
}

```

# Installin cucumber preprocessor

-  Install cucumber cypress plugin
```sh
  npm install -D cypress-cucumber-preprocessor
```

- Add cucumber plugin to cypress config 

```
const cucumber = require('cypress-cucumber-preprocessor').default;

...
on('file:preprocessor', cucumber());
```

`plugins.index.js` should look like this  

```js

const cucumber = require('cypress-cucumber-preprocessor').default;

/**
 * @type {Cypress.PluginConfig}
 */
// eslint-disable-next-line no-unused-vars
module.exports = (on, config) => {
  // `on` is used to hook into various events Cypress emits
  // `config` is the resolved Cypress config
  on('file:preprocessor', cucumber());
};

```




