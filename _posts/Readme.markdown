Readme

##### How to start up this blog:

    > cd ~/klikwiki/ghost
    > npm start

Default port is 2368.

Editing is accomplished (as normal) at `http://localhost:2368/ghost`.

---

##### Set up a static front page from

`https://ghost.org/forum/using-ghost/4647-static-front-page/?page=2`

(This has already been done.  This is just in case I need to do it again!)

---

I just spent a little bit of time getting this working and wanted to share what I did, which is a small update on what evildonald did in post 5.

In core/controllers/frontend.js, we make two replacements and an addition.

> Note: new file path is core/server/controllers/frontend.js

Replacement 1-
~Line180 replace

    if (isNaN(pageParam) || pageParam < 1 || (req.params.page !== undefined && pageParam === 1)) {
with

    if (pageParam < 1) {

---

Replacement 2-
~Line204 replace

    view = (pageParam > 1) ? 'index' : channelOpts.firstPageTemplate;
with 

    view = 'index'

---

***addition***
~line282, after

    single: function (req, res, next) {
    
    var path = req.path,
    
    params,
    
    usingStaticPermalink = false;
add

    if(path == "/"){
                         /////////////////////////////////////////
    path = "/homepage/"  // Note:  I changed to path = "/home/" //
                         /////////////////////////////////////////
    };
    
---

Then one little swap in core/routes/frontend.js:
line 69 change:

    router.get('/', frontend.homepage);
to

    router.get('/', frontend.single);

---

and then make sure you create a static content page with url /homepage **(note: I changed name of page to home, not homepage)** and you're good to go

---

I changed "homepage" to "home" because the function frontendControllers (around line 238 seemed to define the home page by the name "home" rather than "homepage".  I don't know if this name change was necessary.  I made the change before I realized that node.js was caching the pages and that I needed to restart it.)

##### Restart node.js for this to work!

    npm start