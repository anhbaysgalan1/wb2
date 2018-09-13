# # Cryptex - an open-source crypto currency exchange



## [Cryptex.online](https://www.cryptex.online) Introduction

Cryptex is a free and open-source crypto currency exchange implementation with the Rails framework.
Cryptex.online is a fork of Cryptex designed for micro-services architecture. We have simplified the code
in order to use only Cryptex API with external frontend and server components.

To build your own exchange you should now run Cryptex as a backend instead of forking the repository,
and extend it using other microservices such as [Barong](https://www.github.com/rubykube/barong).

## Mission

Our mission is to build an open-source crypto currency exchange with a high performance trading engine and incomparable security. We are moving toward dev/ops best practices of running an enterprise grade exchange.

We provide webinar or on site training for installing, configuring and administration best practices of Cryptex.
Feel free to contact us for joining the next training session: [Cryptex.online](https://www.cryptex.online)

Help is greatly appreciated, feel free to submit pull-requests or open issues.

## Things You Should Know

**RUNNING AN EXCHANGE IS HARD.**

This repository is not a turn key solution and will require engineering and design of security process by your company, with or without our assistance. This repository is one component among many we recommend using for composing an enterprise grade exchange. It is highly recommended to deploy a UAT environment and build automated tests for your needs, including Functional tests, Smoke tests and Security vulnerability scans. You may not need to have an active developer on Cryptex source code, however, we recommend the following team setup: 1 dev/ops, 3 frontend developers (react / angular), 2 QA engineers, 1 Security Officer.

**SECURITY KNOWLEDGE IS A REQUIREMENT.**

Cryptex cannot protect your customers if you leave your admin password 1234567, or open sensitive ports to public internet. No one can. Running an exchange is a very risky task because you're dealing with money directly. If you don't know how to make your exchange secure, hire an expert.

You must know what you're doing, there's no shortcut. Please get prepared before you continue:

* Rails knowledge
* Security knowledge
* Cloud and Linux administration
* Docker and Kubernetes administration
* Micro-services and OAuth 2.0

## Features

* Designed as high performance crypto currency exchange
* Built-in high performance matching-engine
* Built-in multiple wallet support (e.g. deposit, hot, warm and cold)
* Build-in Management API - server-to-server API with high privileges
* Build-in RabbitMQ Event API
* Usability and scalability
* Websocket API and high frequency trading support
* Support multiple digital currencies (e.g. Bitcoin, Litecoin, Ethereum, Ripple etc.)
* Support ERC20 Tokens
* API endpoint for FIAT deposits or payment gateways.
* Powerful admin dashboard and management tools
* Highly configurable and extendable
* Industry standard security out of box
* Maintained by [cryptex.online](https://www.cryptex.online)
* [KYC Verification](http://en.wikipedia.org/wiki/Know_your_customer) provided by [Barong](https://www.github.com/rubykube/barong)

## Getting Started

We advice to use [minimalistic environment](#minimalistic-local-development-environment-with-docker-compose) if you want to develop only Cryptex and don't touch processes which interact with other components.

Otherwise we advice to use [workbench based environment](#local-development-environment-with-workbench)

### Minimalistic local development environment with docker-compose:

#### Prerequisites
* [Docker](https://docs.docker.com/install/) installed
* [Docker compose](https://docs.docker.com/compose/install/) installed
* Ruby 2.5.1
* Rails 4.2+

#### Installation

1. Copy initial configurations `./bin/init_config`
2. Install yarn dependencies `rake yarn:install`
3. Start backend services (RabbitMQ, Redis, MySQL) `docker-compose -f config/backend.yml up -d`
4. Setup database `rake db:create db:migrate db:seed`
5. Start cryptex daemons `god -c lib/daemons/daemons.god`
6. Start rails server `rails server`

### Local development environment with workbench:

We suggest you to start using Cryptex by installing [Workbench](https://github.com/rubykube/workbench). [Workbench](https://github.com/rubykube/workbench) which is based on [Docker containers](https://www.docker.com/what-docker) is a convenient and straightforward way to start Cryptex development environment.

#### Prerequisites
* [Docker](https://docs.docker.com/install/) installed
* [Docker compose](https://docs.docker.com/compose/install/) installed

#### Prepare the workbench

1. Recursive clone : `git clone --recursive https://github.com/rubykube/workbench.git`
2. Move to workbench `cd workbench`
3. Build the images: `make build`
4. Run the application: `make run`

You should add those hosts to your `/etc/hosts` file:

```
0.0.0.0 api.wb.local
0.0.0.0 auth.wb.local

0.0.0.0 api.slanger.wb.local
0.0.0.0 ws.slanger.wb.local

0.0.0.0 pma.wb.local
0.0.0.0 monitor.wb.local

0.0.0.0 btc.wb.local
0.0.0.0 eth.wb.local
```
Now you have cryptex up and running.

#### [Barong](https://github.com/rubykube/barong)

Barong is an essential part of Rubykube Cryptex. It is a KYC OAuth 2.0 provider. Barong replace the KYC, 2FA, Phone verification from legacy Cryptex.
Barong manage roles and kyc level across all applications from the RKCP. It's easy to extend by using the EventAPI or Rest API.

##### Barong key features

* KYC Verification for individuals
* SMS and Google two-factor authentication
* OAuth 2.0 provider
* Transaction Signature support
* Supply JWT tokens to frontend and mobile app


Start barong:

```sh
$> docker-compose run --rm barong bash -c "./bin/link_config && ./bin/setup"
$> docker-compose up -d barong
```

This will output password for **admin@barong.io**. Default password is **`Qwerty123`**

#### Cryptex

Start cryptex server

```sh
$> docker-compose run --rm cryptex bash -c "./bin/link_config && rake db:create db:migrate db:seed"
$> docker-compose up -d cryptex
```

After all of that you can start using Cryptex in your browser just by following one of the hosts which you added earlier.


### Production setup:

* [Deploy production cluster with kite](https://github.com/rubykube/kite/blob/master/README.md)
* [Kubernetes deployment architecture](docs/architecture.md)

## API

You can interact with Cryptex through API:

* API v2
* Management API v1
* Websocket API

## Getting Involved
We want to make it super-easy for Cryptex users and contributors to talk to us and connect with each other, to share ideas, solve problems and help make Cryptex awesome. Here are the main channels we're running currently, we'd love to hear from you on one of them:

### Discourse

[Rubykube Discourse Forum](https://discuss.rubykube.io)

This is for all Cryptex users. You can find guides, recipes, questions, and answers from Snowplow users including the Cryptex.online team.
We welcome questions and contributions!

### Telegram

[@cryptex](https://t.me/cryptex)

Chat with us and other community members on Telegram.

### GitHub
Cryptex issues

If you spot a bug, then please raise an issue in our main GitHub project (rubykube/cryptex); likewise, if you have developed a cool new feature or improvement in your Rubykube Cryptex fork, then send us a pull request!
If you want to brainstorm a potential new feature, then the Rubykube Discourse Forum (see above) is probably a better place to start.

### Email
hello@cryptex.online

If you want to talk directly to us (e.g. about a commercially sensitive issue), email is the easiest way.

## Getting Support and Customization

If you need help with running/deploying/customizing Cryptex,
you can contact us on [cryptex.online](https://www.cryptex.online).

Contact us by email: [hello@cryptex.online](mailto:hello@cryptex.online)

## License

Cryptex is released under the terms of the [MIT license](http://cryptex.mit-license.org).

## What is Cryptex?

[Cryptex](http://en.wikipedia.org/wiki/Pixiu) (Chinese: 貔貅) is a Chinese mythical hybrid creature
considered to be a very powerful protector to practitioners of Feng Shui.

**[This illustration copyright for Cryptex Team]**

![logo](public/cryptex.png)
