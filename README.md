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
#### Eslint rules:
* [no-use-before-define](https://eslint.org/docs/rules/no-use-before-define "Eslint documentation") 
  * Don't use a function before it is defined: Set to warn
* [indent](https://eslint.org/docs/rules/indent "Eslint documentation") 
  * Indent style: Set to tabs
* [no-debugger](https://eslint.org/docs/rules/no-debugger "Eslint documentation") 
  * Don't call debugger: Set to warn
* [no-alert](https://eslint.org/docs/rules/no-alert#top "Eslint documentation") 
  * Don't use alert: Set to warn
* [no-await-in-loop](https://eslint.org/docs/rules/no-await-in-loop "Eslint documentation") 
  * Don't use await in loops: Set to off
* [no-return-assign](https://eslint.org/docs/rules/no-return-assign "Eslint documentation")
  * Disallow Assignment in return - Set to default; Not allowed unless they are enclosed in parentheses.
* [no-restricted-syntax](https://eslint.org/docs/rules/no-restricted-syntax "Eslint documentation")
  * Disallow specified syntax: Set to error
    * ForInStatement
    * LabeledStatement
    * WithStatement
* [no-unused-vars](https://eslint.org/docs/rules/no-unused-vars "Eslint documentation")
  * This rule is aimed at eliminating unused variables, functions, and function parameters: Set to warn
    * ignoreRestSiblings - set to true
    * argsIgnorePattern - is set to ignore variables with "res|next|^err" included
* [prefer-const](https://eslint.org/docs/rules/prefer-const "Eslint documentation")
  * Used to flag variables that are not reassigned and should be a const - Set to error
    * destructuring is set to "all", allows destructured variables to be a let if not all the variable are reassigned
* [arrow-body-style](https://eslint.org/docs/rules/arrow-body-style "Eslint documentation")
  * Enforce or disallow the use of braces around arrow function body - Set to "as-needed" to allow not to have braces around the body when not needed.
* [no-unused-expressions](https://eslint.org/docs/rules/no-unused-expressions "Eslint documentation")
  * Eliminate unused expressions which have no effect on the state of the program - Set to error
    * allowTaggedTemplates: Enable you to use tagged template literals in your expressions - Set to true
* [no-param-reassign](https://eslint.org/docs/rules/no-param-reassign "Eslint documentation")
  * Prevent unintended behavior caused by modification or reassignment of function parameters - Set to error
    * props - Set back to false to overwrite AirBnB setup
* [no-console](https://eslint.org/docs/rules/no-console "Eslint documentation")
  * Disallows console.log() - set to warn
* [func-names](https://eslint.org/docs/rules/func-names "Eslint documentation")
  * Enforce or disallow the use of named function expressions
  * Turned off
* [space-before-function-paren](https://eslint.org/docs/rules/space-before-function-paren "Eslint documentation")
  * Enforces or disallows space before function parentheses
  * Turned off, Prettier deals with this
* [comma-dangle](https://eslint.org/docs/rules/comma-dangle "Eslint documentation")
  * Allows of disallows 
  * Turned off, Prettier deals with this
* [max-len](https://eslint.org/docs/rules/max-len "Eslint documentation")
  * Enforces a maximum line length to increase code readability and maintainability
  * Turned off, Prettier deals with this
* [no-underscore-dangle](https://eslint.org/docs/rules/no-underscore-dangle "Link to no-underscore-dangle - Eslint documentation")
  * This rule disallows dangling underscores in identifiers
  * Turned off, unsure if Pretter deals with this
* [radix](https://eslint.org/docs/rules/radix "Eslint documentation")
  * Aimed at preventing the unintended conversion of a string to a number of a different base than intended or at preventing the redundant 10 radix if targeting modern environments only
  * Turned off
* [no-shadow](https://eslint.org/docs/rules/no-shadow "Eslint documentation")
  * Aims to eliminate shadowed variable declarations (Variables that are repeated and set again inside a function)
  * Set to error
    * Hoist is set to all: Reports all shadowing before the outer variables/functions are defined
    * Allow is set to allow shadowing on: resolve, reject, done, next, err, and error
* [quotes](https://eslint.org/docs/rules/quotes "Eslint documentation")
  * Enforces the consistent use of single quotes
  * avoidEscape is set to true, this allows strings to use single-quotes or double-quotes so long as the string contains a quote that would have to be escaped otherwise
  * allowTemplateLiterals is set to true, this allows strings to use backticks
* [consistent-return](https://eslint.org/docs/rules/consistent-return "Link to consistent-return - Eslint documentation")
  * Requires return statements to either always or never specify values
  * Turned off
#### Import rules:
* [import](https://www.npmjs.com/package/eslint-plugin-import "NPM package page")
* [import/prefer-default-export](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md "Github documentation")
  * When there is only a single export from a module, prefer using default export over named export
  * Turned off
* [import/extensions](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/extensions.md "Github documentation")
  * Provide a consistent use of file extensions
  * Turned off
#### React rules:
* [react/display-name](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/display-name.md "Github documentation")
* [react/no-array-index-key](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-array-index-key.md "Github documentation")
* [react/react-in-jsx-scope](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/react-in-jsx-scope.md "Github documentation")
* [react/prefer-stateless-function](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-stateless-function.md "Github documentation")
* [react/forbid-prop-types](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/forbid-prop-types.md "Github documentation")
* [react/no-unescaped-entities](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-unescaped-entities.md "Github documentation")
* [react/require-default-props](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/require-default-props.md "Github documentation")
* [react/jsx-filename-extension](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-filename-extension.md "Github documentation")
#### React hooks rules:
* [react-hooks/rules-of-hooks](https://reactjs.org/docs/hooks-rules.html#eslint-plugin "React hooks documentation")
  * Checks rules of Hooks
* [react-hooks/exhaustive-deps](https://reactjs.org/docs/hooks-rules.html#eslint-plugin "React hooks documentation")
  * Checks effect dependencies
#### Jsx-a11y rules:
* [jsx-a11y/accessible-emoji](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/accessible-emoji.md "Github documentation")
* [jsx-a11y/href-no-hash](https://www.npmjs.com/package/eslint-plugin-jsx-a11y "NPM package page")
  * This rule seems to be deprecated and if therefor turned off. Anchor is valid has replaced this.
* [jsx-a11y/anchor-is-valid](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/anchor-is-valid.md "Github documentation")
#### Prettier rules:
* [Prettier - trailingComma](https://prettier.io/docs/en/options.html#trailing-commas "Prettier documentation")
* [Prettier - singleQuote](https://prettier.io/docs/en/options.html#quotes "Prettier documentation")
* [Prettier - printWidth](https://prettier.io/docs/en/options.html#print-width "Prettier documentation")
* [Prettier - useTabs](https://prettier.io/docs/en/options.html#tabs "Prettier documentation")

## Links:
[AirBnB - Javascript style guide](https://github.com/airbnb/javascript "Link to AirBnB - Javascript style guide")
[Eslint - Hompage](https://eslint.org/ "Link to Eslint homepage")
[Prettier - Homepage](https://prettier.io/ "Link to Prettier homepage")