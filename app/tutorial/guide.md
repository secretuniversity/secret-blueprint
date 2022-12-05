# Secret Blueprint Box Tutorial 

## Introduction

This box comes with everything you need to create your own Secret Box. 

### Setting Up Your Environment

If you haven't already launched this box in a Gitpod workspace, or setup your local environment, follow the "Getting Started" steps [here](https://github.com/secretuniversity/secret-blueprint-box/blob/main/README.md).

At this point your _Secret Blueprint Box_ workspace should be setup and includes: 

* a running `LocalSecret` blockchain instance
* an initial version of the _Secret Counter_ contract has been uploaded to `LocalSecret`
* and _Secret Blueprint App_ has been launched, which includes this tutorial

You should have the following three terminal windows open in your local environment:

1. `LocalSecret` - the first terminal shows the blockchain starting up and producing blocks
2. `Secret Box Workspace` - the 2nd terminal is where your contract gets compiled, deployed, and is the window you'll use to enter commands as you go through this tutorial
3. `Secret Box Frontend` - the 3rd terminal is where your application server is launched, after `LocalSecret` is running and the _Secret Counter_ contract has been created

**Gitpod Workspace Configuration**

If you've launched this box in [Gitpod](https://gitpod.io/docs), your workspace should look like this: 

![](https://i.imgur.com/TOZWYbb.png)

_Gitpod Workspace Configuration_

The `.gitpod.yml` (in the project root directory) has definitions for tasks and prebuild information 
that define how the Secret Box is configured and launched.

During the prebuild phase, Gitpod installs all of the project dependencies including pulling the necessary docker
images used for `LocalSecret` and the contract optimizer (see the `Makefile`). 

There are additional Gitpod `yml` configurations for:

- `.gitpod.yml.localsecret` - launches the `LocalSecret` blockchain on workspace startup
- `.gitpod.yml.secretbox` (the default) - automates the entire process for the secret box, including compiling/deploying/creating the contract, running unit tests, and finally launching the frontend DApp
- `.gitpod.yml.simple` - this configuration installs all the required dependencies, but doesn't start `LocalSecret` or launch the frontend

When the workspace is launched using the full automated configuration (the default), `LocalSecret` is started, shown in the first terminal window. In the second terminal window, the script that uploads and instantiates the secret contract is kicked off. Finally, the frontend app is opened in a [VS Code](https://code.visualstudio.com/) browser preview window.

To open the Secret Box in an external browser, open a new terminal window within the 
workspace and enter the following Gitpod CLI command.

```
gp preview $(gp url 5173) --external
```

NOTE: the _Vite_ server is configured to listen to port 5173 for requests.


## Getting Started

Aside from making your contract and app-specific changes to the template code, you'll want to update the following:

 1. `Cargo.toml` - `cargo` configuration and contract dependencies
<br/>

 2. `README.md` - information including how to run it locally (you can use the `docs/` directory for additional guides, diagrams or other images needed to document your Secret Box). 
<br/>

 3. `examples/schema.rs` - update with the name of your secret contract
<br/>

 4. `tests/secretbox.ts` - integration tests for your Secret Box
<br/>

 5. `app/tutorial/` - write your guide in `guide.md` and include any images in `illustrations/`
<br/>

 6. `app/` - make your Secret Box frontend changes here
 <br/>

 7. `docs/setting-up-your-environment` - to make it more specific to your _Secret Box_ (this guide contains instructions to work with a box in a local developer environment)
 <br/>


See the following steps for more details on the changes you'll want to make. Feel free to make any needed modifications to make this Secret Box your own :tada:.

### Cargo Configuration
 - Make sure to modify the `Cargo.toml` file so it has the correct Secret Box name, author, description, etc.
    
    ``` 
    [package]
    name = "secret-blueprint-box"
    version = "0.1.0"
    authors = ["laura <laura@secretchaingirl.io>"]
    edition = "2021"
    description = "A secret box blueprint for creating your own"
    license = "MIT" 
    ```
 - And define the secret contract dependencies needed by your Secret Box
    
    ``` 
    [dependencies]
    cosmwasm-std = { package = "secret-cosmwasm-std", version = "1.0.0" }
    cosmwasm-storage = { package = "secret-cosmwasm-storage", version = "1.0.0" }
    schemars = "0.8.1"
    serde = { version = "1.0.114", default-features = false, features = ["derive"] }
    thiserror = { version = "1.0" }
    
    # [dev-dependencies]
    cosmwasm-schema = "1.0.0"
    ```

    
### README

 - Modify the "Open in Gitpod" link so that it references your Secret Box repository name/location

```
https://gitpod.io/#https://github.com/secretuniversity/secret-blueprint-box
```

 - Update it so that it's specific to your Secret Box.
 
The README is meant to be used in a local developer environment. Include instructions on setting up and running your Secret Box. Consider including anything you think will help [Secret University](https://scrt.university) list your secret box, upon review and approval by the core team. Based on your judgement, you might have images and even diagrams (e.g. UML), design descriptions--basically the key things you think will be helpful for Secret Network developers in learning from and using your Secret Box.

### Schema

- Modify `examples/schema.rs` and change the secret contract name so that it matches `Cargo.toml`

```
use secret_blueprint_box::msg::{CountResponse, ExecuteMsg, InstantiateMsg, QueryMsg};
use secret_blueprint_box::state::State;
```

### Integration Tests

- After completing your secret contract and unit test code, modify the `secretbox.ts` as needed. These are super helpful for illustrating how to interact with a Secret App such as connecting to the network, querying and executing transactions, etc.


## Tutorial
This is where you'll write the guide for your Secret Box. Under the `app/tutorial/` directory you'll find a starting guide (this file :tada:) in `guide.md`.

- revise this guide as needed
- store images used in your guide in the `app/tutorial/illustrations` directory for your reference
- use https://imgur.com or another image hosting platform to store your images and then reference them in your guide as: `![](URL of image)`
 
### Writing Your Guide

One thing to consider when writing your guide is to determine what blueprint code your Secret Box should have and what will be given in the tutorial for developers to add/modify manually.

In this scenario, consider creating a `solutions/` or similar directory that developers can refer to while learning.  It's also entirely possble, and acceptable, that your code is complete and the tutorial steps walk the developer through the key aspects and code snippets you decide to include!

This is an excellent example of a code walkthrough that is more inline with the above approach: [Millionaire's Problem Breakdown](https://docs.scrt.network/secret-network-documentation/development/getting-started/millionaires-problem-breakdown-extra-credit).

## Secret Box Frontend
This is where all of your frontend code goes, under the `app/` directory and is setup as a [Vite](https://vitejs.dev/guide/)  project using the [Vue](https://vuejs.org/) framework and [Typescript](https://www.typescriptlang.org/) programming language.

*Vite* is a fast, lean build tool that lets you work with a number of frameworks (e.g. *vue, react, svelte*) and either *Javascript* or *Typescript*.

If you want to use other frameworks and languages, feel free to completely revamp the frontend code, the `README.md` and `package.json` to fit your Secret Box needs.

After adding your code:

1. Use `src/assets/logo.png` in your `src/App.vue`, which is the Secret Box logo, somewhere within the header of your application
<br/>

2. Add any box images needed as part of your guide to the `illustrations/` directory. For example, listing unit-test results in a tutorial step
<br/>

3. Change the name of your Secret Box app in `package.json`
<br/>

4. Change the `<title>` element in `index.html` to the name of your Secret Box
<br/>

5. Put any images referenced in your modified `index.html` in the `public/` directory
<br/>

6. Modify the SecretBox Vue element in `App.vue`
<br/>

7. Images for your Secret Box frontend go in `src/assets`
<br/>

8. Create your frontend SecretBox component in `src/components/SecretBox.vue`
<br/>


### UI/UX
If you're able to create and implement your own Secret Box UI/UX that's great. Secret Boxes are meant to have beautiful, intuitive and easy to use interfaces.

If you're not that kind of developer (quite common!) and don't have the UI/UX expertise to create a polished user interface, we ask that you create a wireframe in the form of a diagram or a simple text-based description of the elements required by your box and any other notes that would be helpful. Reach out to us via the "Submit a Ticket" form with your wireframe and/or notes, after submitting your _Secret Box_ for approval. Our team will work with you to create a design based on your vision.

We look forward to seeing what Secret Box you will create for the Secret Network developer community :tada:.
