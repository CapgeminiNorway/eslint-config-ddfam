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

#### Set up the rules:
Create a `.eslintrc` file in the root folder of your project and add the folowing ruleset:<br/>
[Eslintrc fil](https://github.com/CapgeminiNorway/eslint-config-ddfam/blob/master/.eslintrc "CapgeminiNorway - Eslintrc fil")


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