Please follow the below instructions to update node in your machine:

Windows
Update npm
npm install npm@latest -g
Clear npm cache
npm cache clean -f
Install n
npm install -g n
Update node to latest version
n latest
Mac
With Homebrew
brew update
brew upgrade node
Install and Update yarn
Please follow the below instructions to install or update yarn in your machine.

On Windows
Install yarn
npm install -g yarn
Update yarn
yarn set version latest
On Mac
Install yarn
brew install yarn
Update yarn
brew update
brew upgrade yarn
VS Code Editor Setup
In order to follow along the tutorial series, I recommend you to use Visual Studio Code Editor and install & apply the below extensions and settings.

Extensions
Install the below extensions:

ESLint
Prettier
Path Autocomplete
Settings
Go to your Visual Stuido Code settings.json file and add the below settings there:

// config related to code formatting
"editor.defaultFormatter": "esbenp.prettier-vscode",
"editor.formatOnSave": true,
"[javascript]": {
  "editor.formatOnSave": false,
  "editor.defaultFormatter": null
},
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true,
  "source.organizeImports": true
},
"eslint.alwaysShowStatus": true
Set Line Breaks
Make sure in your VS Code Editor, "LF" is selected as line feed instead of CRLF (Carriage return and line feed). To do that, just click LF/CRLF in bottom right corner of editor, click it and change it to "LF". If you dont do that, you will get errors in my setup.

Line Feed

Linting Setup
In order to lint and format your code automatically according to popular airbnb style guide, I recommend you to follow the instructions as described in video. References are as below.

Install Dev Dependencies
yarn add -D eslint prettier
npx install-peerdeps --dev eslint-config-airbnb-base
yarn add -D eslint-config-prettier eslint-plugin-prettier
Setup Linting Configuration file
Create a .eslintrc.json file in the project root and enter the below contents:

{
  "extends": ["prettier", "airbnb-base"],
  "parserOptions": {
    "ecmaVersion": 12
  },
  "env": {
    "commonjs": true,
    "node": true
  },
  "rules": {
    "no-console": 0,
    "indent": 0,
    "linebreak-style": 0,
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 100,
        "tabWidth": 4,
        "semi": true
      }
    ]
  },
  "plugins": ["prettier"]
}
