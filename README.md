Eslint config - DDFAM
===================  

This is a installation manual for setting up Eslint and Prettier on a frontend project.<br/>
The config is currently under review and is a "Work in Progress".

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

### Set up the rules:
Create a `.eslintrc` file in the root folder of your project and add the folowing ruleset:<br/>
[Eslintrc fil](https://github.com/CapgeminiNorway/eslint-config-ddfam/blob/master/.eslintrc "CapgeminiNorway - Eslintrc fil")


### Add linting scripts:
To lint on command add the following in your `package.json` file:
```JSON
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint . --fix"
},
``` 

### VSCode settings:
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

## Rule explanation:
* **Eslint rules:**
* [no-use-before-define](https://eslint.org/docs/rules/no-use-before-define "Eslint documentation")
* [indent](https://eslint.org/docs/rules/indent "Eslint documentation")
* [no-debugger](https://eslint.org/docs/rules/no-debugger "Eslint documentation")
* [no-alert](https://eslint.org/docs/rules/no-alert#top "Eslint documentation")
* [no-await-in-loop](https://eslint.org/docs/rules/no-await-in-loop "Eslint documentation")
* [no-return-assign](https://eslint.org/docs/rules/no-return-assign "Eslint documentation")
* [no-restricted-syntax](https://eslint.org/docs/rules/no-restricted-syntax "Eslint documentation")
* [no-unused-vars](https://eslint.org/docs/rules/no-unused-vars "Eslint documentation")
* [prefer-const](https://eslint.org/docs/rules/prefer-const "Eslint documentation")
* [arrow-body-style](https://eslint.org/docs/rules/arrow-body-style "Eslint documentation")
* [no-unused-expressions](https://eslint.org/docs/rules/no-unused-expressions "Eslint documentation")
* [no-param-reassign](https://eslint.org/docs/rules/no-param-reassign "Eslint documentation")
* [no-console](https://eslint.org/docs/rules/no-console "Eslint documentation")
* [func-names](https://eslint.org/docs/rules/func-names "Eslint documentation")
* [space-before-function-paren](https://eslint.org/docs/rules/space-before-function-paren "Eslint documentation")
* [comma-dangle](https://eslint.org/docs/rules/comma-dangle "Eslint documentation")
* [max-len](https://eslint.org/docs/rules/max-len "Eslint documentation")
* [no-underscore-dangle](https://eslint.org/docs/rules/no-underscore-dangle "Link to no-underscore-dangle - Eslint documentation")
* [radix](https://eslint.org/docs/rules/radix "Eslint documentation")
* [no-shadow](https://eslint.org/docs/rules/no-shadow "Eslint documentation")
* [quotes]([https](https://eslint.org/docs/rules/quotes) "Eslint documentation")
* **Import rules:**
* [import](https "Eslint documentation")
  * Can't find rule or docs..
* [import/prefer-default-export](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md "Github documentation")
* [import/extensions](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/extensions.md "Github documentation")
* [consistent-return](https://eslint.org/docs/rules/consistent-return "Link to consistent-return - Eslint documentation")
* **React rules:**
* [react/display-name](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/display-name.md "Github documentation")
* [react/no-array-index-key](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-array-index-key.md "Github documentation")
* [react/react-in-jsx-scope](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/react-in-jsx-scope.md "Github documentation")
* [react/prefer-stateless-function](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-stateless-function.md "Github documentation")
* [react/forbid-prop-types](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/forbid-prop-types.md "Github documentation")
* [react/no-unescaped-entities](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-unescaped-entities.md "Github documentation")
* [react/require-default-props](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/require-default-props.md "Github documentation")
* [react/jsx-filename-extension](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-filename-extension.md "Github documentation")
* **React hooks rules:**
* [react-hooks/rules-of-hooks](https://reactjs.org/docs/hooks-rules.html#eslint-plugin "React hooks documentation")
  * Checks rules of Hooks
* [react-hooks/exhaustive-deps](https://reactjs.org/docs/hooks-rules.html#eslint-plugin "React hooks documentation")
  * Checks effect dependencies
* **Jsx-a11y rules:**
* [jsx-a11y/accessible-emoji](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/accessible-emoji.md "Github documentation")
* [jsx-a11y/href-no-hash](https://www.npmjs.com/package/eslint-plugin-jsx-a11y "NPM package page")
  * This rule seems to be deprecated and if therefor turned off. Anchor is valid has replaced this.
* [jsx-a11y/anchor-is-valid](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/anchor-is-valid.md "Github documentation")
* **Prettier rules:**
* [Prettier - trailingComma]([https](https://prettier.io/docs/en/options.html#trailing-commas) "Prettier documentation")
* [Prettier - singleQuote](https://prettier.io/docs/en/options.html#quotes "Prettier documentation")
* [Prettier - printWidth](https://prettier.io/docs/en/options.html#print-width "Prettier documentation")
* [Prettier - useTabs](https://prettier.io/docs/en/options.html#tabs "Prettier documentation")

## Links:
[AirBnB - Javascript style guide](https://github.com/airbnb/javascript "Link to AirBnB - Javascript style guide")
[Eslint - Hompage](https://eslint.org/ "Link to Eslint homepage")
[Prettier - Homepage](https://prettier.io/ "Link to Prettier homepage")