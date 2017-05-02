# Heroku Summary

## by Kevin London and Joe Duncko

### About Heroku

According to its [website](https://www.heroku.com/what), "Heroku is a cloud platform that lets companies build, deliver, monitor and scale apps — we're the fastest way to go from idea to URL, bypassing all those infrastructure headaches". Heroku offers a platform as a service that automatically runs many common set ups of modern cloud applications. It compliments this service with third party addons, database support, analytics, CI support, GitHub support, and more to allow you to deploy as fast as possible with as little set up as possible.

### Video

[![Heroku Tool Demo](https://img.youtube.com/vi/5H9lxwXGtqw/0.jpg)](https://www.youtube.com/watch?v=5H9lxwXGtqw)

### Use cases

We’ll be testing using Joe’s senior project, [Cede.io](https://github.com/JoeDuncko/cede.io). It uses Heroku as its hosting service for both the app (Node.js) and the database (MongoDB). It uses the following features from Heroku:

- Easy deployment of a git repository via command line
- No management of infrastructure at all - Heroku automatically guesses and sets up an environment based on your structure
- [Easily keep the deployment version in line with Master on GitHub](https://devcenter.heroku.com/articles/github-integration)
- Addons for common utilities like storage and databases (Cede.io uses the mLab MongoDB Heroku add-on)
- Extensive free tier (sleeps after 30 minutes of activity, limited active time per month)
- With or without a custom domain name (use [cedegame.com](http://cedegame.com/) for the actual game)
- Can see server stats via web
- Manage most things from the website or the command line tool

NOTE: Cede.io actually *can't* scale on Heroku in its current iteration because it does work on a timer, that would be doubled if the app had multiple instances (as per how Heroku scales). More information [here](https://devcenter.heroku.com/articles/scaling#understanding-concurrency). I've thought about using a task queue like RabbidMQ or breaking the timed tasks out to a separate server that only scales vertically (more powerful box). More investigation needs done on this.

### How to Host Cede.io via Heroku

1. Create a Heroku account at [https://id.heroku.com/login](https://id.heroku.com/login)
2. Once on the Heroku Dashboard, create a new Heroku app
3. Select the locale where the app should be hosted, click `Create App`
4. Add a mLab MongoDB Heroku add-on to the app by going to `Resources` > `Find more add-ons` > search for `mlab` > select `mLab MongoDB` > `Install mLab MongoDB` > select the app you just created > `continue` > select a plan (probably the free one) > `Provision`
5. Add a SESSION_SECRET to your Heroku app's environment variables by going to your app's Heroku dashboard > `Settings` > `Reveal environment variables` > type `SESSION_SECRET` as the key and anything as the value > `Add`
6. Install the Heroku CLI from [https://devcenter.heroku.com/articles/heroku-command-line](https://devcenter.heroku.com/articles/heroku-command-line)
7. Open a terminal and run `heroku login` to log in to Heroku
8. Go to where you wish to clone the repo locally and run `git clone https://github.com/JoeDuncko/cede.io.git`
9. Add the Heroku server as a git remote via `heroku git:remote -a [HEROKU APP NAME]`
10. Push the repository to Heroku via `git push heroku master`
11. Heroku should automatically set up and start the app in the cloud

### Tool Evaluation Criteria

Positives

- Easy to set up and maintain
- Easy to set up multiple instances of exactly the same app
- Auto deployment from GitHub Repository upon committing
- Free tier
- Able to use custom domains
- Able to manage most things from the website
- Easy to scale app horizontally [as long as your app is set up in a way that supports doing so](https://devcenter.heroku.com/articles/scaling)

Drawbacks

- Incomplete control over all of infrastructure
- Can't SSH into Heroku box, [see this article for more information](https://devcenter.heroku.com/articles/one-off-dynos#ssh-access)
- Can't save files onto Heroku box or access its storage at runtime, [see this article for more information](https://devcenter.heroku.com/articles/dynos#ephemeral-filesystem)

### Statistics built into Heroku's dashboard

- Memory usage
- Response time
- Throughput (requests/min)

![image](https://cloud.githubusercontent.com/assets/6749768/25643976/e84554f4-2f70-11e7-806d-8b32844b27f2.png)

## References

- [Heroku technical limits](https://devcenter.heroku.com/articles/limits)
