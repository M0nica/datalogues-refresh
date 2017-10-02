---
layout: post
title: How to Add Author Bio in Jekyll
description: A guide to adding author bios in Jekyll
image: assets/images/GetOut.png
permalink: adding-author-bios-in-jekyll
author: monica_powell
comments: true
---

In the front matter of post in Jekyll you can reference authors by writing `author: NAME OF AUTHOR`
```
layout: post
title: How to Add Author Bio in Jekyll
description: A guide to adding author bios in Jekyll
image: assets/images/GetOut.png
permalink: adding-author-bios-in-jekyll
author: monica_powell
comments: true
```

In this example I have stored my author data in a folder called `_data` that contains a file `authors.yml`

```monica_powell:
    name: Monica Powell
    email: monica@aboutmonica.com
    twitter: http://twitter.com/waterproofheart
    bio: Monica Powell is a web technologist that cares about increasing the visiblity of underestimated individuals in technology. In 2015, she received the &#35;GIRLBOSS award from Sophia Amoruso’s Girl Boss Foundation. She’s currently focusing on making tech more enjoyable & accessible and is always up to chat data visualizations, web development or &#35;BlackGirlMagic.
    image: http://www.datalogues.com/assets/images/monica-powell-headshot.jpg
```

in the folder `_includes` have a file called `author_bio.html`
```
<hr>

  <span><div>
{% if author.image %}<img src="{{author.image}}" class="author-img">{% endif %}


    <div><h3> {{author.name}} &nbsp; {% if author.twitter%} <a href="{{author.twitter}}" class="icon fa-twitter"><span class="label">Twitter</span></a> {% endif %}</h3></div></div>
      <!-- Personal Info. -->
      {{ author.bio }}
  </span>
  <br>
```
