# [Ocean Premium - Frontend](https://op-dev.jongensvantechniek.nl)


[![CircleCI](https://circleci.com/bb/oceanpremium/ocean-premium-api/tree/feature%2Fskeleton.svg?style=svg&circle-token=384a2a280e94bb67b80b424940eb58d7c41b1d69)](https://circleci.com/bb/oceanpremium/ocean-premium-api/tree/feature%2Fskeleton)
![](https://sonar.jongensvantechniek.nl/api/project_badges/measure?project=com.oceanpremium.api&metric=alert_status)
![](https://sonar.jongensvantechniek.nl/api/project_badges/measure?project=com.oceanpremium.api&metric=bugs)
![](https://sonar.jongensvantechniek.nl/api/project_badges/measure?project=com.oceanpremium.api&metric=code_smells)
![](https://sonar.jongensvantechniek.nl/api/project_badges/measure?project=com.oceanpremium.api&metric=coverage)
![](https://sonar.jongensvantechniek.nl/api/project_badges/measure?project=com.oceanpremium.api&metric=vulnerabilities)

## Table of Content

| Table of Content                                                             |
|------------------------------------------------------------------------------|
| 0. [Setup & Configuration](#markdown-header-setup-&-configuration)           |
| 1. [Compile, build & run locally](#markdown-header-compile,-build-&-run)     |
| 2. [Remote deploying](#markdown-header-remote-deploying)                     |
| 3. [Resources](#markdown-header-resources)                                   |
| 4. [Glossary with definitions](https://bitbucket.org/oceanpremium/ocean-premium-api/wiki/Glossary)

## Resources

- [REST API Best practices](https://github.com/tfredrich/RestApiTutorial.com/raw/master/media/RESTful%20Best%20Practices-v1_2.pdf)

- [Ocean Premium - Jira Scrumboard](https://dudesoftechnology.atlassian.net/jira/software/projects/OP/boards/53)

- [Ocean Premium - API]()

- [Glossary with definitions](https://bitbucket.org/oceanpremium/ocean-premium-api/wiki/Glossary)

- [Wireframes](*Ocean Premium - Wireframes - 12042019_1.0*: https://shopix99-my.sharepoint.com/:b:/g/personal/peter_jongensvantechniek_nl/EeCuNhlCXjdFuX30Rnf0nOMBaau8J35EvcpgcFrefaU3QA?e=pNcUcJ)

- [Initial design](https://www.figma.com/proto/0KBc0Pattj9Cc9ov7akc3VFD/Ocean-Premium?node-id=178%3A1962&viewport=468%2C522%2C0.778865&scaling=min-zoom&redirected=1)

## Project details
This project is a [Next.js](https://nextjs.org/) application using the [React framework](https://reactjs.org/).

[Diagrams](https://bitbucket.org/jvt/ocean-premium-frontend/wiki/Diagrams)

## Setup & Configuration

This sections describes on what the prerequisites are on getting started to get the application up and running.

### Prerequisites

#### Node & NPM

- [MacOS - Node 10.15+](https://nodejs.org/en/download/)
- [Windows - Node 10.15+](https://nodejs.org/en/download/)
- [Linux - Node 10.15+](https://nodejs.org/en/download/)

#### IDE

##### VSCode

It is recommended to use [VSCode](https://code.visualstudio.com/)

##### SonarLint - plugin

Because we use [SonarQube](http://sonarqube.org) for static code-analysis, we will also use the [SonarLint](https://www.sonarlint.org) plugin, which we are going to connect to our SonarQube Instance, to retrieve custom profiles for linting.

Configure VSCode plugin to retrieve profile for project from our JVT SonarQube server:
https://www.sonarlint.org/vscode/#vscode-connected-mode

##### Credentials

- Ask Silvia / Steve

##### CI
- [JVT CircleCI - Ocean Premium team access](https://circleci.com/bb/jvt/oceanpremium)

## Setup & configurations

Make sure prerequisites are met, then clone the repo:

```shell
$ git clone git@bitbucket.org:jvt/ocean-premium-frontend.git
```

### Environment variables

To be documented


### Install packages

```shell
$ npm install
```

#### Run locally

```shell
$ npm run dev
```

#### Or run locally with hot reloading

```shell
$ npm run start-dev
```

Which will starts a node server on [http://localhost:3000](http://localhost:3000)
### Remote deploying

See [here](Remote%20deploying) for instructions on deploying

## Additional configurations / relevant information

TO BE DOCUMENTED

## Dependencies

- [Axios - HTTP client](https://github.com/axios/axios)
- [Express - Webframework](https://github.com/expressjs/express)
- [Next.js - Serverside renderer](https://nextjs.org/)
- [Path-match - API endpoint util](https://github.com/pillarjs/path-match)
- [React.js - UI library](https://reactjs.org/)
- [React-dom - HTML DOM util](https://reactjs.org/docs/react-dom.html)
- [TEMPLATE - NAME - SHORT DESCRIPTION OF DEPENDENCY!!!](https://github.com/defunctzombie/node-url)