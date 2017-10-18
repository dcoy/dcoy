+++
comments = false
date = "2017-09-21T16:13:19-05:00"
description = "Getting setup with Hugo"
draft = false
showcomments = false
showpagemeta = false
slug = ""
title = "Hugo & AWS: Part 1"
tags = ["AWS","Hugo","Cloudfront","S3"]
+++

Hello there! This is part one in a series of blog posts that will provide a simple walkthrough on getting setup with Hugo, AWS and TravisCI. I will start with getting Hugo setup locally, configuring your AWS S3 & Cloudfront setup, then end with TravisCI integration. This series of blog posts makes the assumption that you're familiar with the command line.

## What is Hugo?

Hugo is a static site generator. This means that it does not require a backend database or a server to process dynamic content calls. Hugo is fantastic for site landing pages for projects, a blog, or portfolio site.

## Why Hugo?

I chose Hugo as my static site generator for a few reasons:

  1. It's crazy fast. Just check out [How fast is Hugo?](https://gohugo.io/about/what-is-hugo/#how-fast-is-hugo)
  2. Hugo utilizes Go's templating, making writing templates a breeze.
  3. It's simple to setup, just download the binary, which is cross platform, and you're all set!

## Dive into Hugo

Installing Hugo is pretty straight forward, here are the commands that will get you in the right direction:

For macOS, use Homebrew:

```
brew install hugo
```

For Windows, use Chocolatey:

```
choco install hugo -confirm
```

For Linux, use snap or [Linuxbrew](https://linuxbrew.sh):

```
snap install hugo
```

```
brew install hugo
```

Once the installation process finishes, you can test to see if Hugo installed properly, by running `hugo version`. You should see something similar to this:

```
➜  ~ hugo version
Hugo Static Site Generator v0.20.7 darwin/amd64 BuildDate: 2017-05-06T22:00:51-05:00
```

Now that you've successfully installed Hugo, it's time to create your site. Switch to the directory that you'd like your Hugo site to be, then run:

```
hugo new site <site-name>
```

The `hugo new site` will generate the scaffold to build your site, however it does not provide a theme. At this point, your site will look pretty boring, so let's add a theme to it. Head to the [Hugo Themes](https://themes.gohugo.io/) page and choose a theme. I chose to use the [Cactus Plus Theme](https://themes.gohugo.io/hugo-theme-cactus-plus/) by [Hang Jiang](https://github.com/nodejh), however you should choose a theme that works best for you.

Once you have chosen a theme that suits your needs, be sure to initiate tracking on your site, so that you can track the changes you make and commit them to GitHub. Now you're ready to add the theme to your site -- there are two methods to do so:

1. Clone the theme as a Git Submodule to the `themes/` directory.
2. Clone the theme into the `themes/` directory

I chose option #2 as I want to get started quickly, and updates to the theme did not concern me. My intention is to create a new theme all together, but that's later down the line. I may end up replacing this with option #1 in the future. For now, here's how I did this. You will be executing three commands, so let's break down what will be run.

The first command to execute will create the `.gitignore` file and ensure you don't track the `public/` directory, along with all of its contents. By default, Hugo generates the `public/` directory to server its static assets, but you don't need to commit those to version control. 

```
echo -e "#Don't track public directory\npublic/**" >> .gitignore
```

Next, you'll be executing a command that clones down the repository of the theme you'd like to use for your Hugo site, into the `themes/` directory:

```
git clone https://github.com/nodejh/hugo-theme-cactus-plus.git themes/cactus-plus
``` 

Finally, you will want to update your TOML configuration file to use the theme when the Hugo build process is executed:

```
echo 'theme = "cactus-plus"' >> config.toml
```

Now that you have initiated version control, set your `.gitignore` file, cloned down a theme and updated the TOML configuration file to use the theme, it's time to add a post to the site. Note: the path to the "posts" directory is dependent on the theme itself, however most themes follow the _`posts/post-title.md`_ convention:

```
hugo new post/first-post.md
```

Update your first post to within the `content/post/` directory with some content, then run `hugo server -wv`, visit `localhost:1313` to see your post! 

**Note**: If you are not seeing your post, it is more than likely set to `draft = true` in the post's metadata. You can simply run `hugo server -wvD` or set `draft = false` to view the post.

That's it! You've successfully installed Hugo, now get to blogging! Next, we're going to cover configuring AWS S3 and Cloudfront to host and serve all of the static content for your site.

Thank you for reading!