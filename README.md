---
title: A Simple Templating Strategy for Canvas Sites
---

# Overview

Tired of chasing down dates and changing data manually on your Canvas site? Wish there was a better way? Well now there is. Using pandoc and markdown you can easily automatically generate your Canvas pages with all the data in the right place.

# How to do it

You'll need two markdown files. One is a template for your page, the other contains the relevant data. Here's an example template that I've saved as `pagetemplate.md`:

```
$if(firsttutorial)$
Your first tutorial is:

* $firsttutorial$
$endif$

$if(secondtutorial)$
Your second tutorial is:

* $secondtutorial$
$endif$

$if(firstassignment)$
Your first assignment is due:

* $firstassignment$
$endif$

$if(secondassignment)$
Your first assignment is due:

* $secondassignment$
$endif$

$body$
```

The stuff between `$` like `secondtutorial` is a variable you will provide data for in your data file.

So corresponding to a template like this, you can keep all your data in one place. Here is an example I saved as `pagedata.md`:

```
---
firsttutorial: Tuesday the 28th of March.
secondtutorial: Tuesday the 11th of March.
firstassignment: April 7 at 23:59
secondassignment: April 29 at 23:59
---

```

The beginning and ending `---` is necessary. Then you just provide data for each of the variables. 

Now, to bring it altogether, run the following pandoc command to create a markdown file from the template:

```
pandoc pagedata.md -o page.md --template=pagetemplate.md
```

Now you have a markdown file that looks like this:

```
Your first tutorial is:

* Tuesday the 28th of March.

Your second tutorial is:

* Tuesday the 11th of March.

Your first assignment is due:

* April 7 at 23:59

Your first assignment is due:

* April 29 at 23:59
```

You can now turn this into some .html ready to past into your Canvas site with the following:

```
pandoc page.md -o page.html
```

The result should be the following .html:

```
<p>Your first tutorial is:</p>
<ul>
<li>Tuesday the 28th of March.</li>
</ul>
<p>Your second tutorial is:</p>
<ul>
<li>Tuesday the 11th of March.</li>
</ul>
<p>Your first assignment is due:</p>
<ul>
<li>April 7 at 23:59</li>
</ul>
<p>Your first assignment is due:</p>
<ul>
<li>April 29 at 23:59</li>
</ul>
```

Ta da!

