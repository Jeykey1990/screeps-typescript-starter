# screeps-starter

> Starter kit for [TypeScript](http://www.typescriptlang.org/)-based [Screeps](https://screeps.com/) AI codes.

This starter kit is a modified version of the original [Screeps/TypeScript sample project](https://github.com/MarkoSulamagi/Screeps-typescript-sample-project) by [Marko Sulamägi](https://github.com/MarkoSulamagi).

## Notice

This repository recently transitioned to TypeScript 2, complete with all sorts of new features, including strict `null` checks, as well as the ability to flatten your code with Webpack. Those who still wish to use TS1 should checkout the [`ts1-legacy`](https://github.com/screepers/screeps-typescript-starter/tree/ts1-legacy) branch. Any notable changes in `master` may be backported into the legacy branch.

To learn more about TypeScript 2, [click here](https://blogs.msdn.microsoft.com/typescript/2016/07/11/announcing-typescript-2-0-beta/).

## Getting Started

### Requirements

* [Node.js](https://nodejs.org/en/) (v4.0.0+)
* Gulp 4.0+ - `sudo npm install -g gulpjs/gulp.git#4.0`

### Quick setup

First, you will have to set up your config files. Create a copy of `config.example.json` and rename it to `config.json`. Then navigate into the `src/config` directory, reate a copy of `config.example.ts` and rename it to `config.ts`.

```bash
# config.json
$ cp config.example.json config.json

# config.ts
$ cd src/config
$ cp config.example.ts config.ts
```

Then, on the `config.json` file, change the `username` and `password` properties with your Screeps credentials.

The `config.json` file is where you set up your development environment. If you want to push your code to another branch, for example, if you have some sort of a staging branch where you test around in Simulation mode, we have left a `branch` option for you to easily change the target branch of the upload process. The `default` branch is set as the default.

The `src/config/config.ts` file is where you store your code-specific config variables. For example, if you want to easily turn on `PathFinder` when needed, you can set your own variable here. Once you've set up your configs, import the `config.ts` file on the file you want to call these configs at:

```js
import * as Config from "../path/to/config";
```

Then simply call the config variables with `Config.CONFIG_VARIABLE`.

**WARNING: DO NOT** commit these files into your repository!

### Installing npm modules

Then run the following the command to install the required npm packages and TypeScript type definitions.

```bash
$ npm install
```

### Running the compiler

```bash
# To compile your TypeScript files on the fly
$ npm start

# To deploy the code to Screeps
$ npm run deploy
```

You can also use `deploy-prod` instead of `deploy` for a bundled version of the project, which has better performance but is harder to debug.

## Notes

### Sample code

This starter kit includes a bit of sample code, which uses some of the new TS2 features mentioned earlier. Feel free to build upon this as you please, but if you don't want to use them, you can remove everything from within the `src/` directory and start from scratch.

When starting from scratch, make sure a `main.ts` file exists with a `loop()` function. This is necessary in order to run the game loop.

**Source:** http://support.screeps.com/hc/en-us/articles/204825672-New-main-loop-architecture

### The `noImplicitAny` compiler flag

TypeScript developers disagree about whether the `noImplicitAny` flag should be `true` or `false`. There is no correct answer and you can change the flag later. But your choice now can make a difference in larger projects so it merits discussion.

When the `noImplicitAny` flag is `false` (the default), the compiler silently defaults the type of a variable to `any` if it cannot infer the type based on how the variable is used.

When the `noImplicitAny` flag is `true` and the TypeScript compiler cannot infer the type, it still generates the JavaScript files. But it also reports an error. Many seasoned developers prefer this stricter setting because type checking catches more unintentional errors at compile time.

In this starter kit, the `noImplicitAny` is set to `true` for a more stricter environment. If you don't like this, you can change the `noImplicitAny` flag to `false` on the `tsconfig.json` file.

**Source:** https://angular.io/docs/ts/latest/guide/typescript-configuration.html


### TSLint

TSLint checks your TypeScript code for readability, maintainability, and functionality errors, and can also enforce coding style standards.

After each successful compiling of the project, TSLint will parse the TypeScript source files and display a warning for any issues it will find.

This project provides TSLint rules through a `tslint.json` file, which extends the recommended set of rules from TSLint github repository: https://github.com/palantir/tslint/blob/next/src/configs/recommended.ts

We made some changes to those rules, which we considered necessary and/or relevant to a proper Screeps project:

 - set the [forin](http://palantir.github.io/tslint/rules/forin/) rule to `false`, it was forcing `for ( ... in ...)` loops to check if object members were not coming from the class prototype.
 - set the [interface-name](http://palantir.github.io/tslint/rules/interface-name/) rule to `false`, in order to allow interfaces that are not prefixed with `I`.
 - set the [no-console](http://palantir.github.io/tslint/rules/no-console/) rule to `false`, in order to allow using `console`.
 - in the [variable-name](http://palantir.github.io/tslint/rules/variable-name/) rule, added `allow-leading-underscore`.

If you believe that some rules should not apply to a part of your code, you can use flags to let TSLint know about it: https://palantir.github.io/tslint/usage/rule-flags/

**More info about TSLint:** https://palantir.github.io/tslint/


## Contributing

1. [Fork it](https://github.com/screepers/screeps-typescript-starter/fork)
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Create a new Pull Request

## Special thanks

[Marko Sulamägi](https://github.com/MarkoSulamagi), for the original [Screeps/TypeScript sample project](https://github.com/MarkoSulamagi/Screeps-typescript-sample-project).
