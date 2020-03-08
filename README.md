Eslint config - DDFAM  
===================  

This is a manual for setting up Eslint and Prettier on a frontend project.

# How LEARN & MAKE  

### Install Eslint dependancies:
```
npm i eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-react-hooks eslint-config-prettier eslint-plugin-prettier prettier --save-dev
```
This will install:
* [AirBnB eslint config](https://www.npmjs.com/package/eslint-config-airbnb "AirBnB eslint config - NPM package page")
* [Eslint plugin - Import](https://www.npmjs.com/package/eslint-plugin-import "Eslint plugin - Import - NPM package page")
* [Eslint plugin - Jsx-a11y](https://www.npmjs.com/package/eslint-plugin-jsx-a11y "Eslint plugin - Jsx-a11y - NPM package page")
* [Eslint plugin - React](https://www.npmjs.com/package/eslint-plugin-react "Eslint plugin - React - NPM package page")
* [Eslint plugin - React hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks "Eslint plugin - React hooks - NPM package page")
* [Prettier eslint config](https://www.google.com "Prettier eslint config - NPM package page")
* [Prettier plugin](https://www.google.com "Prettier plugin - NPM package page")
* [Prettier](https://www.google.com "Prettier - NPM package page")

**PS: If you are not using create-react-app you will need to install Eslint aswell**
`npm i eslint --save-dev`

#### Set up the rules:
Create a `.eslintrc` file in the root folder of your project and add the folowing ruleset:
```JSON
{
    "extends": [
        "airbnb",
        "prettier",
        "prettier/react"
    ],
    "parser": "babel-eslint",
    "parserOptions": {
        "ecmaVersion": 2020,
        "ecmaFeatures": {
            "impliedStrict": true,
            "classes": true
        }
    },
    "env": {
        "browser": true,
        "node": true,
        "jquery": true,
        "jest": true
    },
    "rules": {
        "no-use-before-define": [
            "warn",
            {
                "functions": true,
                "classes": true
            }
        ],
        "indent": [
            "error",
            "tab"
        ],
        "no-debugger": 0,
        "no-alert": 0,
        "no-await-in-loop": 0,
        "no-return-assign": [
            "error",
            "except-parens"
        ],
        "no-restricted-syntax": [
            2,
            "ForInStatement",
            "LabeledStatement",
            "WithStatement"
        ],
        "no-unused-vars": [
            1,
            {
                "ignoreSiblings": true,
                "argsIgnorePattern": "res|next|^err"
            }
        ],
        "prefer-const": [
            "error",
            {
                "destructuring": "all",
            }
        ],
        "arrow-body-style": [
            2,
            "as-needed"
        ],
        "no-unused-expressions": [
            2,
            {
                "allowTaggedTemplates": true
            }
        ],
        "no-param-reassign": [
            2,
            {
                "props": false
            }
        ],
        "no-console": 0,
        "import/prefer-default-export": 0,
        "import": 0,
        "func-names": 0,
        "space-before-function-paren": 0,
        "comma-dangle": 0,
        "max-len": 0,
        "import/extensions": 0,
        "no-underscore-dangle": 0,
        "consistent-return": 0,
        "react/display-name": 1,
        "react/no-array-index-key": 0,
        "react/react-in-jsx-scope": 0,
        "react/prefer-stateless-function": 0,
        "react/forbid-prop-types": 0,
        "react/no-unescaped-entities": 0,
        "jsx-a11y/accessible-emoji": 0,
        "react/require-default-props": 0,
        "react/jsx-filename-extension": [
            1,
            {
                "extensions": [
                    ".js",
                    ".jsx"
                ]
            }
        ],
        "radix": 0,
        "no-shadow": [
            2,
            {
                "hoist": "all",
                "allow": [
                    "resolve",
                    "reject",
                    "done",
                    "next",
                    "err",
                    "error"
                ]
            }
        ],
        "quotes": [
            2,
            "single",
            {
                "avoidEscape": true,
                "allowTemplateLiterals": true
            }
        ],
        "prettier/prettier": [
            "error",
            {
                "trailingComma": "es5",
                "singleQuote": true,
                "printWidth": 80,
                "useTabs": true
            }
        ],
        "jsx-a11y/href-no-hash": "off",
        "jsx-a11y/anchor-is-valid": [
            "warn",
            {
                "aspects": [
                    "invalidHref"
                ]
            }
        ],
        "react-hooks/rules-of-hooks": "error",
        "react-hooks/exhaustive-deps": "warn"
    },
    "plugins": [
        "prettier",
        "react-hooks"
    ]
}
```

#### Add linting scripts:
To lint on command add the following in your `package.json` file:
```JSON
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint . --fix"
},
``` 

#### VSCode settings:
To add linting on save with VSCode; install the [ESlint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint "Eslint extension on Marketplace") extension and add the following setting to your `settings.json` file:
```JSON
"editor.formatOnSave": true,
"[javascript]": {
  "editor.formatOnSave": false
},
"[javascriptreact]": {
  "editor.formatOnSave": false
},
"editor.codeActionsOnSave": {
  "source.fixAll": true
},
```
If you are using the VSCode Prettier extension enabled, turn it off for JavaScript. Eslint will fix this.
```JSON
"prettier.disableLanguages": ["javascript", "javascriptreact"],
``` 

### Optional, but best practice:
#### Set up husky and lint-staged - Not tested yet!
To ensure that Eslint and Prettier will be run every time we can set up [Husky](https://www.npmjs.com/package/husky "Husky - NPM package page")  and [Lint staged](https://www.npmjs.com/package/lint-staged "Lint staged - NPM package page") to run our linting before any commit:
```
npm install  husky lint-staged --save-dev
```
Setup husky and lint-staged in your `package.json` by adding:
```JSON
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  }
},
{
  "lint-staged": {
    "*.+(js|jsx)": ["eslint --fix", "git add"],
    "*.+(json|css|md)": ["prettier --write", "git add"]
  }
}
```
This will run the `eslint --fix` script every time a commit has been done on only the staged files. Hopefully everything if fine!

## Links:
[AirBnB - Javascript style guide](https://github.com/airbnb/javascript "Link to AirBnB - Javascript style guide")
[Eslint - Hompage](https://eslint.org/ "Link to Eslint homepage")
[Prettier - Homepage](https://prettier.io/ "Link to Prettier homepage")