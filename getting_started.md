title: Getting Started
order: 40

This page will help you get started with Telegram!  Yay!

Blogs Posts
------------

If you want to write a blog post, just save the file in the `_posts`
directory.  For example, put the following text in `_posts/hello_world.md`:

    title: Hello World
    date: 2012-07-20
    
    ## Hello World
    
    This is my first blog post.
    
    I like Telegram because:
    
    * It's simple
    * It's got nice templates
    * I control my content
    
If you're using Dropbox to store you files, go to the [Telegram](https://telegr.am)
control panel and click the "Refresh Site" button.

If you're using GitHub to store your files, commit the files (`git add _posts; git commit -m "stuff"`)
and push to GitHub (`git push`).

It will take a few minutes for Telegram to update your site, but once it's updated,
you should see the blog archive page and your blog posts listed on your home page.

Extra Info
-----------

Extra Info is stuff in each page that gives Telegram rules for how to
display the page and how the page fits into the overall structure of the
web site.  There's a list of [Extra Info](https://howto.telegr.am/extra_info)
on the [How To…](https://howto.telegr.am/) site.  Extra Info is also called Properties or Meta Data.

The `_extra_info.md` file contains some Extra Info global to your web site.

    ---
    blog_root: /blog_posts
    site_title: My Blog
    
    ---
    
    This file contains _Extra Info_ about your site.  You can
    put information in here like which directory you want your posts in
    and that sort of stuff and the information will be part of every page
    in your site.  But this page will not be part of your site.

The `blog_root` Extra Info defines what directory to put blogs posts in.

The `site_title` Extra Info is used to define the name of the site.

You can change these values and see what happens.

Note that because the `_extra_info.md` file has a filename that starts with '_', it will not
be output in the resulting web site.

Changing the Template
---------

If no template is present in your set of files (a template is at least a
`/templates-hidden/default.html` file), Telegram loads an external template.

By default, the external template is the Git repository at `https://github.com/telegr-am/template-base.git`.
You can see [default template project](https://github.com/telegr-am/template-base) on GitHub.

If you want to change the template, add the following Extra Info line in any of your files
(although, because it's global, the best place to put it is in `_extra_info.md`):

    template_url: https://github.com/telegr-am/template-blue.git



Adding Pages
-------------

To add a page to your site, create a Markdown or HTML file and put it in your project directory
and update your site.

If you include the `menu` extra info, the page will appear in the menu and if you include
and `order` extra info, that will be the order that the page appears in the menu bar.

Adding stuff to the template page
-------------

By default, the Telegram templates include the `/templates-hidden/include.html` file.  You
can put stuff in this file that changes the way the page is rendered and even add
stuff to the page.

Here are a couple of helpful lines you can include in that file.

Change the footer:

    <span data-lift="xform" data-css="footer *">(c) 2010-2012 David Pollak</span>

The above line uses the `xform` [snippet](https://howto.telegr.am/snippets) which
selects the HTML nodes in the rendered page using the rules in the `data-css`
attribute and then applies a transformation to the selected nodes.  The `footer *`
rule says, "find all the `<footer>` nodes and replace the contents of the footer nodes
with this HTML."  The result will be to put `<span data-lift="xform" data-css="footer *">(c) 2010-2012 David Pollak</span>` into the footer.

Make the template a 2-column template where the left column is 5/8ths the width and
the right column is 3/8ths the width:   
 
    <span data-lift="xform" data-css="#main_content_place [class+]">row</span>
    <span data-lift="xform" data-css="#left_side [class+]">span10</span>
    <span data-lift="xform" data-css="#right_side [class+]">span6</span>
    
The first line selects the element with id `main_content_place` and appends `row` the the `class`
attribute.  The other lines set the span width of the left and right columns.    

Add a Twitter feed to the right side:
    
	<div data-lift="xform" data-css="#right_side *+">
		<span data-lift="twitter?user=dpp"></span>
	</div>

Transform the right side by appending the nodes to the current content of the right side (the `*+`
operator).  The `<span data-lift="twitter?user=dpp"></span>` element invokes the Twitter
snippet with the user `dpp`.

Add Google Analytics to the page:

	<div data-lift="google_analytics?id=abcdefg"></div>

Note that the Google Analytics snippet uses the `tail` snippet so that the actual Google
Analytics JavaScript code appears on the bottom of the page… just before the `</body>` tag.
