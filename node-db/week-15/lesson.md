![](https://img.shields.io/badge/status-draft-darkred.svg)

# Node 3

** What we will learn today?**

* [Node Recap](#node-recap)
* [Best Practices](#best-practices)
* [Node Process Managers](#node-process-managers)
* [REST](#rest)
* [Workshop] (#Workshop)
* [Deploying to Heroku](#deploying-to-heroku)
* [Security](#security)
* [Authentication](#authentication)
* [Homework](Homework)

---

## Node Recap

Javascript has evolved from the browser to be used in the backend. It does not need a framework as we saw in [week-13](../week-13/lesson.md), however a framework like Express allows us to develop faster.

### Documentation

When you are working with frameworks it is always helpful to use their documentation.

* [Express Documentation](https://expressjs.com)
* [Node.js Documentation](https://nodejs.org/api/http.html)

### Middleware

Middleware allow us to process requests to add functionalities that are not built in to Express, for example logging, authentication, etc.

> * Express Documentation: [Using Middleware](https://expressjs.com/en/guide/using-middleware.html)
> * Video: [body-parser](https://www.youtube.com/watch?v=vKlybue_yMQ) which makes it easier to work with POST requests and forms.

### Routing

Routing refers to how an application’s endpoints (URIs) respond to the client requests. These are configured differently for each framework, and can range from basic configuration to very extensive for more complex use cases.

Simple example

```js
app.get("/", function(req, res) {
  res.send("hello world");
});
```

More complicated example using `Passport.js` middleware for authentication

```js
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) return next();
  else res.redirect("/login");
}

app.get("/account", ensureAuthenticated, function(req, res) {
  res.send("welcome user!");
});
```

> * Express Documentation: [Routing](https://expressjs.com/en/guide/routing.html)

## Best Practices

Express have their own recommended [best practices page](https://expressjs.com/en/advanced/best-practice-performance.html)

## Node Process Managers

These process managers monitor for any changes in your node.js application and automatically restart the server, perfect for development and production.

> Popular PMs include:
>
> * [nodemon](http://nodemon.io/)
> * [pm2](https://expressjs.com/en/advanced/pm.html#pm2)

## REST

REST is a convention of how to design your API, whether it is for your own frontend, or other frontends and clients.

> * Read: Resource naming in [REST](http://www.restapitutorial.com/lessons/restfulresourcenaming.html) convention

## Workshop

Continue the remaining steps in the albums workshop (../week13/api-workshop.md)

# Deploying to Heroku

Heroku is a cloud platform as a service (PaaS) that lets companies build,
deliver, monitor, and scale apps. Developers use Heroku to deploy, manage, and
scale modern apps. Heroku is fully managed, giving developers the freedom to
focus on their core product without the distraction of maintaining servers,
hardware, or infrastructure.

1. [Signup for an account](https://signup.heroku.com/) on Heroku
   * It will send a verification to your email so make sure you've entered a
     valid email
1. Download the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)
1. We need to do a small tweak to our app to be ready to be deployed on Heroku.

On server.js, add the `process.env.PORT` bit of code

```js
app.listen(process.env.PORT || 3000, function() {
  console.log("Server is listening on port 3000. Ready to accept requests!");
});
```

This tells our server to look for an **environment variable** called `PORT` and
use it to run the server, otherwise use Port 3000. When the server runs on
heroku, then Heroku sets the `PORT` to the correct value.

`git add` and `commit` your change.

4. Now open the command line in the folder where you have your
   **express-workshop** repo running. If you run the command `git remote -v`,
   you should see one remote **origin** pointing to your repo.

Run these commands:

`heroku login`

> This will ask you for your heroku email and password that you used to
> register.

Once you're logged in:

`heroku create`

> The heroku create command creates a new application on Heroku – along with a
> git remote that must be used to receive your application source.

If you check `git remote -v`, you should see a second remote called **heroku**.

Now push your code to heroku `git push heroku master`. The push will run few
commands from Heroku, then you should see a url similar to
`https://some-random-name-XXXX.herokuapp.com` - go to the URL and if all goes
well, your app should be up and running.

To read more about Heroku and deploying Node Apps to Heroku, check:

1. [Deploying with Git](https://devcenter.heroku.com/articles/git)
1. [Getting Started on Heroku with Node.js](https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up)

## Security

When you take your website to production there is a whole range of things to consider.

![HTTP vs HTTPS](../assets/http-vs-https.png)

Node has built in support for HTTPS, and once you have your own certificates you can use this feature. However sometimes when you deploy to `cloud` Platform Platform as a Service (PaaS) providers such as Heroku, they provide SSL and configure it for you automatically.

> * Read: [Node: HTTPS](https://nodejs.org/api/https.html)
> * Read/Watch: [What is an SSL Certificate?](https://www.globalsign.com/en/ssl-information-center/what-is-an-ssl-certificate/)
> * Read: [Heroku SSL](https://devcenter.heroku.com/articles/ssl)

## Authentication

Sometimes you need to add user functionality for your website. To do this you can make use of external libraries like [passport](www.passportjs.org) to add authentication to your website.

> For more information read:
>
> * [OAuth 2.0 Authorization Framework: Bearer Token Usage](https://tools.ietf.org/html/rfc6750)
> * [Bearer Strategy](https://github.com/jaredhanson/passport-http-bearer)

## Homework

{% include "./homeworknew.md" %}

{% include "../../others/escalation-policy.md" %}
