---
Order: 2
Area: langupreferred quote style and path style for imports added to your code with the `javascript.preferences.quoteStyle` and `javascript.preferences.importModuleSpecifier` settings.

## Formatting

VS Code's built-in JavaScript formatter provides basic code formatting with reasonable defaults.

The `javascript.format.*` [settings](/docs/getstarted/settings.md) configure the built-in formatter. Or, if the built-in formatter is getting in the way, set `"javascript.format.enable"` to `false` to disable it.


## Organize Imports

The **Organize Imports** Source Action sorts the imports in a JavaScript file and removes any unused imports:

<!-- TODO: replace with js specific example -->
<video src="images/javascript/organize-imports.mp4" placeholder="images/javascript/organize-imports-placeholder.png" autoplay loop controls muted>
    Sorry, your browser doesn't support HTML 5 video.
</video>

You can run **Organize Imports** from the **Source Action** context menu or with the `kb(editor.action.organizeImports)` keyboard shortcut.

Organize imports can also be done automatically when you save a JavaScript file by setting:

```json
"editor.codeActionsOnSave": {
    "source.organizeImports": "explicit"
}
```

## Code Actions on Save

The `editor.codeActionsOnSave` setting lets you configure a set of Code Actions that are run when a file is saved. For example, you can enable organize imports on save by setting:

```json
// On explicit save, run fixAll source action. On auto save (window or focus change), run organizeImports source action.
"editor.codeActionsOnSave": {
    "source.fixAll": "explicit",
    "source.organizeImports": "always",
}
```

As of today, the following enums are supported:
* `explicit` (default): Triggers Code Actions when explicitly saved. Same as `true`.
* `always`: Triggers Code Actions when explicitly saved and on Auto Saves from window or focus changes.
* `never`: Never triggers Code Actions on save. Same as `false`.

You can also set `editor.codeActionsOnSave` to an array of Code Actions to execute in order.

Here are some source actions:

* `"organizeImports"` -  Enables organize imports on save.
* `"fixAll"` - Auto Fix on Save computes all possible fixes in one round (for all providers including ESLint).
* `"fixAll.eslint"` -  Auto Fix only for ESLint.
* `"addMissingImports"` - Adds all missing imports on save.

See [Node.js/JavaScript](/docs/nodejs/working-with-javascript) for more information.

## Code suggestions

VS Code automatically suggests some common code simplifications such as converting a chain of `.then` calls on a promise to use `async` and `await`

<video src="images/javascript/code-suggestions-convert-async.mp4" placeholder="images/javascript/code-suggestions-convert-async-placeholder.png" autoplay loop controls muted>
    Sorry, your browser doesn't support HTML 5 video.
</video>

Set `"javascript.suggestionActions.enabled"` to `false` to disable suggestions.

## Enhance completions with AI

