# Heroku Summary

## by Kevin London and Joe Duncko

### About Heroku

According to its [website](https://www.heroku.com/what), "Heroku is a cloud platform that lets companies build, deliver, monitor and scale apps — we're the fastest way to go from idea to URL, bypassing all those infrastructure headaches". Heroku offers a platform as a service that automatically runs many common set ups of modern cloud applications. It compliments this service with third party addons, database support, analytics, CI support, Github support, and more to allow you to deploy as fast as possible with as little set up as possible.

### Use cases

We’ll be testing using Joe’s senior project, Cede.io ( https://github.com/JoeDuncko/cede.io ). It uses Heroku as its hosting service for both the app (Node.js) and the database (MongoDB). It uses the following features from Heroku:

- Easy deployment of a git repository via command line
- No management of infrastructure at all - Heroku automatically guesses and sets up an environment based on your structure
- Easily keep the deployment version in line with Master on GitHub ( https://devcenter.heroku.com/articles/github-integration )
- Addons for common utilities like storage and databases (Cede.io uses the mLab MongoDB Heroku add-on)
- Extensive free tier (sleeps after 30 minutes of activity, limited active time per month)
- With or without a custom domain name (use cedegame.com for the actual game)
- Can see server stats via web
- Manage most things from the website or the command line tool
- Auto scaling (needs tested)

### How to use Heroku

- Create a Heroku account at https://id.heroku.com/login
- Once on the Heroku Dashboard, create a new Heroku app
- Select the locale where the app should be hosted, click `Create App`
- Add a mLab MongoDB Heroku add-on to the app by going to `Resources` > `Find more add-ons` > search for `mlab` > select `mLab MongoDB` > `Install mLab MongoDB` > select the app you just created > `continue` > select a plan (probably the free one) > `Provision`
- Add a SESSION_SECRET to your Heroku app's environment variables by going to your app's Heroku dashboard > `Settings` > `Reveal environment variables` > type `SESSION_SECRET` as the key and anything as the value > `Add`
- Install the Heroku CLI from https://devcenter.heroku.com/articles/heroku-command-line
- Open a teriminal and run `heroku login` to log in to Heroku
- Go to where you wish to clone the repo locally and run `git clone https://github.com/JoeDuncko/cede.io.git`
- Add the Heroku server as a git remote via `heroku git:remote -a [HEROKU APP NAME]`
- Push the repository to Heroku via `git push heroku master`
- Heroku should automatically set up and start the app in the cloud

### tool evaluation criteria

Positives

- Easy to set up and maintain
- Easy to set up multiple intances of exactly the same app
- Auto deployment from Github Repository upon committing
- Free tier
- Able to use custom domains
- Able to manage most things from the website

Drawbacks

- https://devcenter.heroku.com/articles/limits
- Incomplete control over all of infrastructure
- Can't SSH into Heroku box
- Can't save files onto Heroku box or access its storage at runtime
