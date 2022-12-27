# ESLint with Svelete & Typescript for VS Code

This template should help you with the configuration of ESLint for Svelte & Typescript in VS Code.

It is based on a Vite app for Svelte and Typescript.

## Installation 

To be able to lint your Svelte Typescript code you need: 
 - eslint
 - eslint-plugin-svelte3
 - @typescript-eslint/parser
 - @typescript-eslint/eslint-plugin
 - eslint-config-google _(optional)_

 You can install al of theme with:
 
 ```sh
 npm i --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-plugin-svelte3 eslint-config-google
 ```

## Configuration 

As explained on the [eslint-plugin-svelte3 doc](https://www.npmjs.com/package/eslint-plugin-svelte3#Installation), you first need to configure your `.eslintrc.*` file.

For example: 
```js
module.exports = {
  parserOptions: {
    ecmaVersion: 2019,
    sourceType: 'module'
  },
  env: {
    es6: true,
    browser: true
  },
  parser: '@typescript-eslint/parser',
  plugins: [
    'svelte3',
    '@typescript-eslint'
  ],
  overrides: [
    {
      files: ['*.svelte'],
      processor: 'svelte3/svelte3'
    }
  ],
  rules: {
    // ...
  },
  settings: {
    'svelte3/typescript': () => require('typescript'), // pass the TypeScript package to the Svelte plugin
    // OR
    'svelte3/typescript': true, // load TypeScript as peer dependency
    // ...
  }
};
```

Perfect, you can now run `npx eslint ./src` to know all the lint issues in your Typescript and Svelte files.  
But we can go further and use ESlint VS Code's extension to display all the issues directly in the files.

## ESLint extension 

If we install it, it will display the issues in your Typescript files, but why ?  
Because we did not tell it to check issues in `.svelete` files. 

To do so add the following configuration in your settings.json file: 
```js
{
    // ...
    "eslint.validate": [
        "svelte",
    ],
    // ...
}
```