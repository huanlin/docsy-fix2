---
title: Readme
linkTitle: _README_
weight: 1
---

This project is derived from the official [Docsy Example](https://github.com/google/docsy-example) repository, and it can be used as a template as well.

## What is a Standalone version, and why?

*Standalone* means this project does not require additional HTTP connections for pulling dependencies from GitHub. For example, bootstrap, FontAwesome and Docsy. This can be useful in a highly secured private network where HTTP connections to GitHub or GitLab are banned. Despite corporates having their own Nexus server, Docsy still needs to pull some dependencies from GitHub. If the Internet connection is blocked, you might encounter the following errors while running `hugo server` command:

```console
error: unable to access http://github.com/FortAwesome/Font-Awesome...
error: unable to access http://github.com/google/docsy...
```

That was the situation I had struggled with. So I created this standalone (or local) version for myself. 

## How to use this project?

First, download this repo as a ZIP file and extract it to your local folder, say `d:/work/docsy-example-standalone`. Usually, you will not `git clone` this repo because the network environment does not allow any `git` requests to GitHub, and I think that's why you're here.

Then run `npm install` to see if everything is up-to-date, i.e. no error and nothing needs to download.

```
cd d:/work/docsy-example-standalone
npm install
```

The result should look like this:

```console
added 210 packages, and audited 211 packages in 9s

52 packages are looking for funding
  run `npm fund` for details

1 moderate severity vulnerability

To address all issues, run:
  npm audit fix

Run `npm audit` for details.
npm notice
npm notice New major version of npm available! 9.8.1 -> 10.3.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v10.3.0
npm notice Run npm install -g npm@10.3.0 to update!
npm notice
```

Then run `npm audit fix` as it suggested. The output will look like below:

```console
changed 2 packages, and audited 211 packages in 1s

52 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

Now run `hugo server` command to build and run the website:

```
hugo server
```

You should see something like this:

```console
Start building sites …
hugo v0.115.3-5c2e014a5150553a9fa4f9c1eb7dc4db89c0f1ab+extended windows/amd64 BuildDate=2023-07-13T16:11:34Z VendorInfo=gohugoio

                   | FA | NO | EN
-------------------+----+----+-----
  Pages            | 26 | 94 | 73
  Paginator pages  |  0 |  0 |  0
  Non-page files   |  3 |  1 |  3
  Static files     | 30 | 30 | 30
  Processed images | 10 |  2 |  9
  Aliases          |  3 |  0 |  3
  Sitemaps         |  2 |  1 |  1
  Cleaned          |  0 |  0 |  0

Built in 1708 ms
Watching for changes in d:\Work\docsy-example-standalone\{assets,content,layouts,package.json,themes}
Watching for config changes in d:\Work\docsy-example-standalone\hugo.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at //localhost:1313/ (bind address 127.0.0.1)
```

That means success. Your website is now running locally.

> If the first line is `hugo: downloading modules` instead of `Start building sites`, that means something wrong in the configuration files and Hugo is still trying to download dependencies from GitHub, which shouldn't happen.

## How this project is built?

> You don't need to read this section. They are just my notes.

This project is built with the following steps:

1. Copy from the official Docsy Example repository, then clone it into a local directory, e.g. `d:/work/docsy-example-standlone`. Let's call it the work folder.
2. From the work folder, run `npm install`, remove `node_modules/` from `.gitignore`, then commit and push to GitHub. Without `node_modules` committed to the repo, it won't work in my work environment.
3. Create a `themes` folder under the work folder.
4. Download [Docsy](https://github.com/google/docsy) as a ZIP file, and extract files to `themes/docsy` folder. Git commit and push.
5. Download [bootstrap](https://github.com/twbs/bootstrap) as a ZIP file, and extract files to `themes/twbs/bootstrap` folder. Git commit and push.
6. Download [FortAwesome/Font-Awesome](https://github.com/FortAwesome/Font-Awesome) as a ZIP file (Font-Awesome-6.x.zip), and extract files to `themes/FortAwesome/Font-Awesome` folder. Git commit and push. 
 
As you can see, all dependencies are committed to the repo on GitHub.

Now open `hugo.toml` with a text editor, and find the following text:

```toml
  [[module.imports]]
    path = "github.com/google/docsy"
    disable = false
```

Replace them with:

```toml
  [[module.imports]]
    path = "docsy"
    disable = false
```

Then open `themes/docsy/hugo.yaml`, find the following sections:

```toml
[[module.imports]]
  path = "github.com/twbs/bootstrap"
  disable = false
  ignoreConfig = true
[[module.imports]]
  path = "github.com/FortAwesome/Font-Awesome"
  disable = false
```

Replace them with:

```toml
[[module.imports]]
  path = "twbs/bootstrap"
  disable = false
  ignoreConfig = true
[[module.imports]]
  path = "FortAwesome/Font-Awesome"
  disable = false
```

That's it.

You can find out more about how to install Hugo for your environment in the official [Getting started](https://www.docsy.dev/docs/getting-started/#prerequisites-and-installation) guide.

Update: see [update-docsy-v0.10.0](update-docsy-v0.10.0)

