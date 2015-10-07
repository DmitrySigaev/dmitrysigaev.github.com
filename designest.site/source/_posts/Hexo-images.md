title: How to insert images in your Hexo post 
date: 2013-10-01 19:47:26
tags: Hexo.js, Node.js
categories:
 - Hexo
---

I had started using of Hexo, but Hexo docs are not exhaustive.
So I have decided to describe in my blog how it can be done in different ways.
You can choose yourself.

After Hexo instalation your folder tree looks like:

``` plain
.
+-- _config.yml
+-- package.json
+-- scaffolds
+-- scripts
+-- source
|   +-- _drafts
|   L-- _posts
L-- themes
```

I will describe about the structure in next time. Now we should look at source folder.

### source

Source folder. This is where you put your site's content.
Hexo ignores hidden files and files or folders whose names are prefixed with `_` (underscore) - except the `_posts` folder.
Renderable files (e.g. Markdown, HTML) will be processed and put into the `public` folder, while other files will simply be copied.

So. Let's create a new `images` folder inside of `source` folder:

``` plain
.
+-- _config.yml
+-- package.json
+-- scaffolds
+-- scripts
+-- source
|   +-- images
|   +-- _drafts
|   L-- _posts
L-- themes
```

This `images` folder will simply be copied to `public` folder when you type `hexo generate` command.

Let's insert `test.png` file to `images` folder.
and create a new article:

## new

``` bash
$ hexo new insert-image-to-post
```
Above command will created insert-image-to-post.md file(post)
In the end ofinsert-image-to-post.md file we should insert string:

`![Test PNG image ](/images/test.png)`


Also when you view your site by `hexo server` all should look good.

