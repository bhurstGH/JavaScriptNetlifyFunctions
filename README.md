# JavaScriptNetlifyFunctions

## Purpose

This is a simple guide to writing and deploying your first Netlify Function using JavaScript.

Netlify makes it extremely easy to take advantage of AWS's serverless Lambda functions. They can currently be deployed with JavaScript and Go. If you're interested in the slightly more complicated Go side of this process, head here: [GolangNetlifyFunctions](https://github.com/phoenixcoder/GolangNetlifyFunctions).

## Deploying functions...

You will need both a Netlify and a GitHub account before you get started.

### Creating the project

#### Quick steps:

1. Create a new GitHub project named JavaScriptNetlifyFunctions.
1. Open the project locally.
1. Create a `netlify.toml` file in the root directory and copy the contents from the same file in this repository.
1. Create a `/functions` folder.
1. Create a `helloWorld.js` file in the `/functions` folder and copy it's contents from the same file in this repository.
1. Skip to Deploying the project.

#### Details

Begin by creating a new GitHub repository, which you will eventually deploy. Feel free to name it JavaScriptNetlifyFunctions or anything else you would like. Once you have cloned the repository to your local machine, navigate to that directory and open it in your favorite editor. Assuming you are using VS Code, you can open the project folder by typing this in your terminal:

`code .`

The next step is to create a `netlify.toml` file in the root directory of your project. This file will instruct Netlify on which directory your Lambda functions will be stored in. Open the file in your editor and add:

```
[build]
functions = "./functions"
```

Now you need to create the folder that the `netlify.toml` points to, so create `/functions` in your project directory. Once this is done, create and open a classic `helloWorld.js` file. This is where you will actually write your function:

```
exports.handler = function (event, context, callback) {
    // Do cool stuff here
}
```

It doesn't do much right now but this is the basic scaffolding of a serverless function. The `handler()` function will be exported and will receive the `event` and `context` parameters from Netlify when it is called. Let's take advantage of the `callback` and update it so that it actually does something:

```
exports.handler = function (event, context, callback) {
    callback(null, {
        statusCode: 200,
        body: "Hello, world!"
    })
}
```
