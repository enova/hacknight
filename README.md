## [![enova](http://i.imgur.com/5aGFxNT.png)](http://www.enova.com) SOA hacknight
We're going to use [IFTTT](ifttt.com) to grab posts on reddit, send them to a fake a Wordpress application ([ifttt](https://github.com/enova/ifttt)), then to an external application ([reddit_to_twitter](https://github.com/enova/reddit_to_twitter)). Below is an example of taking posts from `r/ruby` and posting them to your Twitter account.

#### `git clone https://github.com/enova/hacknight`

---

#### reddit_to_twitter

1. Sign up for IFTTT/Twitter/Reddit. You can use your personal accounts if you want.
  - [https://ifttt.com/join](http://ifttt.com/join)
  - [https://twitter.com/signup](https://twitter.com/signup)
  - [https://www.reddit.com/login](https://www.reddit.com/login)

2. Register a new app to Twitter
  - [https://apps.twitter.com/](https://apps.twitter.com/)
  - Create New App
    - name: `whatever you want`
    - desc: `whatever you want`
    - website: `heroku URL for reddit_to_twitter application` (step 3)
    - callback url: `leave blank`
  - Save application
  - Select application
    - Change Permissons to `Read and Write`
    - Copy your `Keys and Access Tokens` for below
  
3.  Configure [reddit_to_twitter](https://github.com/enova/reddit_to_twitter/) app and deploy to Heroku
  - `cd reddit_to_twitter/`
  - Edit [server.rb](https://github.com/enova/reddit_to_twitter/blob/master/server.rb#L13) with your Twitter secret keys from above
  - `git add .`
  - `git commit`
  - `heroku create`
  - `git push heroku master`
  - Update the Website setting on the Twitter app you created (step 2)
  
5. Configure [ifttt](https://github.com/enova/ifttt/) app and deploy to Heroku
  - Update `var heroku_app` in [app.js](https://github.com/enova/ifttt/blob/master/app.js#L14) with your heroku URL for the reddit_to_twitter application
  - `heroku create`
  - `git push heroku master`

6. Add [IFTTT.com](http://ifttt.com) channels
  - Go to `Channels`
  - Select `WordPress`
  - Activate Channel
    - Blog URL: `heroku URL for ifttt application` (step 5)
    - Username: `first name`
    - Password: `anything`
  - Activate
  - Go to `Channels`
  - Select `Reddit`
  - Activate
  - Login with Reddit
  
7. Create a new IFTTT Recipe
  - Go to `My Recipes`
  - `Create a Recipe`
  - Choose `Reddit`
    - Any new post in a subreddit
    - ruby, any subreddit you want
  - Click `That`
    - Select `WordPress`
    - Create a post
      - Title: `whatever_you_want` (this is what you will tweet)
      - Body: `whatever_you_want`
      - Categories: `ifttt_application_heroku_url`
    - `Create Recipe`

8. Manually Trigger IFTTT 
  - Select "Check" in your My Recipes Page of IFTTT
