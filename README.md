<div align="center">
<img src="blop_logo.png" />
</div>

Very simple bash based static site generator with absolutely no features at all. Only real dependency is pandoc.

Demo [blog](https://uoou.gitlab.io/blop_blog/) and [repo for that blog](https://gitlab.com/uoou/blop_blog/tree/master/public) so you can see what's what.

## Installation

Clone the repo and copy the script wherever you like, curl it, copy and paste. Whatever you fancy, it's just a bash script.

## Usage

`blop` essentially just converts markdown into HTML in a lightly structured way. Run `blop` in a directory where you want the local copy of your blog to live and then upload/push the resulting HTML to your website.

### Structure

The stuff `blop` expects inside that local blog folder is as follows:

| Directory/File | Description |
| - | - |
| `markdown/` | A directory called 'markdown' which contains the markdown files which will be turned into HTML blog posts. |
| `index_template.html` | Used to generate the site's 'index.html' file. |
| `post_template.html` | Used to generate individual blog posts. |
| `archive_template.html` | Used to generate the blog archive, if enabled. (See [Per-Site Settings](#per-site-settings)). |
| `rss_template.xml` | Used to generate the RSS feed. |
| `url.txt` | A simple text file containing the live site's URL, **without trailing slash**. Used to construct the absolute links in the RSS feed. |
| `site.conf` | An optional file which sets up some defaults on a per-site basis. See [Per-Site Settings](#per-site-settings). |

### Templating

`blop` uses (very) light templating. The various `*_template.html` files can be constructed in normal HTML. Special HTML comment tags in these files will be replaced with particular content in the HTML output when `blop` is run.

For example, `<!--post list-->` in `index_template.html` will be replaced with the actual post listing in `index.html` when it is generated.

Here's a complete list of templatable files and the template tags available to them:

#### index_template.html

| Tag | Description |
| - | - |
| `<!--post list-->` | The post listing — a list of links to blog posts. You can format this list as you like; see `listing_format` in [Per-Site Settings](#per-site-settings). |

#### post_template.html

| Tag | Description |
| - | - |
| `<!--title-->` | The title of the blog post. Derived from the markdown file's filename unless overidden in the [Front Matter](#front-matter). |
| `<!--author-->` | The name of the post's author. Derived from `default_author` in `site.conf` (see [Per-Site Settings](#per-site-settings)) unless overidden in the [Front Matter](#front-matter). |
| `<!--date-->` | The post's date. This is derived from the markdown file's modification date. Date can be overidden in [Front Matter](#front-matter). |
| `<!--post-->` | The post's contents. i.e. the actual body text of the post. |

#### archive_template.html

| Tag | Description |
| - | - |
| `<!--archive list-->` | The post listing for the archive page — a list of links to blog posts. You can format this list as you like; see `listing_format` in [Per-Site Settings](#per-site-settings). See also `max_posts` in [Per-Site Settings](#per-site-settings) |

#### rss_template.xml

| Tag | Description |
| - | - |
| `<!--url-->` | Replaced with the site's base URL as derived from `url.txt` (see [Structure](#structure)). |
| `<!--rss-->` | The body text of the post in an RSS-friendly format. |

### Front Matter

Individual posts can contain minimal YAML*ish* front matter to override the post title and author name. Put something like the following (including the dashes) at the top of a post's markdown:

```
---
author: Rebecca Black
title: It's Friday
date: 2011-03-14
summary: The order of days of the week
---
```

The following fields are available in a post's front matter:

| Field | Description |
|-|-|
| `author` | Overrides the default author as defined in `site.conf`. |
| `title` | Overrides the title as derived from the markdown file's name |
| `date` | Overrides the date as derived from the file's modification date. Format can be anything the `date` command would understand as input. YYYY-MM-DD is probably simplest. |
| `summary` | A short post-summary which can be used in `listing_format`. See [Per-Site Settings](#per-site-settings). |
### Per-Site Settings

You can create a file called `site.conf` in the blog's root directory to override default settings. Format is YAML*ish*, i.e.:

```
max_posts: 20
short_date_format: %Y
default_author: Rebecca Black
```

Settings are:

| Setting | Description |
|-|-|
| `default_author` | Unless overidden in the blog's markdown file (see [Front Matter](#front-matter)), this will be the author. |
| `max_posts` | How many posts to list in the index.html. Set to `unlimited` to list all posts and disable the archive. |
| `group_by_date` | Whether to insert date-grouping headers in the index listing as in the archive. Set to `true` or `false`. |
| `date_format` | The format to use for dates on blog entires. |
| `short_date_format` | The date format to use when grouping by date. |
| `listing_format` | The format to use in post listings. `<!--title-->`, `<!--summary-->` (described in [Front Matter](#front-matter)), `<!--author-->` and `<!--date-->` will be replaced with what you'd expect and `<!--title-nospaces-->` equates to the generated html file's basename, to be used in links. |

Note that settings values should be unquoted.

Date format strings are as per Linux's `date` command. See `man date` or [this handy table](https://www.tutorialkart.com/bash-shell-scripting/bash-date-format-options-examples/#list-of-bash-date-formatting-options).

## Miscellany

Each time blop is run it will delete all the html files in the `posts` directory (so don't put any other static content in there, make a separate directory or put it in the root), the `index.html` file, `archive.html` and `rss.xml`. It won't touch anything else.

The examples in [the example repo](https://gitlab.com/uoou/blop_blog/tree/master/public) constitute a very minimal example of a working blog. You can really go nuts with the template files and structure them how you like. You can also add in as many other static HTML files wherever you like (outside of the `posts` directory). `blop` *won't touch* any static content you add to your site.

#### Examples

A couple of example sites using `blop`.

* [My new personal blog](https://friendo.monster/)
* [HexDSL's site](https://hexdsl.co.uk/)
* [HexDSL's pixel art site](https://pixelfridge.club/)
