## [![enova](http://i.imgur.com/5aGFxNT.png)](http://www.enova.com) SOA hacknight
We're going to use [IFTTT](ifttt.com) to grab posts on reddit and send them to an external application to play with ([reddit_to_twitter](https://github.com/enova/reddit_to_twitter)). 

Below is an example of taking new posts from `r/ruby` and posting them to your Twitter account.

---

#### reddit_to_twitter

1. Sign up for IFTTT/Twitter/Reddit. You can use your personal accounts if you want.
  - [https://ifttt.com/join](http://ifttt.com/join)
  - [https://twitter.com/signup](https://twitter.com/signup)
  - [https://www.reddit.com/login](https://www.reddit.com/login)

2. Register a new app to Twitter
  - [https://apps.twitter.com/](https://apps.twitter.com/)
  - Create New App
    - Name: `whatever you want`
    - Description: `whatever you want`
    - Website: `http://google.com/` (will change in step 3)
    - Callback URL: `leave blank`
  - Save application
  - Select application
    - Click on Permissons tab and change to `Read and Write`
    - Click on the Keys and Access Tokens tab. Generate an `Access Token`
    - Copy your generated keys for below
  
2. Install Git/Git for Windows and Heroku Toolbelt
  - [http://git-scm.com/download/win](http://git-scm.com/download/win)
  - [https://toolbelt.heroku.com/windows](https://toolbelt.heroku.com/windows)
  
3. Clone down the repo:
  - `git clone https://github.com/enova/reddit_to_twitter`

4.  Configure [reddit_to_twitter](https://github.com/enova/reddit_to_twitter/) app and deploy to Heroku
  - `cd reddit_to_twitter`
  - Change [server.rb](https://github.com/enova/reddit_to_twitter/blob/master/server.rb#L13) with your Twitter secret keys from above
  - `git add .`
  - `git commit -m 'added keys'`
  - `heroku create YOURNAME-ruby` (replace YOURNAME with... your name)
  - `git push heroku master`
  - Update the Website setting on the Twitter app you created (step 2) with `YOURNAME-ruby.herokuapp.com`

5. Add [IFTTT.com](http://ifttt.com) channels
  - When logged in, go to  `Channels`
  - Select `Maker`
  - Activate 
  - Go back to `Channels`
  - Select `Reddit`
  - Activate
  - Login with Reddit
  
7. Create a new IFTTT Recipe
  - Go to `My Recipes`
  - Click `Create a Recipe`
  - Click `This`
    - Select `Reddit` as Trigger Channel
      - `Any new post in a subreddit` as a Trigger
      - `ruby` or any subreddit you want
  - Click `That`
    - Select `Maker` as Action Channel
      - `Make a Web Request` as Action
        - Url: `YOURNAME-ruby.herokuapp.com`
        - Method: `post`
        - Content Type: `application/json`
        - Body: `{{Title}} - {{Content}}` (feel free to use something else)
    - Create Recipe

8. Manually Trigger the Recipe 
  - Press `Check` in your My Recipes Page of IFTTT
  - Check the log to see if it ran successfully

9. Annoy your followers with automatically posted tweets.

#### debugging

You've finished the above steps, yet you're still not seeing any tweets? 

- Use the command `heroku logs` inside of your app folders. This will show you the server log from your heroku apps. 
  
