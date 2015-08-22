---
layout: post
title:  "Jekyll Instructions"
date:   2015-08-17 10:18:00
categories: 
---

### Fire-up Kasper Locally

Kasper is a port of Ghost's Casper theme to Jekyll.  The advantages to me of this approach are:

- It uses Ghost's Casper theme, which I really like
- It produces *static* pages stored in the _posts subdirectory which are easily backed up and managed rather than a database
- It is suitable for deployment on github pages using Jekyll

Kasper is already installed on this Mac. Further instructions for using it can be found by loading it up.  (I have a page of instructions.)
Follow these instructions to access it:

    > cd ~/jekyll/kasper
    > jekyll serve --watch

If there is an error, you might be prompted to `jekyll build` and start again.  If so, then `jekyll build`.

The `--watch` option autogenerates the static html so that you do not have to constantly rebuild.


The default port is 4000.  If you want to change the server port, use the `--port` option, e.g., `jekyll serve --watch --port 4001`

#### Add Disqus Comments & Google Analytics

You can add disqus comments by adding you disqus shortname in _includes/disqus.html and google analytics to your blog by adding your blog's ID in _config.yml. Its not required but you might want to include those two files in .gitignore. See this [link](From: [link](http://sahilshekhawat.me/sahilshekhawat/tech/blog/2015/05/04/build-a-blog-with-jekyll-and-github-pages.html)).

### Steps to get Kasper up and running on Github Pages

- Fork the Kasper theme [rosario/kasper](https://github.com/rosario/kasper)
- Rename your new repository as **GithubUserName**.*github.io*
- You can access your new website at `http://githubusername.github.io`
- Create a new subdirectory to hold your local files

Then

```
> cd myNewDir
> gem install jekyll
> git init
> git add .
> git commit -m "initial commit"
> git remote add origin YourNewGitRepository
> git push -u origin master
```

Whenever you add or edit files, push them again.

### Alternative: Clone Kasper and Install Jekyll

I was able to get pages to be served on github pages, BUT I was unable to get the Kasper theme applied to them.  I am not sure why.  (But this method involved a **clone** of the Kasper project rather than a **fork**.  That might be the problem.)  But I am including these instructions *just in case*.  See this [link](http://www.jaridmargolin.com/why-i-decided-to-use-jekyll.html).


    $ git clone https://github.com/rosario/kasper.git
    $ cd kasper
    $ gem install jekyll
    $ jekyll serve --watch --port 4001

### Some notes on Jekyll

The posts (which are *static* pages) reside in the _posts subdirectory.  They carry a `*.markdown` extension and are converted to html by the Jekyll "engine."

**The posts must have the *layout block***.
The layout block looks like this:

    ---
    layout: post
    title:  "A test page"
    date:   2015-08-17 10:18:00
    categories: Comedy
    ---
    
The layout references a template in the _layouts folder.

The categories, date and title will form the route to the file (and a subdirectory structure on the local machine).  The category is not necessary.  I do not think the *time* (as opposed to *date*) is necessary.

The date may be necessary (at least for the Kasper implementation).  The site is still "blog-like" and the page routes (and subdirectory structure) are based on a *blog* format.  I think that Kasper **requires** that my file name start with a date (because of its blog origins).  The only exception to that is for the creation of *static top-level* pages (see below).

Each listed category will be part of the URL (see below).  The category may be blank. In the URL the category **precedes** the name of the file.  Further, the naming convention is to hypenate the file name, like so:

- YYYY-MM-DD/cat1/cat2/cat3 etc/Name-of-page.markdown

Thus, for example, the **link** for the page described by the layout block above would be:

    http://localhost:4001/comedy/2015/08/17/A-test-page.html

If there were more categories, each category would beincluded in the route as indicated above.

#### Static top-level pages
You can add pages (e.g., an "about" page) to the "top level" by placing them in the top-level directory.  I believe you will have to restart the server so that the html file based on that markdown file will be created.  The html file will be created and stored in the _site subdirectory.  

*(I have not tried it, but it is probably possible simply to store the exported html to the _site subdirectory.  The markdown can be exported to html by previewing the markdown in the browser and then saving the file as html to the appropriate subdirectory.)*

#### Page Footer

Edit _layouts/post.html to change the page footer.

#### Page Header

The **Home** link on each page still points to the "blog" style home page.  I may be able to change that by adapting the instructions that I found to do that with the Ghost blog.  That remains to be seen.

Note the following code at the top of _layouts/post.html:


```handlebars
<header class="main-header post-head {% if page.cover %}" style="background-image: url({{ page.cover }}) {%else%}no-cover{% endif %}">
    <nav class="main-nav {% if page.cover %} overlay {% endif %} clearfix">
        <a class="back-button icon-arrow-left" href="{{ site.baseurl }}">Home</a>
        <a class="subscribe-button icon-feed" href="{{ site.baseurl }}rss.xml">Subscribe</a>
    </nav>
</header>
```

The home url is defined as "/" using the variable `site.baseurl`.  I should be able to redefine `site.baseurl` much as I did with the Ghost fix.  

(When previewed with the markdown previewer in TextMate, the above code does not appear exactly as it does in the source of this page.  However, when viewed with the Sublime Text markdown previewer, it does appear exactly as above.  If it does not appear in the previewer being used, it is because the referenced variables *have been evaluated*, so the variable `site.baseurl` does not appear in the previewed code.  Rather, what appears in the code is its value, namely, `"/"`.  To see the `site.baseurl` variable (which is what will need to be properly set), you would need to look either at the source of this page, or the source of the page _layouts/post.html.)

#### Hyperlink with anchor

I made this link with an anchor tag:  Test [link](#alternative-clone-kasper-and-install-jekyll) (with anchor).  The jump to the anchor works when the markdown is *previewed* (with the Sublime Text markdown previewer) but not when the page is served from Github pages.  I suppose git flavored markdown does not recognize the anchor.  (This could still be accomplished with *raw* html.)


---

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com


