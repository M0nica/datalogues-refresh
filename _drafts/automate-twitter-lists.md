---
layout: post
title: Auto-populate Twitter Lists in 5 minutes with Python
description: Using Twython Twitter API wrapper to add users to a Twitter List
image: assets/images/blue_bird.jpg
permalink: automate-twitter-lists
author: monica_powell
comments: true
category: Dev
tags: [web, api, twitter]
---



We are going to create a Python script that will automatically search Twitter
for individuals who use the **#FreeCodeCamp** hashtag and add them to a Twitter
list of “FreeCodeCampers”. [Twitter
lists](https://help.twitter.com/en/using-twitter/twitter-lists) are a way to
curate a group of individuals on Twitter and collect all of their tweets in a
stream, without having to follow each individual accounts. Twitter lists can
contain up to 5,000 individual Twitter accounts.

We can accomplish this by installing a couple of Python packages, registering an
application with Twitter, accessing our Twitter credentials, making [Twitter
Search
API](https://developer.twitter.com/en/docs/tweets/search/api-reference/get-search-tweets)
calls and [Twitter list
API](https://developer.twitter.com/en/docs/accounts-and-users/create-manage-lists/api-reference/get-lists-list)
calls.

### 1. Installing necessary Python packages

First we need to create a file named `addToFreeCodeCampList.py` where we will
write our script and then import two Python modules into this file:

**Import Config**

In the same directory as our`addToFreeCodeCampList.py`  we will create a file
named `config.py` that stores our top secret Twitter API credentials. We are
going to import our API credentials from that file into our
`addToFreeCodeCampList.py` by including the line  `import config`. Twitter
requires a valid API key, API secret, access token and token secret for all API
requests.

**Import Twython**

[Twython](https://github.com/ryanmcgrath/twython) is a Python wrapper for the
Twitter API that makes it easier to programmatically access and manipulate data
from Twitter using Python. We can import Twython with the following line `from
twython import Twython, TwythonError`.

Your `addToFreeCodeCampList.py` should now look like this:

    import config
    from twython import Twython, TwythonError

### 2. Twitter Authentication

Second, we need to authenticate our application in order to access the Twitter
API. You need to have a Twitter account in order to access [Twitter’s
Application Management site](https://apps.twitter.com/). The Application
Management site is where you can view/edit/create API keys, API secrets, access
tokens and token secrets.

1.  In order to create these credentials we need to create an application by going
to the Application Management site and clicking “Create new app” which should
direct you to a page that looks similar to the one below.

![](https://cdn-images-1.medium.com/max/800/1*H8TiOR6qnIXo_sNoRb7OGw.png#img-center)

2.  You should fill out of the required fields and then click “Create your
Twitter application”. You will then be redirected to a page with details about
your application

3. Click on the tab that says “Keys and Access Tokens”. Copy the Consumer Key
(API Key) and Consumer Secret (API Secret) into the `config.py` file

4. Scroll down and click to create access tokens. Copy the generated Access
Token and Access Token Secret into the `config.py` file.

For reference, I recommend formatting your config.py similar to the file below:

{% gist M0nica/1ccc5716b189df683062d1cfb926d960 %}

<span class="figcaption_hack">Above is my recommended format for a Twitterr API config.py. If you are committing to GitHub.</span>

5. Right now all of our Twitter credentials live inside of our `config.py`.
We’ve imported `config` into our `addToFreeCodeCampList.py` file however, we
have not actually passed any information between the files.

Let’s change that by creating a Twython object and passing in the necessary
secret passwords from our `config.py` with the following:

  ```twitter = Twython(config.api_key, config.api_secret, config.access_token, config.token_secret)```

The `addToFreeCodeCampList.py` file should now look similar to this:

{% highlight python linenos %}
    import config

    from twython import Twython, TwythonError

    # create a Twython object by passing the necessary secret passwords
    twitter = Twython(config.api_key, config.api_secret, config.access_token, config.token_secret)

{% endhighlight %}    

### 3. API Twitter searches and add users to list

- Let’s make an API call to search Twitter and return the 100 most recent,
original tweets that contain “#FreeCodeCamp”

{% highlight python linenos %}
      # return tweets containing #FreeCodeCamp
    response = twitter.search(q=’”#FreeCodeCamp” -filter:retweets’, result_type=”recent”, count=100)
    {% endhighlight %}

- Look at the tweets returned from our search

{% highlight python linenos %}
    # for each tweet returned from search of #FreeCodeCamp
    for tweet in response[‘statuses’]:
     # print tweet info if needed for debugging
     print(tweet)
     print(tweet[‘user’][‘screen_name’])
    {% endhighlight %}

A single tweet returned by this API call looks like this in JSON:

{% highlight json linenos %}

    {'created_at': 'Sun Dec 24 00:23:05 +0000 2017', 'id': 944725078763298816, 'id_str': '944725078763298816', 'text': 'Why is it so hard to wrap my head around node/express. Diving in just seems so overwhelming. Templates, forms, post…
     'truncated': True, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ae52rro63i', 'expanded_url': 'https://twitter.com/i/web/status/944725078763298816', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com" rel="nofollow">Twitter Web Client</a>', 'in_reply_to_status_id': None, 'in_reply_to_status_id_str': None, 'in_reply_to_user_id': None, 'in_reply_to_user_id_str': None, 'in_reply_to_screen_name': None, 'user': {'id': 48602981, 'id_str': '48602981', 'name': 'Matt Huberty', 'screen_name': 'MattHuberty', 'location': 'Oxford, MS', 'description': "I'm a science and video game loving eagle scout with a Microbio degree from UF. Nowadays I'm working on growing my tutoring business at Ole Miss. Link below!", 'url': 'https://t.co/dfuqNNoBYZ', 'entities': {'url': {'urls': [{'url': 'https://t.co/dfuqNNoBYZ', 'expanded_url': 'http://www.thetutorcrew.com', 'display_url': 'thetutorcrew.com', 'indices': [0, 23]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 42, 'friends_count': 121, 'listed_count': 4, 'created_at': 'Fri Jun 19 04:00:44 +0000 2009', 'favourites_count': 991, 'utc_offset': -28800, 'time_zone': 'Pacific Time (US & Canada)', 'geo_enabled': False, 'verified': False, 'statuses_count': 199, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/777294001598758912/FVOIrnb4_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/777294001598758912/FVOIrnb4_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/48602981/1431670621', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': True, 'default_profile_image': False, 'following': False, 'follow_request_sent': False, 'notifications': False, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 1, 'favorite_count': 0, 'favorited': False, 'retweeted': False, 'lang': 'en'}
    MattHuberty

{% endhighlight %}

and like this on Twitter.com:

<center><blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Why is it so hard to wrap my head around node/express. Diving in just seems so overwhelming. Templates, forms, posts, gets, Jade/Pug, Stylus, npm. The learning resources assume you know too much. <a href="https://twitter.com/hashtag/NodeJS?src=hash&amp;ref_src=twsrc%5Etfw">#NodeJS</a> <a href="https://twitter.com/hashtag/freecodecamp?src=hash&amp;ref_src=twsrc%5Etfw">#freecodecamp</a></p>&mdash; Matt Huberty (@MattHuberty) <a href="https://twitter.com/MattHuberty/status/944725078763298816?ref_src=twsrc%5Etfw">December 24, 2017</a></blockquote></center>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


- Add Tweet-ers to our Twitter list

In order to add the author of the tweet to our Twitter list we need the username
associated with the tweet `tweet['user']['screen_name']`

Let’s try to add the users from these tweets to our freecodecamplist. I created
my Twitter list at
[https://twitter.com/waterproofheart/lists/freecodecampers](https://twitter.com/waterproofheart/lists/freecodecampers)
which means for my script the slug is `freecodecampers` and the
`owner_screen_name` is mine, waterproofheart.

![](https://cdn-images-1.medium.com/max/600/1*nlyUXiitKFHOHk9hwUpl7w.png#img-center)

You can create your own Twitter list by navigating to your Twitter profile on
desktop and clicking on the left-hand side to “Create a list”. View the
o[fficial Twitter List
documentation](https://help.twitter.com/en/using-twitter/twitter-lists) for more
information.

{% highlight python linenos %}
    for tweet in response['statuses']:

    # try to add each user who has tweeted the hashtag to the list
     try:
     twitter.add_list_member(slug=’YOUR_LIST_SLUG’, owner_screen_name=’YOUR_USERNAME’, screen_name= tweet[‘user’][‘screen_name’])

    #if for some reason Twython can't add user to the list print exception message
    except TwythonError as e:
     print(e)
{% endhighlight %}

You can test your script by running `python addToFreeCodeCampList.py` in the
terminal.

My working script looks like this:

{% gist M0nica/1ccc5716b189df683062d1cfb926d960 %}

This script can be set to automatically run locally or remotely via a cron job
which allow tasks to be performed on a server on a set schedule.


**A version of this article was originally published by Monica Powell on [FreeCodeCamp](www.aboutmonica.com/) on January, XY, 2018**
