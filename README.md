<<<<<<< HEAD
This is my website https://jasonsanta.xyz
=======
# blop

Very simple bash based static site generator with absolutely no features at all. Only real dependency is pandoc.

Example [blog](https://uoou.gitlab.io/blop_blog/) and [repo for that blog](https://gitlab.com/uoou/blop_blog) so you can see what's what.

## Installation

Clone the repo and copy the script wherever you like it, curl it, copy and paste. Whatever you fancy, it's a bash script.

## Usage

Run it in the directory where you want your blog to live then upload/push the resulting html to wherever you like.

It expects the following things:

`markdown/`

A directory called markdown which contains the markdown files that will be turned into html blog posts.

`index_template.html`

This is the file the blog's index.html will be built from. Put whatever html you like in here. The post listing will replace the `<!--post-list-->` html comment in this file. You can rejig what gets listed in an option near the top of the blop script itself.

`post_template.html`

Similar to the index template, this is the basis for individual blog posts. The following html comments will be replaced with what you'd expect: `<!--title-->`, `<!--author-->`, `<!--date-->` and `<!--post-->`.

The rest you can do with as you wish - write as much or as little html as you like, CSS it up, include javascript and images and videos and whatnots.

`rss_replate.xml`

This is the template for the RSS feed. What a surprise. Fiddle as you like.

`url.txt`

This file should contain the url of your blog's root, without a trailing space. This is used to provide the absolute links in the RSS feed.

The rest you can do as you like. Put whatever static html you want in the root and link to it from other folers, add an images folder, lots of CSS, videos, under-construction animated gifs...

Each time blop is run it will delete all the html files in the `posts` directory (so don't put any other static content in there, make a separate directory or put it in the root), the `index.html` file and `rss.xml`. It won't touch anything else.


>>>>>>> 1716150 (blop)
