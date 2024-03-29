# JavaScriptNetlifyFunctions

![](../images/netlifylogo.png)

## Purpose

This is a simple guide to writing and deploying your first Netlify Function using JavaScript and GitHub.

Netlify makes it extremely easy to take advantage of AWS's serverless Lambda functions. They can currently be deployed with JavaScript and Go. If you're interested in the Go side of this process, head here: [GolangNetlifyFunctions](https://github.com/phoenixcoder/GolangNetlifyFunctions).

## Contents

- [Guide](#guide)
  - [Creating the project](#creating-the-project)
    - [Quick steps](#quick-steps)
    - [Details](#details)
    - [Visual Checkpoint](#visual-checkpoint)
  - [Deploying the project](#deploying-the-project)
    - [Quick steps](#quick-steps-1)
    - [Details](#details-1)
  - [Calling a function](#calling-a-function)
    - [Quick steps](#quick-steps-2)
    - [Details](#details-2)
- [Additional Info](#additional-info)
  - [Multiple Functions](#multiple-functions)
  - [Quick note on local function testing](#quick-note-on-local-function-testing)

## Guide

You will need both a Netlify and a GitHub account before you get started.

### Creating the project

#### Quick steps:

1. Create a new GitHub project named JavaScriptNetlifyFunctions.
1. Open the project locally.
1. Create a `netlify.toml` file in the root directory and copy the contents from the same file in this repository.
1. Create a `/functions` folder.
1. Create a `helloWorld.js` file in the `/functions` folder and copy it's contents from the same file in this repository.

- Skip to [Deploying the project's Quick steps](#quick-steps-1).

#### Details

<details>

<summary>Click for more detailed instructions.</summary>

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

Now it will return a status code of 200 and "Hello, world!" when it is invoked by hitting this endpoint on your Netlify site:

`https://[something-clever-netlify-made-for-you].netlify.com/.netlify/functions/helloWorld`

Git commit and push your changes to GitHub and we're ready to deploy!

</details>

#### Visual Checkpoint

You should now have something similar to:

![](../images/01-create-folders.png)
![](../images/02-create-netlify.png)
![](../images/03-create-helloworld.png)

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

- Skip to [Calling a function's Quick steps](#quick-steps-2)

#### Details

<details>

<summary>Click for more detailed instructions.</summary>

Sign up for a Netlify account if you haven't already and log in. It is convenient to do so by authenticating through your GitHub account.

After logging in, you should be looking at your list of sites. If you have never deployed to Netlify before, it will probably be blank. You can fix that now by clicking the "New site from Git" button in the upper right.

You should now be presented with the "Create a new site" panel. Click the GitHub icon and you will be asked to authorize the Netlify application on GitHub and a series of other confirmations. Follow along with the images below:

<img src="../images/01-deploy-authnetlify.png" width="50%" height="50%">

After authorizing and choosing your GitHub account, you should click "Configure Netlify on GitHub":

<img src="../images/02-deploy-confignetlify.png" width="50%" height="50%">

Here, you will be able to choose whether you allow the Netlify app to access to all of your repositories, or only the ones you specifically select. This choice is entirely up to you. If you choose only select repositories, select your JavaScriptNetlifyFunctions repository from the drop down list. Click the "Install" button when you're finished:

<img src="../images/03-deploy-installnetlify.png" width="50%" height="50%">

You will be taken back to Netlify and be able to choose repository. If you allowed access to all repositories, you may want to use the search bar to narrow it down. Otherwise, it should automatically show you the repository you chose:

<img src="../images/04-deploy-chooserepo.png" width="50%" height="50%">

The branch to deploy should already be set to `master`, but ensure that it is. This is the branch Netlify will watch for updates. It will automatically rebuild and deploy your site when you push changes here, so this is important. When you are ready, click "Deploy site." You're almost there:

<img src="../images/05-deploy-masterbranch.png" width="50%" height="50%">

When the site has finished the build and deploy process, you should see this:

<img src="../images/06-deploy-published.png" width="50%" height="50%">

Congratulations! You've now written and deployed a serverless function to Netlify.

</details>

### Calling a function

#### Quick steps:

1. From your site's Overview page, choose `Functions` from the navigation menu.
1. Choose `helloWorld.js` from your list of functions.
1. Copy and paste the `Endpoint` URL and paste it into a browser.
1. Enjoy the fruits of your labor!

#### Details

The "hard" part is over! If you aren't currently on your site's `Overview` page, you can select it from your site list. Along the top navigation you can click `Functions` to see a list of your deployed serverless functions. This is only `helloWorld.js` right now, so click that. You will be presented with an `Endpoint` URL that you can use to invoke your function. Something close to:

`https://[something-clever-netlify-made-for-you].netlify.com/.netlify/functions/helloWorld`

You will see the "Hello, world!" that you returned in your function callback's body, and that's all there is to it.

## Additional Info

### Multiple Functions

Adding multiple functions to your Netlify deployment is as simple as dropping them in your functions folder. This repository provides a `goodbyeWorld.js` companion to the `helloWorld.js` function we walked through earlier, for instance:

`https://[something-clever-netlify-made-for-you].netlify.com/.netlify/functions/goodbyeWorld`

###  Quick note on local function testing

Netlify provides a useful command line tool which you can install globally on your system from the terminal:

`npm install -i netlify-cli`

While the Netlify CLI contains many tools, we will only be concerned with one in this document:

`netlify dev`

When typing this command in your project folder, Netlify will launch a server on `localhost:8888`, allowing you to test your serverless functions without deploying them first:

`http://localhost:8888/.netlify/functions/helloWorld`
`http://localhost:8888/.netlify/functions/goodbyeWorld`

[You can read more about the Netlify CLI here](cli.netlify.com)

_Note that this is only confirmed to work with serverless JavaScript functions. Golang functions require a build step that may require more setup or further development from the Netlify team._

