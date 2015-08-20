---
layout: post
title:  "Jekyll Instructions"
date:   2015-08-17 10:18:00
categories: 
---

Test [link](#static-top-level-pages) (with anchor).

### Clone Kasper and Install Jekyll


    $ git clone https://github.com/rosario/kasper.git
    $ cd kasper
    $ gem install jekyll
    $ jekyll serve --watch --port 4001

the --watch option turns on Auto Generation - this is a good thing, so you do not have to `jekyll build` every time you edit a page.  (Port 4000 is the default.  Change it with the --port option.)

The posts (which are *static* pages) reside in the _posts subdirectory.  They carry a `*.markdown` extension and are converted to html by the Jekyll "engine."

**The posts must have the *layout block***.
The layout block looks like this:

    ---
    layout: post
    title:  "A test page"
    date:   2015-08-17 10:18:00
    categories: Comedy
    ---
    
The category is not necessary.  I do not think the time is necessary.

The date may be necessary (at least for the Kasper implementation).  The site is still "blog-like" and the page routes (and subdirectory structure) are based on a *blog* format.  I think that Kasper **requires** that my file name start with a date (because of its blog origins).  The only exception to that is for the creation of *static top-level* pages (see below).

Each listed category will be part of the URL (see below).  The category may be blank. In the URL the category **precedes** the name of the file.  Further, the naming convention is to hypenate the file name, like so:

- YYYY-MM-DD/cat1/cat2/cat3 etc/Name-of-page.markdown

Then, for example, the **link** for this page would become:

    http://localhost:4001/comedy/2015/08/17/A-test-page.html

If there were more categories, each category is sequentially added to the route.

#### Static top-level pages
You can add pages (only static?) to the "top level" by placing them in the kasper directory.  I believe you will have to restart the server so that the html file based on that markdown file will be created.  The html file will be created and stored in the _site subdirectory.  (I have not tried it, but it is probably possible simply to store the exported html to the _site subdirectory.  The markdown can be exported to html by previewing the markdown in the browser and then saving the file as html to the appropriate subdirectory.)

Edit _layouts/post.html to change the page footer.

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

The home url is defined as "/" using the variable `site.baseurl`.  I should be able to redefine `site.baseurl` much as I did with the Ghost fix.  (The above code does not appear exactly as it does in the source of this page.  The variables have been evaluated, so `site.baseurl` does not appear in the code above.  To see the `site.baseurl` variable, you need to look either at the source of this page, or the source of page _layouts/post.html.)


---

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com


