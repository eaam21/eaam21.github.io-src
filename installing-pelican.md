Title: Installing pelican
Slug: installing-pelican
Date: 2016-05-03 17:14:36
Tags: pelican, python, blog
Category: software
Authors: Elías Alejandro

When I decided to start with this blog I didn't know about Pelican I just wanted a free hosting for my blog
integrated with git, some time ago some friends told me about Octopress and how it works however it runs with
ruby. Currently I'm not familiar with ruby (long time ago I made a task with ruby on rails
however nowadays my knowledge about ruby can be a little bit rusty) So I started to 
looking for a python alternative because currently it's more comfortable for me.
There are many sites about how to install Pelican, I took some pieces of them to make launch this blog.
At the end of this post I've included some of them.


###Repos
Firstly we need to have a github repository to upload the blog. To publish you only need one
repository named like your username with *github.io* at the end. Please refer to github for create static web pages.
```console
 username.github.io
```
ok. but I decided to have 2 repos the first one to publish my blog and the second one for store the
markdown sources needed to build all the html for the blog
```console
 username.github.io-src
```
It might be annoying because we have 2 repos, but I thought it can save my life later. :)

###Installation
Create and activate a virtual environment to install pelican.
```console
$ pip install virtualenv
$ virtualenv ~/pelican
$ cd ~/pelican
$ . bin/activate
```
Into pelican directory with the environment activated, install: pelican and markdown
```console
$ pip install pelican
$ pip install markdown
```
Then go to root directory and create 'blog' directory. Into this directory we'll create
all pelican files.
```console
$ ls
bin  include  lib  local
$ mkdir blog
$ ls
bin  blog  include  lib  local
```
Enter into the 'blog' diretory and create all the Pelican files.
Pelican will ask you some questions about your blog. At this point you should already have a git repo to upload your blog.
```console
$ pelican-quickstart
Where do you want to create your new web site? [.] 
 What will be the title of this web site? My Blog
 Who will be the author of this web site? Your Blog Name
 What will be the default language of this web site? [en] 
 Do you want to specify a URL prefix? e.g., http://example.com   (Y/n) y
 What is your URL prefix? (see above example; no trailing slash) http://username.github.io
 Do you want to enable article pagination? (Y/n) y
 How many articles per page do you want? [10] 
 What is your time zone? [Europe/Paris] America/Lima
 Do you want to generate a Fabfile/Makefile to automate generation and publishing? (Y/n) Y
 Do you want an auto-reload & simpleHTTP script to assist with theme and site development? (Y/n) y
 Do you want to upload your website using FTP? (y/N) n
 Do you want to upload your website using SSH? (y/N) n
 Do you want to upload your website using Dropbox? (y/N) n
 Do you want to upload your website using S3? (y/N) n
 Do you want to upload your website using Rackspace Cloud Files? (y/N) n
 Do you want to upload your website using GitHub Pages? (y/N) y
 Is this your personal page (username.github.io)? (y/N) y
```
Then pelican will generate the following files:
```console
blog/
  ├── content
  ├── output
  ├── develop_server.sh
  ├── fabfile.py
  ├── makefile
  ├── pelicanconf.py       
  └── publishconf.py
```
*content:* contains all our markdown files.

*output:* contains all the html that will be visible.

Pelican look into the *content* directory and then generate all the html, css,..
in the *output* directory to be published. At this point we can see our blog with:
```console
$ make devserver
```
go to your favorite browser. 
```console
http://localhost:8000
```
You can only see the blog without any posts. To stop your local webserver:
```console
$ ./develop_server.sh stop
```
###The first post
I removed those 2 directories (content, output) and clone my 2 repos intead of them.
```console
$ rmdir content output
$ git clone https://github.com/username/username.github.io.git output
$ git clone https://github.com/username/username.github.io-src.git content
```
We are going to create the first post. Enter into the content directory and create
a file with .md extension and the following content. It can be *hello.md*
```console
Title: My super title
Date: 2010-12-03 10:20
Modified: 2010-12-05 19:30
Category: Python
Tags: pelican, publishing
Authors: Alexis Metaireau, Conan Doyle
Summary: Short version for index and feeds

This is the content of my super blog post.
```
Then let's Pelican builds our blog:
```console
$ make devserver
```
This command will create all the html, css.. into output directory.
Finally go to : `http://localhost:8000`. At this point you can easily take a tour
for how to write under markdown format.
###Themes
You can change the default theme provided by Pelican. There's some themes in
[http://www.pelicanthemes.com](http://www.pelicanthemes.com) 

So you can list all the installed themes with:
```console
$ pelican-themes -l
```
Install a new theme
```console
$ pelican-themes -vi /path/to/your/downloaded-directory-theme
```
Activate the theme. Add to `pelicanconf.py` file the theme's name
```console
THEME = 'awesome-theme'
```
Then rebuild all with:
```console
$ make devserver
```
###Disqus
You can also add Disqus to your blog. First you need go to Disqus website, sign up and then get your *userid*
then add it into the `pelicanconf.py` file
```console
DISQUS_SITENAME=u'yourusername'
```
###Publishing
Finally to see *blog* under github web only make a git push. 
```console
$ cd output
$ git add .
$ git commit -m "First post"
$ git push -u origin master
```
Don't forget there are 2 repos the first one to publish (html, css...)
and the second one to upload the markdown files.
```console
$ cd content
$ git add .
$ git commit -m "First post source"
$ git push -u origin master
```
Now, you can visit the https://username.github.io and see the new site you’ve just created.

You can add *plugins*, *social widget*, modify *site url* all that into the `pelicanconf.py` file. 
I recomend read more about this file from the official Pelican website.
###Tips and Tricks
You can visit [https://github.com/getpelican/pelican/wiki/Tips-n-Tricks](https://github.com/getpelican/pelican/wiki/Tips-n-Tricks)
to obtain some tricks for Pelican.

I use the *make newpost* it is a useful script to automatically create new posts. :)


###Links
Usefull links that help me to make this blog:

[http://docs.getpelican.com/en/3.6.3/](http://docs.getpelican.com/en/3.6.3/)

[http://chdoig.github.io/create-pelican-blog.html](http://chdoig.github.io/create-pelican-blog.html)

[https://fedoramagazine.org/make-github-pages-blog-with-pelican/](https://fedoramagazine.org/make-github-pages-blog-with-pelican/)

[http://cyrille.rossant.net/pelican-github/](http://cyrille.rossant.net/pelican-github/)

[http://mathamy.com/migrating-to-github-pages-using-pelican.html](http://mathamy.com/migrating-to-github-pages-using-pelican.html)

[http://www.wangbo.info/config-pelican-themes-disqus-and-pygments.html](http://www.wangbo.info/config-pelican-themes-disqus-and-pygments.html)
