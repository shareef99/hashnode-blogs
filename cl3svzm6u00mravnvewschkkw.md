## How to publish a CLI tool on NPM

**Hello Developers 🙌🙌🙌**

Recently I wanted to create a CLI tool, but I only know JavaScript, so I researched and found out that we can create CLI applications using JavaScript. I published my CLI tool named _track-task_ and will show you how to publish a package in NPM. You can download and use it.

```npm
npm i -g track-task
```

### How to publish NPM package?

**Step 1:-** Initialize _npm_ by `npm init -y`
It will create a default package.json file, which will look something like

```json
{
  "name": "track-task",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

Points to note here

- Name should be unique, otherwise it will throw error while publishing.
- Start with version 1.0.0 and remember to update to version whenever you make changes to your code.
- Add a bin as `" bin "./index.js"` from this point your code will run.
- Add keywords and author name to stand out.

**Step 2:-** Code your application.
Code your whole application and test it out locally and make sure to add `#! /usr/bin/env node`, it makes your file executable.

**Step 3:-** Add more info to package.json.
Add repository, bugs and homepage urls
```json
{
  ...
  "repository": {
    "type": "git",
    "url": "git+https://github.com/shareef99/task-tracker.git"
  },
  "bugs": {
    "url": "https://github.com/shareef99/task-tracker/issues"
  },
  "homepage": "https://github.com/shareef99/task-tracker/#readme",
}
```

**Step 4:-** Publishing your CLI tool

- Create _npm account_.
- Login into npm account from terminal.
```npm
npm login
```
- Enter the username and password.
- Make sure you are ready to publish.
- Publish your package.
```npm
npm publish
```

**_Congratulations ✨✨✨ You have published the npm package._**

**Step 5:-** Updating package.
Don't forget to change the version of in package.json file after update your code. Once you are done with the coding, run `npm publish`.

**Thanks and Happy Coding**

Closing here 👋👋👋

> This is **Shareef**.
> My [Portfolio](https://portfolio.shareef.vercel.app/)
> Twitter [ShareefBhai99](https://twitter.com/shareefBhai99)
> [Linkedin](https://www.linkedin.com/in/nadeem-shareef-7a8394182/)
> My [other Blogs](https://dev.to/shareef)