[GitHub Copilot](https://copilot.github.com/) is an AI-powered code completion tool that helps you write code faster and smarter. You can use the [GitHub Copilot extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) in VS Code to generate code, or to learn from the code it generates.

[![GitHub Copilot extension in the VS Code Marketplace](images/javascript/copilot-extension.png)](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)

GitHub Copilot provides suggestions for numerous languages and a wide variety of frameworks, and it works especially well for Python, JavaScript, TypeScript, Ruby, Go, C# and C++.

You can learn more about how to get started with Copilot in the [Copilot documentation](/docs/editor/github-copilot.md).

Once you have the Copilot extension installed and enabled, you can test it our for your JavaScript projects.

Create a new file - you can use the **File: New File** command in the Command Palette (`kbstyle(F1)`).

In the JavaScript file, type the following function header:

```js
function calculateDaysBetweenDates(begin, end) {
```

Copilot will provide a suggestion like the following - use `kbstyle(Tab)` to accept the suggestion:

![Copilot JavaScript ghost text suggestion](images/javascript/js-suggest.png)

## Inlay hints

Inlay hints add additional inline information to source code to help you understand what the code does.

**Parameter name inlay hints** show the names of parameters in function calls:

![Parameter name inlay hints](images/javascript/inlay-parameters.png)

This can help you understand the meaning of each argument at a glance, which is especially helpful for functions that take Boolean flags or have parameters that are easy to mix up.

To enable parameter name hints, set `javascript.inlayHints.parameterNames`. There are three possible values:

* `none` — Disable parameter inlay hints.
* `literals` — Only show inlay hints for literals (string, number, Boolean).
* `all` — Show inlay hints for all arguments.

**Variable type inlay hints** show the types of variables that don't have explicit type annotations.

Setting: `javascript.inlayHints.variableTypes.enabled`

![Variable type inlay hints](images/javascript/inlay-var-types.png)

**Property type inlay hints** show the type of class properties that don't have an explicit type annotation.

Setting: `javascript.inlayHints.propertyDeclarationTypes.enabled`

![Property type inlay hints](images/javascript/inlay-property-types.png)

**Parameter type hints**  show the types of implicitly typed parameters.

Setting: `javascript.inlayHints.parameterTypes.enabled`

![Parameter type inlay hints](images/javascript/inlay-parameter-types.png)

**Return type inlay hints** show the return types of functions that don't have an explicit type annotation.

Setting: `javascript.inlayHints.functionLikeReturnTypes.enabled`

![Return type inlay hints](images/javascript/inlay-return-type.png)

## References CodeLens

The JavaScript references CodeLens displays an inline count of reference for classes, methods, properties, and exported objects:

![JavaScript references CodeLens](images/javascript/references-codelens.png)

To enable the references CodeLens, set `"javascript.referencesCodeLens.enabled"` to `true`.

Click on the reference count to quickly browse a list of references:

![JavaScript references CodeLens peek](images/javascript/references-codelens-peek.png)

## Update imports on file move

When you move or rename a file that is imported by other files in your JavaScript project, VS Code can automatically update all import paths that reference the moved file:

<video src="images/javascript/update-imports.mp4" placeholder="images/javascript/update-imports-placeholder.png" autoplay loop controls muted>
    Sorry, your browser doesn't support HTML 5 video.
</video>

The `javascript.updateImportsOnFileMove.enabled` setting controls this behavior. Valid settings values are:

* `"prompt"` - The default. Asks if paths should be updated for each file move.
* `"always"` - Always automatically update paths.
* `"never"` - Do not update paths automatically and do not prompt.

## Linters

[Linters](https://en.wikipedia.org/wiki/Lint_%28software%29) provides warnings for suspicious looking code. While VS Code does not include a built-in JavaScript linter, many JavaScript linter [extensions](/docs/editor/extension-marketplace.md) available in the marketplace.

<div class="marketplace-extensions-javascript-linters-curated"></div>

> **Tip:** This list is dynamically queried from the [VS Code Marketplace](https://marketplace.visualstudio.com). Read the description and reviews to decide if the extension is right for you.

## Type checking

You can leverage some of TypeScript's advanced type checking and error reporting functionality in regular JavaScript files too. This is a great way to catch common programming mistakes. These type checks also enable some exciting Quick Fixes for JavaScript, including **Add missing import** and **Add missing property**.

![Using type checking and Quick Fixes in a JavaScript file](images/javascript/checkjs-example.gif)

TypeScript tried to infer types in `.js` files the same way it does in `.ts` files. When types cannot be inferred, they can be specified explicitly with JSDoc comments. You can read more about how TypeScript uses JSDoc for JavaScript type checking in [Working with JavaScript](/docs/nodejs/working-with-javascript.md).

Type checking of JavaScript is optional and opt-in. Existing JavaScript validation tools such as ESLint can be used alongside built-in type checking functionality.

## Debugging

VS Code comes with great debugging support for JavaScript. Set breakpoints, inspect objects, navigate the call stack, and execute code in the Debug Console. See the [Debugging topic](/docs/editor/debugging.md) to learn more.

### Debug client side

You can debug your client-side code using a browser debugger such as our built-in debugger for Edge and Chrome, or the [Debugger for Firefox](https://marketplace.visualstudio.com/items?itemName=hbenl.vscode-firefox-debug).

### Debug server side

Debug Node.js in VS Code using the built-in debugger. Setup is easy and there is a [Node.js debugging tutorial](/docs/nodejs/nodejs-tutorial.md#debug-your-express-app) to help you.

![debug data inspection](images/javascript/debug_data_inspection.gif)

## Popular extensions

VS Code ships with excellent support for JavaScript but you can additionally install debuggers, snippets, linters, and other JavaScript tools through [extensions](/docs/editor/extension-marketplace.md).

<div class="marketplace-extensions-javascript-curated"></div>

> **Tip:** The extensions shown above are dynamically queried. Click on an extension tile above to read the description and reviews to decide which extension is best for you. See more in the [Marketplace](https://marketplace.visualstudio.com).

## Next steps

Read on to find out about:

* [Working with JavaScript](/docs/nodejs/working-with-javascript.md) - More detailed information about VS Code's JavaScript support and how to troubleshoot common issues.
* [jsconfig.json](/docs/languages/jsconfig.md) - Detailed description of the `jsconfig.json` project file.
* [IntelliSense](/docs/editor/intellisense.md) - Learn more about IntelliSense and how to use it effectively for your language.
* [Debugging](/docs/editor/debugging.md) - Learn how to set up debugging for your application.
* [Node.js](/docs/nodejs/nodejs-tutorial.md) - A walkthrough to create an Express Node.js application.
* [TypeScript](/docs/languages/typescript.md) - VS Code has great support for TypeScript, which brings structure and strong typing to your JavaScript code.

## Common questions

### Does VS Code support JSX and React Native?

VS Code supports **JSX** and **React Native**. You will get IntelliSense for **React/JSX** and **React Native** from automatically downloaded type declaration (typings) files from the [npmjs](https://www.npmjs.com) type declaration file repository. Additionally, you can install the popular [React Native extension](https://marketplace.visualstudio.com/items?itemName=vsmobile.vscode-react-native) from  the Marketplace.

To enable ES6 import statements for **React Native**, you need to set the `allowSyntheticDefaultImports` compiler option to `true`. This tells the compiler to create synthetic default members and you get IntelliSense. **React Native** uses **Babel** behind the scenes to create the proper run-time code with default members. If you also want to do debugging of **React Native** code, you can install the [React Native Extension](https://marketplace.visualstudio.com/items?itemName=vsmobile.vscode-react-native).

### Does VS Code support the Dart programming language and the Flutter framework?

Yes, there are VS Code extensions for both [Dart](https://marketplace.visualstudio.com/items?itemName=Dart-Code.dart-code) and [Flutter](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter) development. You can learn more at the [Flutter.dev](https://flutter.dev/docs/development/tools/vs-code) documentation.

### IntelliSense is not working for external libraries

`Automatic Type Acquisition` works for dependencies downloaded by npm (specified in `package.json`), Bower (specified in `bower.json`), and for many of the most common libraries listed in your folder structure (for example `jquery-3.1.1.min.js`).

**ES6 Style imports are not working.**

When you want to use ES6 style imports but some type declaration (typings) files do not yet use ES6 style exports, then set the [TypeScript compiler option](https://www.typescriptlang.org/docs/handbook/compiler-options.html) `allowSyntheticDefaultImports` to true.

```json
{
    "compilerOptions": {
        "module": "CommonJS",
        "target": "ES6",
        // This is the line you want to add
        "allowSyntheticDefaultImports": true
    },
    "exclude": [
        "node_modules",
        "**/node_modules/*"
    ]
}
```

### Can I debug minified/uglified JavaScript?

Yes, you can. You can see this working using JavaScript source maps in the [Node.js Debugging](/docs/nodejs/nodejs-debugging.md) topic.

### How do I disable Syntax Validation when using non-ES6 constructs?

Some users want to use syntax constructs like the proposed pipeline (`|>`) operator. However, these are currently not supported by VS Code's JavaScript language service and are flagged as errors. For users who still want to use these future features, we provide the `javascript.validate.enable` [setting](/docs/getstarted/settings.md).

With `javascript.validate.enable: false`, you disable all built-in syntax checking. If you do this, we recommend that you use a linter like [ESLint](https://eslint.org) to validate your source code.

### Can I use other JavaScript tools like Flow?

Yes, but some of [Flow's](https://flow.org) language features such as type and error checking may interfere with VS Code's built-in JavaScript support. To learn how to disable VS Code's built-in JavaScript support, see [Disable JavaScript support](/docs/nodejs/working-with-javascript.md#disable-javascript-support).
