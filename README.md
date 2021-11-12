![Huginn](https://raw.github.com/huginn/huginn/master/media/huginn-logo.png "Your agents are standing by.")

-----

## What is Huginn?

Huginn is a system for building agents that perform automated tasks for you online.  They can read the web, watch for events, and take actions on your behalf.  Huginn's Agents create and consume events, propagating them along a directed graph.  Think of it as a hackable version of IFTTT or Zapier on your own server.  You always know who has your data.  You do.

![the origin of the name](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/the-name.png)

#### Here are some of the things that you can do with Huginn:

* Track the weather and get an email when it's going to rain (or snow) tomorrow ("Don't forget your umbrella!")
* List terms that you care about and receive email when their occurrence on Twitter changes.  (For example, want to know when something interesting has happened in the world of Machine Learning?  Huginn will watch the term "machine learning" on Twitter and tell you when there is a spike in discussion.)
* Watch for air travel or shopping deals
* Follow your project names on Twitter and get updates when people mention them
* Scrape websites and receive email when they change
* Connect to Adioso, HipChat, Basecamp, Growl, FTP, IMAP, Jabber, JIRA, MQTT, nextbus, Pushbullet, Pushover, RSS, Bash, Slack, StubHub, translation APIs, Twilio, Twitter, Wunderground, and Weibo, to name a few.
* Send digest email with things that you care about at specific times during the day
* Track counts of high frequency events and send an SMS within moments when they spike, such as the term "san francisco emergency"
* Send and receive WebHooks
* Run custom JavaScript or CoffeeScript functions
* Track your location over time
* Create Amazon Mechanical Turk workflows as the inputs, or outputs, of agents (the Amazon Turk Agent is called the "HumanTaskAgent"). For example: "Once a day, ask 5 people for a funny cat photo; send the results to 5 more people to be rated; send the top-rated photo to 5 people for a funny caption; send to 5 final people to rate for funniest caption; finally, post the best captioned photo on my blog."

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/huginn/huginn?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![Changelog #199](https://img.shields.io/badge/changelog-%23199-lightgrey.svg)](https://changelog.com/podcast/199)

Join us in our [Gitter room](https://gitter.im/huginn/huginn) to discuss the project.

### Join us!

Want to help with Huginn?  All contributions are encouraged!  You could make UI improvements, [add new Agents](https://github.com/huginn/huginn/wiki/Creating-a-new-agent), write [documentation and tutorials](https://github.com/huginn/huginn/wiki), or try tackling [issues tagged with #"help wanted"](https://github.com/huginn/huginn/issues?direction=desc&labels=help+wanted&page=1&sort=created&state=open).  Please fork, add specs, and send pull requests!

Really want a fix or feature? Want to solve some community issues and earn some extra coffee money? Take a look at the [current bounties on Bountysource](https://www.bountysource.com/trackers/282580-huginn).

Have an awesome idea but not feeling quite up to contributing yet? Head over to our [Official 'suggest an agent' thread ](https://github.com/huginn/huginn/issues/353) and tell us!

## Examples

Please checkout the [Huginn Introductory Screencast](http://vimeo.com/61976251)!

And now, some example screenshots.  Below them are instructions to get you started.

![Example list of agents](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/your-agents.png)

![Event flow diagram](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/diagram.png)

![Detecting peaks in Twitter](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/peaks.png)

![Logging your location over time](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/my-locations.png)

![Making a new agent](https://raw.githubusercontent.com/huginn/huginn/master/doc/imgs/new-agent.png)

## Getting Started

### Docker

The quickest and easiest way to check out Huginn is to use the official Docker image. Have a look at the [documentation](https://github.com/huginn/huginn/blob/master/doc/docker/install.md).

### Local Installation

If you just want to play around, you can simply fork this repository, then perform the following steps:

* Run `git remote add upstream https://github.com/huginn/huginn.git` to add the main repository as a remote for your fork.
* Copy `.env.example` to `.env` (`cp .env.example .env`) and edit `.env`, at least updating the `APP_SECRET_TOKEN` variable.
* Make sure that you have MySQL or PostgreSQL installed. (On a Mac, the easiest way is with [Homebrew](http://brew.sh/). If you're going to use PostgreSQL, you'll need to prepend all commands below with `DATABASE_ADAPTER=postgresql`.)
* Run `bundle` to install dependencies
* Run `bundle exec rake db:create`, `bundle exec rake db:migrate`, and then `bundle exec rake db:seed` to create a development database with some example Agents.
* Run `bundle exec foreman start`, visit [http://localhost:3000/][localhost], and login with the username of `admin` and the password of `password`.
* Setup some Agents!
* Read the [wiki][wiki] for usage examples and to get started making new Agents.
* Periodically run `git fetch upstream` and then `git checkout master && git merge upstream/master` to merge in the newest version of Huginn.

Note: By default, email messages are intercepted in the `development` Rails environment, which is what you just setup.  You can view
them at [http://localhost:3000/letter_opener](http://localhost:3000/letter_opener). If you'd like to send real email via SMTP when playing
with Huginn locally, set `SEND_EMAIL_IN_DEVELOPMENT` to `true` in your `.env` file.

If you need more detailed instructions, see the [Novice setup guide][novice-setup-guide].

[localhost]: http://localhost:3000/
[wiki]: https://github.com/huginn/huginn/wiki
[novice-setup-guide]: https://github.com/huginn/huginn/wiki/Novice-setup-guide

### Develop

All agents have specs! And there's also acceptance tests that simulate running Huginn in a headless browser.

* Install PhantomJS 2.1.1 or greater:
  * Using [Node Package Manager](https://www.npmjs.com/): `npm install phantomjs`
  * Using [Homebrew](http://brew.sh/) on OSX `brew install phantomjs`
* Run all specs with `bundle exec rspec`
* Run a specific spec with `bundle exec rspec path/to/specific/test_spec.rb`.
* Read more about rspec for rails [here](https://github.com/rspec/rspec-rails).

## Using Huginn Agent gems

Huginn Agents can now be written as external gems and be added to your Huginn installation with the `ADDITIONAL_GEMS` environment variable. See the `Additional Agent gems` section of `.env.example` for more information.

If you'd like to write your own Huginn Agent Gem, please see [huginn_agent](https://github.com/huginn/huginn_agent).

Our general intention is to encourage complex and specific Agents to be written as Gems, while continuing to add new general-purpose Agents to the core Huginn repository.

## Deployment

Please see [the Huginn Wiki](https://github.com/huginn/huginn/wiki#deploying-huginn) for detailed deployment strategies for different providers.

### Heroku

Try Huginn on Heroku: [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy) (Takes a few minutes to setup. Read the [documentation](https://github.com/huginn/huginn/blob/master/doc/heroku/install.md) while you are waiting and be sure to click 'View it' after launch!)

Huginn launches on the free version of Heroku [with significant limitations](https://github.com/huginn/huginn/blob/master/doc/heroku/install.md). For non-experimental use, we strongly recommend Heroku's 1GB paid plan or our Docker container.

### OpenShift

#### OpenShift Online

Try Huginn on OpenShift Online

Create a new app with either `mysql` or `postgres`:
```bash
oc new-app -f https://raw.githubusercontent.com/huginn/huginn/master/openshift/templates/huginn-mysql.json
```
or
```bash
oc new-app -f https://raw.githubusercontent.com/huginn/huginn/master/openshift/templates/huginn-postgresql.json
```
**Note**: You can also use the web console to import either json file by going to "Add to Project" -> "Import YAML/JSON".

If you are on the Starter plan, make sure to follow the [guide](https://docs.openshift.com/online/getting_started/beyond_the_basics.html#btb-creating-a-new-application-from-source-code) to remove any existing application.

The templates should work on a v3 installation or the current v4 online.

### Manual installation on any server

Have a look at the [installation guide](https://github.com/huginn/huginn/blob/master/doc/manual/README.md).

### Optional Setup

#### Setup for private development

See [private development instructions](https://github.com/huginn/huginn/wiki/Private-development-instructions) on the wiki.

#### Enable the WeatherAgent

In order to use the WeatherAgent you need an [API key with Wunderground](http://www.wunderground.com/weather/api/). Signup for one and then change the value of `api_key: your-key` in your seeded WeatherAgent.

Note, Wunderground no longer offers free API keys. You can still use the WeatherAgent by setting the service key to darksky, and getting an [API key from DarkSky](https://darksky.net/dev).

#### Disable SSL

We assume your deployment will run over SSL. This is a very good idea! However, if you wish to turn this off, you'll probably need to edit `config/initializers/devise.rb` and modify the line containing `config.rememberable_options = { :secure => true }`.  You will also need to edit `config/environments/production.rb` and modify the value of `config.force_ssl`.

## License

Huginn is provided under the MIT License.

Huginn was originally created by [@cantino](https://github.com/cantino) in 2013. Since then, many people's dedicated contributions have made it what it is today.

[![Build Status](https://travis-ci.org/huginn/huginn.svg)](https://travis-ci.org/huginn/huginn) [![Coverage Status](https://coveralls.io/repos/huginn/huginn/badge.svg)](https://coveralls.io/r/huginn/huginn) [![Dependency Status](https://gemnasium.com/huginn/huginn.svg)](https://gemnasium.com/huginn/huginn) [![Bountysource](https://www.bountysource.com/badge/tracker?tracker_id=282580)](https://www.bountysource.com/trackers/282580-huginn?utm_source=282580&utm_medium=shield&utm_campaign=TRACKER_BADGE)

Huginn Docker images
====================

Huginn is packaged in two docker images.

#### [huginn/huginn](multi-process/README.md) multiple process image

This image runs all processes needed by Huginn in one container, when the database is not linked it will also start MySQL internally. This is great to try huginn without having to set up anything, however maintenance and backups can be difficult.

#### [huginn/huginn-single-process](single-process/README.md) multiple container image

This image runs just one process per container and thus needs at least two container to be started, one for the Huginn application server and one for the threaded background worker. It is also possible to every background worker in a separate container to improve the performance. See [the PostgreSQL docker-compose configuration](single-process/postgresql.yml) for an example.

Docker image for Huginn using the production environment and separate container for every process
=================================================

This image runs a linkable [Huginn](https://github.com/huginn/huginn) instance.

It was inspired by the [official docker container for huginn](https://hub.docker.com/r/huginn/huginn)

The scripts/init script generates a .env file containing the variables as passed as per normal Huginn documentation.
The same environment variables that would be used for Heroku PaaS deployment are used by this script.

The scripts/init script is aware of mysql and postgres linked containers through the environment variables:

    MYSQL_PORT_3306_TCP_ADDR
    MYSQL_PORT_3306_TCP_PORT

and

    POSTGRES_PORT_5432_TCP_ADDR
    POSTGRES_PORT_5432_TCP_PORT

Its recommended to use an image that allows you to create a database via environmental variables at docker run, like `postgresql` or `mysql`, so the db is populated when this script runs.

Additionally, the database variables may be overridden from the above as per the standard Huginn documentation:

    DATABASE_ADAPTER #(must be either 'postgresql' or 'mysql2')
    DATABASE_HOST
    DATABASE_PORT

If your database user does not have the permission to create the Huginn database please make sure it exists and set the `DO_NOT_CREATE_DATABASE` environment variable.

This script will run database migrations (rake db:migrate) which should be idempotent.

It will also seed the database (rake db:seed) unless this is defined:

    DO_NOT_SEED

This same seeding initially defines the "admin" user with a default password of "password" as per the standard Huginn documentation.
You can customize the admin account name with the environment variable ``SEED_USERNAME`` and ``SEED_PASSWORD``.

If you do not wish to have the default 6 agents, you will want to set the above environment variable after your initially deploy, otherwise they will be added automatically the next time a container pointing at the database is spun up.

The CMD launches Huginn via the scripts/init script. This may become the ENTRYPOINT later.  It does take under a minute for Huginn to come up.  Use environmental variables that match your DB's creds to ensure it works.

## Usage

Simple startup using docker compose (you need to daemonize with `-d` to persist the data):

    cd docker/single-process
    docker-compose up

or if you like to use PostgreSQL:

    docker-compose -f postgresql.yml up

Manual startup and linking to a MySQL container:

    docker run --name huginn_mysql \
        -e MYSQL_DATABASE=huginn \
        -e MYSQL_USER=huginn \
        -e MYSQL_PASSWORD=somethingsecret \
        -e MYSQL_ROOT_PASSWORD=somethingevenmoresecret \
        mysql

    docker run --rm --name huginn_web \
        --link huginn_mysql:mysql \
        -p 3000:3000 \
        -e DATABASE_NAME=huginn \
        -e DATABASE_USERNAME=huginn \
        -e DATABASE_PASSWORD=somethingsecret \
        huginn/huginn-single-process

    docker run --rm --name huginn_threaded \
        --link huginn_mysql:mysql \
        -e DATABASE_NAME=huginn \
        -e DATABASE_USERNAME=huginn \
        -e DATABASE_PASSWORD=somethingsecret \
        huginn/huginn-single-process /scripts/init bin/threaded.rb

or alternatively:

    docker run --rm --name huginn_threaded \
        --link huginn_mysql:mysql \
        -e DATABASE_NAME=huginn \
        -e DATABASE_USERNAME=huginn \
        -e DATABASE_PASSWORD=somethingsecret \
        -e WORKER_CMD='bin/threaded.rb' \
        huginn/huginn-single-process

## Environment Variables

Other Huginn [12factored](https://12factor.net/) environment variables of note are generated and put into the .env file as per Huginn documentation. All variables of the [.env.example](https://github.com/huginn/huginn/blob/master/.env.example) can be used to override the defaults which a read from the current `.env.example`.

For variables in the .env.example that are commented out, the default is to not include that variable in the generated .env file.

In newer versions of Docker you are able to pass your own .env file in to the container with the `--env-file` parameter.

## Building on your own

You don't need to do this on your own, but if you really want run this command in the Huginn root directory:

    bin/docker_wrapper build --rm=true --tag={yourname}/huginn -f docker/single-process/Dockerfile .

## Source

The source is [available on GitHub](https://github.com/huginn/huginn/tree/master/docker/single-process).

Please feel free to submit pull requests and/or fork at your leisure.
