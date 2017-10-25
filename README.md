# dannyEngServerSideNotes
moved to git from enterprise b/c i couldn't figure out to use gitprint on enterprise

# notes about app dev

the purpose of this markdown is to illustrate the components of a web app and to walk through the general work flow of web app development.

---

## some parts to know

Our apps (so far) consist of a few parts:

- the database: this is where we store raw information in the form of tables through PostgresSQL. it lives in the depths of your computer, or in the depths of a server, so the only way you can interact with it is via terminal and .sql files.

- packages/modules: these are bundles of Javascript written by other coders. these packages make complex goals (like DOM manipulation) simpler.

- `package.json`: related to above. this file holds a list of all the necessary packages your project needs to run properly. we can create this file for a new project using `npm init` via terminal. we can also use `npm install` to install all the packages it lists.

- views: before, we used .html files. Unfortunately, .html files are written in stone -- they don't change when we need them to, and, depending on what you're making, you'll need them to. Enter .ejs files; they work like .html files, except they allow variables through your Javascript. We can also split code into parts and connect them -- so you can work on pieces instead of a giant whole. (fyi, this do-it-in-interchangeable-parts style is called modularity.)

- css files: thankfully, these haven't changed much. these files make your webpage look fancy.

there's more, but they're all involved in a complex relationship. let's go through the framework of an app development first:

## database

Build the database structure. Make the migration file(s) and the seed file(s). These structure your database tables and populate those tables, respectively.

## folders

we've got a lot of folders to manage, so here's a generalized folder structure:

```
.
├── README.md
├── app folder
│   ├── controllers
│   │   └── controller.js
│   ├── db
│   │   ├── config.js
│   │   ├── migrations
│   │   │   └── migration.sql
│   │   └── seeds
│   │       └── seed.sql
│   ├── models
│   │   └── model.js
│   ├── node_modules
│   ├── package-lock.json
│   ├── package.json
│   ├── public
│   │   └── styles
│   │       ├── reset.css
│   │       └── style.css
│   ├── routes
│   │   └── routes.js
│   ├── server.js
│   └── views
│       ├── partials
│       │   ├── boilerplate.ejs
│       │   └── end.ejs
│       ├── index.ejs
│       ├── ...
│       └── show.ejs
│

```

(sorry for the crappy tree)

anyways, this structure is something you can expect to manage.

## config

when you do app development, first you need to manage all the configuration. basically, how does your app communicate with the database? (answer: `pg-promise`)

the `config.js` file handles this. it's mostly the same for every project we've done so far save where we designate the target (local) database:

```
    return pgp({
      database: [INSERT DATABASE HERE],
      port: 5432,
      host: 'localhost'
    });
```

replace the insert with whatever you're naming the database on your computer.

EXPORT!

It's also a good idea to keep track of which packages you'll be needing. You can `npm install --save [package here]` that package into your project directory as you need them.

## how it works

here's a handy thing to see how your app generally works:

 - client inputs a URL
 - read & interpret the URL
 - depending on the URL structure, go to specified page and/or talk to the database
 - database does its thing, maybe return information
 - page responds
 - wait for the client to do something else

And here's how your files sorta reflect this work process:

```
address URL -> server.js -> router.js -> controller.js -> model.js -> config.js -> database shenanigans
```

the thing above shows a general idea of what file does what; if your specific process is different somehow, then the order will change.

## model

so your app and your database has the ability to communicate with each other. now you need to tell your app what to say to your database.

we use the model for this. specifically, your `model.js` file holds all the SQL commands you'll ever need for your app.

you'll have to IMPORT your `config.js` because you need its export data.

all the SQL commands you need have to be separated into different methods according to its task. remember, a method is a function located within an object, so create an empty object first!

after you have all the SQL query methods you'll need, EXPORT!

## controller

so now you have a database and what to say to it. now you need something to manage all those SQL commands -- especially if you're looking for complex SQL command sequences!

that's where `controller.js` comes in: your compact all the `model.js` methods into new methods! here's also where you put status messages for your server (500 for errors, for example).

again, IMPORT your `model.js` and EXPORT your `controller.js`.

## router

so you have the methods you need to make your app functions work. now, you just need a way for the client to use those functions. we do this through the URL bar.

since computers are dumb but diligent, you need to tell them how to handle your possibly extensive list of features through the URL. we've been doing it through `/`, `/[some path]`, and `/:id`, but i guess there are other ways.

`router.js` manages those url stuff and associates each combination you use with a `controller.js` method.

so, IMPORT `controller.js` and EXPORT `router.js`.

## server

so you have the routes. now you need your `server.js`. this is where you set up the modules you'll need to do the things your server does. the home page/default pages for your app goes here.

you set up a `static` directory here, which is basically a root directory/origin point for your paths. you also set up a `view` directory here, for your views.

here's a list of packages we import and use here:

 - `express` <- essential. has all the tools your server uses
 - `body-parser` <- lets your server read json stuff
 - `morgan` <- lets you log information onto your console
 - `path` <- sorta subtle. basically, lets you make paths by pasting things together
 - `method-override` <- html does only GET and POST by itself. this lets you do PUT and DELETE via forms.

 we also do the port stuff here.

 check out the `server.js` from our past lectures/assignments for a template.

## views

views! so, i mentioned way above how .html is too stiff for app use. `ejs` is an engine that lets you use .ejs files in place of .html files; .ejs files can react to Javascript-like code!

build your views according to what you need. your `controller.js` will reference to your views since the controller handles rendering specific pages.

## css

css. some people like it, others hate it. flexbox is magic here.

---

so that's basically it.

of course, there's also bug-fixing/quality-testing. what's good about your app? what isn't going as you planned?

generally, errors you get are because you made a typo somewhere, or broke syntax.

remember: html tags need to close. methods and functions might need parameters. type both brackets first, then fill in the contents. make sure loops have ways to end.

big problems are hard to solve, so break them up into smaller chunks.

programming requires critical thinking skills. (i think they call it algorithmic problem-solving or something.) practice approaching any sort of problem by identifying what you need to do, what you have, and what you can do, and what you can find with what you have. then take your new info and repeat. take down the problem step-by-step.

you can google problems for practice, if you want.



anyways, here's all i know so far for the web app unit. hope it's useful for your project.

as far as api usage goes, i haven't really used/practiced it. i'll look over j's video sometime...

