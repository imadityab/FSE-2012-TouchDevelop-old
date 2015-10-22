![](https://az31353.vo.msecnd.net/c04/gttu.png)

Touch Develop is a touch-friendly, cross-platform, mobile-first app creation environment developed with <3 at Microsoft Research. 
[![Build Status](https://travis-ci.org/Microsoft/TouchDevelop.svg)](https://travis-ci.org/Microsoft/TouchDevelop)

[![App Status](https://www.touchdevelop.com/badges/release/current)](https://www.touchdevelop.com/app)
[![Beta Status](https://www.touchdevelop.com/badges/release/beta)](https://www.touchdevelop.com/app/beta)
[![latest Status](https://www.touchdevelop.com/badges/release/latest)](https://www.touchdevelop.com/app/latest)
[![Cloud Status](https://www.touchdevelop.com/badges/release/cloud)](https://www.touchdevelop.com/)


[![Dependency Status](https://david-dm.org/Microsoft/TouchDevelop.svg)](https://david-dm.org/Microsoft/TouchDevelop)
[![devDependency Status](https://david-dm.org/Microsoft/TouchDevelop/dev-status.svg)](https://david-dm.org/Microsoft/TouchDevelop#info=devDependencies)


**This repo contains the source code of the TouchDevelop editor.** If you are
intending to write Touch Develop scripts, you want to go to
`touchdevelop.com`:
* **stable:** https://www.touchdevelop.com/app/
* **beta:** https://www.touchdevelop.com/app/beta

If you want to always run the latest build,
* **latest:** https://www.touchdevelop.com/app/latest

The make sure which version you're running, tap the small
copyright/legal/version bar in the bottom right, and then the **latest changes**
button. This will give you the changes that went into your current version, and
in particular if the fix for your submitted issue is in.  If the expected
change is not there, try reloading the page. Keep in mind that the build
process takes a few minutes.

Other pages of interest:
* landing page: [https://www.touchdevelop.com](https://www.touchdevelop.com)
* blog: [https://www.touchdevelop.com/blog](https://www.touchdevelop.com/blog)
* Hour Of Code tutorials: [https://www.touchdevelop.com/hoc](https://www.touchdevelop.com/hoc)

## What's in this repo?

The repo is mostly written in [Typescript](http://www.typescriptlang.org/) with tiny pieces
of HTML gluing.

This repo contains the source code for:
* the browser client
 * the compiler
 * the editor
 * the runtime
* the node.js client

However, you will not find the cloud backend code here. Indeed,
[https://www.touchdevelop.com](https://www.touchdevelop.com) takes care of
storing and managing the scripts.

## Contributing

There are many ways to [contribute](https://github.com/Microsoft/TouchDevelop/blob/master/CONTRIBUTING.md) to TouchDevelop.

* [submit bugs](https://github.com/Microsoft/TouchDevelop/issues) and help us verify fixes as they are checked in.
* review the [source code changes](https://github.com/Microsoft/TouchDevelop/pulls)
* [contribute bug fixes or features](https://github.com/Microsoft/TouchDevelop/blob/master/CONTRIBUTING.md).

If you're not a developer but still would like to help, we've got more tasks for you!

* [help translate the user inferface](https://touchdeveloptranslator.azurewebsites.net): do you use TouchDevelop and speak a foreign language? You can help!

## Setup

In order to build TouchDevelop, ensure that you have [Git](http://git-scm.com/downloads) and [Node.js](http://nodejs.org/) installed.

* clone a copy of the repo:

````
git clone https://github.com/Microsoft/TouchDevelop.git
````

* change to the TouchDevelop directory:

````
cd TouchDevelop
````

* install dependencies:

````
npm install jake -g
npm install tsd@next -g
tsd reinstall
npm install
````

### Quick windows setup
These steps install the tools for Windows (+ extras to handle the Arduino compilation scenarios)
* install [Chocolatey](https://chocolatey.org/)
* install nodejs, Visual Studio Code
````
choco install -y nodejs git visualstudiocode arduino python2 pip
````

## Building

There's different ways to build and run TouchDevelop:

* just build:

````
jake
````

You can generate source maps by defining the env variable ``TD_SOURCE_MAPS``

````
export TD_SOURCE_MAPS=1 # optional, will slow down your build
````

* build and run locally:

````
jake local
````

* run packaged as a [nwjs] app:

````
jake nw
````

* run the test suite

````
jake test
````

* cleaning

````
jake clean
````

## Editing

You can use your favorite editor to edit the TypeScript file. Here are a couple tips:

* [Visual Studio Code](https://code.visualstudio.com/), cross platform editor for TypeScript. Simply open the folder in Code.
* Atom: there are a number of packages that will give you TypeScript coloring

## Documentation

All the docs are available online at
[https://www.touchdevelop.com/docs](https://www.touchdevelop.com/docs).

The docs are authored as TouchDevelop scripts in TouchDevelop itself. You can
fork them and send pull requests from TouchDevelop itself to update them.
You can update the local cache of documents by running this command:

    jake update-docs

## More handy commands

Our catch-all tool is `build/client.js`, which is compiled from
`tools/client.ts`. Some of the common invocations of `client.js` are
exposed as Jake targets.

    # assumes TD_UPLOAD_KEY and TD_UPLOAD_USER are set, uploads a new test build
    jake upload

Find out about other commands directly:

    node build/client.js

The `client.js` is built by default.

## The various directories in the tree

* `ast`: contains the lexer, parser, type-checker and ast definitions for the
  TouchDevelop language
* `browser`: feature-detection
* `editor`: the TouchDevelop user interface that drives the website: hub, script
  list, editor itself
* `generated`: files needed for the build that are re-generated manually once in
  a while
* `intellitrain`:
* `json`:
* `lib`: the libraries exposed to TouchDevelop scripts, written in TypeScript
* `libcordova`: Apache Cordova specific implementations
* `libnode`: Node.JS specific implementations
* `libwab`: WebAppBooster implementations, used by the Windows Phone client
* `libwinRT`: (deprecated) WinRT specific implementations
* `mc`: Minecraft bindings
* `noderunner`: runs in the cloud, and parses TouchDevelop scripts / compiles
  them by responding to requests on `/api`.
* `node-webkit`: configuration files for the node-webkit app creation
* `officemix`: office mix app host
* `rt`: various run-time support libraries for the TouchDevelop application:
  in-browser storage, cloud connection, promises, DOM utilities...
* `runner`: the run-time system for *generated* TouchDevelop apps; that is, once
  a TouchDevelop script is packaged as an app (webapp, cordova app, etc.),
  `runner.js` is the runtime system and the stub is in `webapp`
* `shell`: shell app used by Azure and node-webkit; basically a way to serve
  files locally
* `storage`: code for syncing your locally-stored scripts and the cloud storage,
  in the TouchDevelop application
* `tools`: internal tools that are part of the build (pre-processing)
* `webapp`: the stub file that is used to generate the HTML5 Web App when
  exporting a script
* `www`: the base files that make up the TouchDevelop website (html and css)

### Structure of the generated website / app

When packaged, as the website or as an app, the directory structure is flat.
That is, the CSS and HTML files from `www/` as well as the generated `.js` files
from `build/` all end up in the same directory. That way, `index.html` can refer
to `main.js` without worrying.

When running locally (via `jake local`), the local node server knows where to find
the right files to give the illusion that all files are in the `/editor/local/`
directory of the web server.

## LICENSE

The MIT License (MIT)

Copyright (c) 2015 Microsoft

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## 3rd Party Notices

- Font Awesome by Dave Gandy http://fontawesome.io

***
# TouchDevelop
App Development on Mobile Devices
***
This repository contains information related to the tool TouchDevelop presented at Foundations of Software Engineering, 2012. The tool was originally presented in [this paper](http://dl.acm.org/citation.cfm?id=2393641).

This repository _is not_ the original repository for this tool. Here are some links to the original project:
* [The Official Project Page](https://www.touchdevelop.com/)
* [Original Github Repo](https://github.com/Microsoft/TouchDevelop)

In this repository, for TouchDevelop you will find:
* :white_check_mark: Source code

This repository was constructed by [Aditya](https://github.com/imadityab) under the supervision of [Emerson Murphy-Hill](https://github.com/CaptainEmerson).
