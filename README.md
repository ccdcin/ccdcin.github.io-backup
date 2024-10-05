# About
This is the website for CCDC's 2024 December Conference on Theater of the Oppressed.

# About this document
This document is here to capture how to go about making changes to both the content and the look and feel of the site

# Content
So content on Jekyll (that is the static site generator that this project uses and Github Pages uses to host the site) is stored 
in something called front-matter, and also in structured files that sit inside a special directory called `_data`. Frontmatter is 
denoted by three dashes on the top of the page or post, followed by variables that describe the page and its content. Content 
could be the title of the page or post, the description which could be used on the page itself, and also used to populate SEO tags.

So this looks something like this. Lets assume this is a file called special-page.md:
```
    ---
    title: My special Page
    description: This is a longer bit of text about why I chose to write this page
    author: arun
    permalink: special-page/
    twitter: arunk
    ---`

    # About
    An abstract about this page
```

So some of the tags like title etc are used by Jekyll and they could also be used by our templates to render content. Certain 
data like `permalink` have special meanings in Jekyll. It means the link to the page will be found at https://thissite.com/special-page/
You can put anything you want in permalink, it just can't clash with another page having the same permalink.

# Our Pages
Our site has just a couple of pages. The home page is index.md. This file in turn includes various subsections of the front page, like 
programme.html, about.html etc.

The other main page is speakers.md which is it's own page and found at `/speakers/`.

# Data
The content on the site comes from the files inside `_data` folder.

The files are:
* schedule.yaml
* speakers.yaml

YAML is just a structured way of marking data. Creating whatever kind of relationship and structures you like between data. Creating lists, sub-lists,
objects within lists, lists within objects, objects within other structures etc.

## schedule.yaml
So this file contains the schedule for the conference. It is a list of objects. The hyphen before anything in YAML usually means it is a list. YAML defines 
variables as `name-of-variable: value`. So the schedule.yaml is a list of objects and each object represents one day. Each day has an id, this helps us track 
the day and link to it, and also do things like change the colour for each day. The rest of the fields `title` and `date` are used to display on the bar 
about that day. The day also has one property called `events` which is a list of events. You can see it is also a list because of the hyphen before the `title`
property. So events which is  property of day has a list of individual events that are happening that day. So each event has a `title` property which is used 
to display the name of the event, `timings` used to show the timings of the event, when it starts and ends. And it has `speakers` property which is a list of ids.

The `speakers` propery simply has string IDs, these are the same IDs that are used in speakers.yaml. Against each speaker there is a property named `id` which is a 
string, usually just their first name, but it can be anything, anything that is easy for you to remember when you are adding and changing data. The id field 
cannot have special characters or spcaes in it, so just stick to alphabets and if you really need then numbers.

So to add all the conference events, you can add them one after another in the schedule.yaml file. The order matters, because that is the order in which 
the days and events will be displayed in the programme section of the site. Now this is flexible, lets say you want to extend the day object, to add a property 
called `highlight`, a field that might be used to describe what is the highlight of the day, what event or thing is the most looked out for. Of course just 
adding it to schedule.yaml, is only half the job. The rest is, making changes to the HTML or md files and incorporating the data into the HTML of the page.

So the one strange symbol in the `schedule.yaml` file is the `>-` symbol next to the `description` field. It basically tells Jekyll that the property is a multi-lined 
piece of text.

# speakers.yaml
This file contains all the speakers of the conference. Again order matters. The order you add speakers in this file is the order in which they will show up 
both on the grid and in the list below. Speakers have a full name stored in the `name` property. They also have a `pic` property, which is the name of their profile 
picture. You will have to place the image with that exact file name (these file names are case-sensitive) into the `assets/img/speakers` folder. And then 
when you commit your changes into github, their pictures will appear in the profie section, both in the grid view and the longer list 
view below. I also just added the `social` attribute to the game, which is a list of key value pairs. The key is the name of the social network, and the 
value is your username in that network. The name of the social network is used to pull up the right icon, and then link to the site, and your account 
is used to create the correct hyperlink to go view the speaker's profile on the social media site.

# HTML/CSS
So the files are really quite simple. The main layouts are appropriately inside a directory called `_layouts` The file default.html inside there is the basic 
layout of the site, its basic set of features, what Javascript files it uses, what CSS it uses etc. Although the files are called .html, they are not HTML. 
They are a template format called Jinja. This format allows you to mix both HTML, to structure the page, along with importing other files. 

Important files include:
- `_include/header.html` - This contains the top header and navbar of the site.
- `_includes/footer.html` - This is the default footer on all pages, showing the CCDC logo ultimately. 
- `_includes/programme.html` - This file is included in the main program.
