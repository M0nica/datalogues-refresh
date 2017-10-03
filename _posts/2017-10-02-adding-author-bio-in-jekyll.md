---
layout: post
title: How to Add Author Bio to Posts in Jekyll
description: A guide to including biographical information for authors in Jekyll blog posts
image: assets/images/author-bio.png
permalink: adding-author-bios-in-jekyll
author: monica_powell
comments: true
---
*The above image is a preview of how the author bio will appear at the end of this tutorial.*

Datalogues is powered by [Jekyll](https://jekyllrb.com/), a static-site generator. The theme I selected for the site did not support authors out of the box however it is easy to implement author functionality in Jekyll.

### 1) Edit/create appropriate folders and files in Jekyll project

- front matter of individual blog posts where author should be included
- \_layouts/post.html


and created the following folders/files:
- \_data/authors.yml
- \_includes/author_bio.html



### 2) Store Author Data
I have stored my author data in a folder called `_data` that contains a file `authors.yml`. The author information associated with `monica_powell` is pulled into my post from the `authors.yml` data file.

```
monica_powell:
    name: Monica Powell
    email: monica@aboutmonica.com
    twitter: http://twitter.com/waterproofheart
    bio: Monica Powell is a web technologist that cares about increasing the visiblity of underestimated individuals in technology. In 2015, she received the &#35;GIRLBOSS award from Sophia Amoruso’s Girl Boss Foundation. She’s currently focusing on making tech more enjoyable & accessible and is always up to chat data visualizations, web development or &#35;BlackGirlMagic.
    image: http://www.datalogues.com/assets/images/monica-powell-headshot.jpg
```

### 3) Reference relevant authors in the front matter of individual blog posts
In the front matter of each blog post in Jekyll you should reference authors in [YAML (YAML Ain't Markup Language)](http://www.yaml.org/start.html) using the following format `author: NAME OF AUTHOR`. The name of author should be an exact match one of the variables in your `authors.yml`

The front matter in Jekyll sets the metadata for a post and is key to properly building posts. YAML is a human friendly data serialization standard for all programming languages.

Here is an example of the front matter for this particular post.
```
layout: post
title: How to Add Author Bio in Jekyll
description: A guide to adding author bios in Jekyll
image: assets/images/author-bio.png
permalink: adding-author-bios-in-jekyll
author: monica_powell
comments: true
```

### 4) Define HTML for author bio

in the folder `_includes` create a file called `author_bio.html` to define the HTML for how author bio's should be displayed

```

<hr>

  <span>

  <div>
{% if author.image %}<img src="{{author.image}}" class="author-img">{% endif %}


## display author name and link to author's twitter if one has been provided  
  {% raw %}
  <div>
    	<h3> {{author.name}} &nbsp;
     		{% if author.twitter%}
    	 <a href="{{author.twitter}}" class="icon fa-	twitter"><span class="label">Twitter</span></a>
     		{% endif %}
     </h3>
   	</div>


    </div>
    ## Author Bio
      {{ author.bio }}
  </span>
  <br>

  {% endraw %}
```

### 5) Add author bios to the post layout

Add a line in `post.html` where author bio should appear and pull in the HTML as defined above in `author_bio.html`. The logic is set so that it will only call that HTML template if there is author information associated with this particular post.

```
  ## if there is an author bio
  {% raw %}
  {% if author.bio %}
      {% include author_bio.html %}
  {% endif %}
  {% endraw %}
```

All done! Feel free to comment below or tweet me if you have any questions!
