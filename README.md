
# SiteVision Front End Boilerplate

Node, Gulp, Sass, Autoprefixer, minification, 
image optimization and embedding and more. 

*Created by Henrik Ekelöf at Bouvet Örebro in 2016.*


## Content

- [Why use this?](#why-use-this)
- [What's in the box](#whats-in-the-box)
- [Set up a new project](#set-up-a-new-project)
   - [GitHub Repo](#github-repo)
   - [Add the boilerplate](#add-the-boilerplate)
   - [Edit project files](#edit-project-files)
   - [SiteVision project site setup](#sitevision-project-site-setup)
- [How to use](#how-to-use)
   - [Gulp](#gulp)
      - [Gulp Watch](#gulp-watch)
      - [Gulp Build](#gulp-build)
   - [Git](#git)
   - [Optimized images](#optimized-images)
   - [Embedded images](#embedded-images)
   - [Async font-face](#async-font-face)
   - [Sass](#sass) 


## Why use this?

I wanted a skeleton project for the frontend stuff I use in almost all of my web projects to get started faster and to get the setup right with less effort every time. This boilerplate does that for me. Feel free to use it as you wish in your projects!

The boilerplate is created with SiteVision projects in mind but will probably work for any CMS. I will add setup for other CMSs in case I use this in other systems. 

My setup is:

- Development on OS X using IntelliJ IDEA, Web- or PhpStorm
- SiteVision CMS running on remote server
- Source code repo on GitHub
- Local webserver (using gulp-connect) to serve JS and CSS during development
- "Deploy" by building and pushing to GitHub Pages. The site will use the files at GitHub as a demo version during development. When the project is finished I will upload the files to the server.
  

## What's in the box

- [Gulp](http://gulpjs.com/) tasks.
- [Sass](http://sass-lang.com/).
- [Autoprefixer](https://github.com/postcss/autoprefixer).
- CSS minification.
- [Optimization of image assets](https://github.com/sindresorhus/gulp-imagemin).
- Images embedded (Base64 encoded) in CSS on demand.
- Script concatention and minification.
- Setup for async loading of font-face fonts embedded in separate CSS.
- Custom [Lodash](https://lodash.com/) builds based on usage in JS-files available.
- JSHint on build, .jshintrc for use by IDE.
- JSCS on build, .jscsrc for use by IDE. Uses customized version of [jQuery JS Style Guide](https://contribute.jquery.org/style-guide/js/)
- Serving assets from localhost
- Instructions and velocity script for including files in SiteVision (head)
- Bookmarklet to toggle dev- and production (or demo) mode


## Set up a new project

### GitHub Repo

- Create a new GitHub repository for the project
- Create branch `gh-pages`
- Delete master
- Clone repo to your computer

### Add the boilerplate

- Clone (or update) Boilerplate repo
- Copy files to new project repo

### Edit project files

- Edit package.json (Name, description, GitHub URLs)
- Edit _config.yml (set project name)
- Run `$ npm install`

### SiteVision project site setup

- Copy content from additional-head-elements.vm to SiteVision as an "Additional HEAD element" with Velocity type.
- Add metadata (as links): assetJsMain, assetCssMain, assetCssFonts (optional)

Now you can build the site and deploy so you get your asset URLs. Point metadata in SiteVision to URLs on GitHub Pages.


## How to use

As you work on your web project you will "deploy" by pushing code to GitHub Pages. Everytime you do that, the site will be updated with your newest code for the customer to look at and test.

When you write the code you will serve your JS and CSS from a local webserver (started by Gulp). You need to tell SiteVision to fetch from your localhost instead of from GitHub. You do that by passing a URL parameter: `?devmode=true`.


### Gulp

#### Gulp Watch

`$ gulp watch` or `$ gulp`

- Start local webserver
- Watch `_js` and `_sass` folders for changes
- Build and concatenate JS on change
- Compile Sass to CSS on change

Default URLs for local files:

- http://localhost:8080/main.js
- http://localhost:8080/main.css

#### Gulp Build

`$ gulp build`

- Run JSHint and JSCS to check scripts
- Build, concatenate and minify JS
- Optimize images
- Compile Sass and minify the CSS

`$ gulp build --rev`

- Same as `$ gulp build` but will add a timestamp to the file name.


### Git

I always forget how to Git from the command line. These are the commands I will use 99.9 % of the time:

- `$ git status`
- `$ git commit -a`
- `$ git pull --rebase`
- `$ git push`

After a `$ gulp build` I will do the commands above in order, and that will push my changes to GitHub and my website will be updated for the customer.

### Optimized images

All image assets in `_assets` folder will be optimized on build. It's a lossless optimization, but you might still want to keep another copy of the image file elsewhere.


### Embedded images

By using the function data-uri in your Sass code you may choose to embed an image in your CSS, Base64 encoded. 

`background-image: data-uri( "foo.svg" )`


### Async font-face

This is my prefered way of including font-face fonts. The advantage is that there will never be a blank screen while your fonts are loading. The fallback font will be visible first (on first page load only), then switched to the font-face font. With a good fallback, this will be quite invisible. On following requests, the font-face font will be stored in localStorage and applied immediately in head, so there will be no request at all.

A script checks the script tag (`#js-main`) for an URL to a CSS file. The file is fetched asynchronously (AJAX) and stored in localStorage. On the next request we check if there is a file in localStorage and skip the request. The CSS file will have the font-face font embeded as Base64.

- fonts.css must be uploaded to the SiteVision server. It is fetched with AJAX so it must be on the same domain as the visited page.


### Sass 

The folder structure is using [the 7-1 architecture pattern](http://sass-guidelin.es/#architecture). 

You will probably want to go through the files and remove stuff you do not want. 

Some stuff included:

- Normalize CSS
- `data-uri` function for embedding image assets
- `em` and `rem` helper functions  
- Example on how to use same background multiple times with only one include (see `_bgimg-extends.scss`)


