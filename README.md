# JavaScriptNetlifyFunctions

## Purpose

This is a simple guide to writing and deploying your first Netlify Function using JavaScript and GitHub.

Netlify makes it extremely easy to take advantage of AWS's serverless Lambda functions. They can currently be deployed with JavaScript and Go. If you're interested in the slightly more complicated Go side of this process, head here: [GolangNetlifyFunctions](https://github.com/phoenixcoder/GolangNetlifyFunctions).

## Guide

You will need both a Netlify and a GitHub account before you get started.

### Creating the project

#### Quick steps:

1. Create a new GitHub project named JavaScriptNetlifyFunctions.
1. Open the project locally.
1. Create a `netlify.toml` file in the root directory and copy the contents from the same file in this repository.
1. Create a `/functions` folder.
1. Create a `helloWorld.js` file in the `/functions` folder and copy it's contents from the same file in this repository.
1. Skip to Deploying the project's Quick Steps.

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

Now that the function actually does something, it will return a status code of 200 and "Hello, world!" when it is invoked by hitting this endpoint on your Netlify site:

`https://[something-clever-netlify-made-for-you].netlify.com/.netlify/functions/[function-name]`

Git commit and push your changes to GitHub and we're ready to deploy!

#### Visual Checkpoint

You should now have something similar to:
Folder structure. Toml. helloWorld.

### Deploying the project

#### Quick steps:

1. Sign up for (if necessary) and into Netlify. Signing up with your GitHub account eases things along.
1. From your `Sites` page, click "New site from Git".
1. Choose "GitHub" from the "Continuous Deployment" options.
1. Authorize the Netlify GitHub application.
1. Configuring the Netlify app.
1. Choose whether to allow access to all of your repositories or only those you select.
1. Allow the Netlify app to install.
1. Choose your JavaScriptNetlifyFunctions repository.
1. Ensure that "Branch to deploy" is set to `master` and click "Deploy site"
1. Once "Production deploys" is labeled as `PUBLISHED`, your functions are deployed.

### Details

Sign up for a Netlify account if you haven't already and log in. It is convenient to do so by authenticating through your GitHub account.

After logging in, you should be looking at your list of sites. If you have never deployed to Netlify before, it will probably be blank. You can fix that now by clicking the "New site from Git" button in the upper right.

You should now be presented with the "Create a new site" panel. Click the GitHub icon and you will be asked to authorize the Netlify application on GitHub and a series of other confirmations. Follow along with the images below:

![Authorize Netlify app](../images/01-deploy-authnetlify.png)

![Configure Netlify app](../images/02-deploy-confignetlify.png)

![Install Netlify app](../images/03-deploy-installnetlify.png)

![Choose the repository](../images/04-deploy-chooserepo.png)

![Set deploy branch to master](../images/05-deploy-masterbranch.png)

![Set deploy branch to master](../images/06-deploy-published.png)
