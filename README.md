## Problem Description
Project created with @vant/cli 2.x, how to manage installation with pnpm and work properly?

## Steps

````
npx create-vant-cli-app

use vue2 create project && cd project

pnpm install --shamefully-hoist=true
````

## Error location
````
> if (event.data?.type !== 'replacePath') {
| return;
| }

````

## Reason for guessing

Optional chaining operator (?.) not working properly
So the problem is between vue-loader, babel-loader and webpack.

I started trying to modify @vant/cli 2.x

### Regex error caused by directory mapping?
````
// lib/config/webpack.base.js
{
    test: /\.(js|ts|jsx|tsx)$/,
    // exclude: /node_modules\/(?!(@vant\/cli))/,
    use: [CACHE_LOADER, 'babel-loader'],
},
````
It didn't work properly.

### Not using @babel/preset-env normally?
````
// lib/config/babel.config.js
[
    // '@babel/preset-env',
    require.resolve('@babel/preset-env'),
    {
        loose: true,
        modules: useESModules ? false : 'commonjs',
    },
],
````
It still didn't work properly.

I'm not familiar with these workflows, how can I migrate to pnpm like @vant/cli version 3.x?
Thank you very much for taking the time to read it and try to deal with it, or provide some more effective ideas.


### Related tool documentation
* [@vant/cli 2.x](https://github.com/youzan/vant/tree/2.x/packages/vant-cli)
* [pnpm install --shamefully-hoist](https://pnpm.io/zh/cli/install#--shamefully-hoist)

### REFERENCE ISSUES
* [vue-cli issues](https://github.com/vuejs/vue-cli/issues/2703)
* [pnpm issues](https://github.com/pnpm/pnpm/issues/831)
* [pnpm issues](https://github.com/pnpm/pnpm/issues/801)
