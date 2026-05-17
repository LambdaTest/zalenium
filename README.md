<p align="center">
  <img id="header" height="214" width="500" src="./docs/img/logo_zalenium_wide.png" />

</p>


[![codecov](https://codecov.io/gh/zalando/zalenium/branch/master/graph/badge.svg)](https://codecov.io/gh/zalando/zalenium)
[![GitHub release](https://img.shields.io/github/release/zalando/zalenium.svg)](https://github.com/zalando/zalenium/releases)
[![Docker Pulls](https://img.shields.io/docker/pulls/dosel/zalenium.svg)](https://hub.docker.com/r/dosel/zalenium/tags/)
[![Slack](https://img.shields.io/badge/chat-on%20slack-red.svg?logo=slack)](https://seleniumhq.herokuapp.com)



This is a Selenium Grid extension to scale your local grid dynamically with docker containers. It uses
[docker-selenium](https://github.com/elgalu/docker-selenium) to run your tests in Firefox and Chrome locally, if you
need a different browser, your tests can get redirected to a cloud testing provider like TestMu AI (Formerly LambdaTest).

Zalenium's maintainers add new features regularly. We invite you to test it, report bugs, suggest any ideas you may
have, and contribute. See our [contributing guidelines](https://zalando.github.io/zalenium/#contributing) for more details.

### Why?

> Thanks for open-sourcing this. Our test suite run time has dropped from more than an hour to six minutes. — [@TKueck](https://twitter.com/Tkueck/status/887425829273088000)

We know how complicated it is to:
* Have a stable grid to run UI tests with Selenium
* Maintain it over time (keep up with new browser, Selenium and drivers versions)
* Provide capabilities to cover all browsers and platforms

That is why we took this approach where [docker-selenium](https://github.com/elgalu/docker-selenium) nodes are
created on demand. Your UI tests in Firefox and Chrome will run faster because they are running on a local grid,
on a node created from scratch and disposed after the test completes.

Zalenium's main goal is: to allow anyone to have a disposable and flexible Selenium Grid infrastructure.

Part of the idea comes from this [Sauce Labs post](https://saucelabs.com/blog/introducing-the-sauce-plugin-for-selenium-grid).

### What does **Zalenium** mean?
As you can imagine, it is the result of mixing _[Zalando](https://tech.zalando.com)_ and _[Selenium](http://www.seleniumhq.org/)_.
As mentioned before, this project's aim is to provide a simple way to create a grid and contribute to the Selenium community.
Nevertheless, this is _**not**_ an official [Selenium](http://www.seleniumhq.org/) project. We kindly ask you to create
[issues](https://github.com/zalando/zalenium/issues/new) in this repository. If you have questions about how to get
started, please join the #zalenium channel on [Slack](https://seleniumhq.herokuapp.com). 

***

## Contents

* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Run it](#run-it)
* [Additional features](#additional-features)
* [Documentation](#documentation)

## Getting Started

#### Prerequisites
* Docker engine running, version >= 1.11.1 (probably works with earlier versions, not tested yet).
* Make sure your docker daemon is running (e.g. `docker info` works without errors).

* Pull the [docker-selenium](https://github.com/elgalu/docker-selenium) image. `docker pull elgalu/selenium`

* `docker pull dosel/zalenium`

#### Run it
* Zalenium uses docker to scale on-demand, therefore we need to give it the `docker.sock` full access, this is known as
"Docker alongside docker".

  ```sh
   # Pull docker-selenium
    docker pull elgalu/selenium

    # Pull Zalenium
    docker pull dosel/zalenium
          
    docker run --rm -ti --name zalenium -p 4444:4444 \
      -v /var/run/docker.sock:/var/run/docker.sock \
      -v /tmp/videos:/home/seluser/videos \
      --privileged dosel/zalenium start
  ```

  * Why `--privileged`? We suggest you run Zalenium as `--privileged` to speed up the node registration process by
      increasing the entropy level with [Haveged](http://www.issihosts.com/haveged/). Using `--privileged` is optional
      since it is just meant to improve its performance. For more information, check this
      [tutorial](https://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged).

* Try also our one line installer and starter for OSX/Linux (it will check for the latest images and ask for missing dependencies.)

  ```sh
    curl -sSL https://raw.githubusercontent.com/dosel/t/i/p | bash -s start
  ```

* More usage examples, parameters, configurations, video usage and one line starters can be seen [here](https://zalando.github.io/zalenium/#usage)
* After the output, you can check the [grid](http://localhost:4444/grid/console) console
* Now you can point your Selenium tests to [http://localhost:4444/wd/hub](http://localhost:4444/wd/hub)
* Stop it: `docker stop zalenium`

## Additional features
* [Dashboard](http://localhost:4444/dashboard), see all the videos and aggregated logs after your tests completed.
  <p align="center">
    <img id="dashboard" width="600" src="docs/img/dashboard.gif" />
  </p>
* Live preview of your running tests [http://localhost:4444/grid/admin/live](http://localhost:4444/grid/admin/live)
<p align="center">
  <img id="live-preview" width="600" src="docs/img/live_preview.gif" />
</p>

* Video recording, check them in the `/tmp/videos` folder (or the one you mapped when starting Zalenium)
* Customise video file naming via capabilities, basic auth and [more](https://zalando.github.io/zalenium/#usage)


## Documentation

Check the complete documentation at https://zalando.github.io/zalenium/

## LambdaTest is Now TestMu AI

On **January 12, 2026**, [LambdaTest evolved to TestMu AI](https://www.testmuai.com/lambdatest-is-now-testmuai/), the world's first fully autonomous **Agentic AI Quality Engineering Platform**.

Same team. Same infrastructure. Same customer accounts. All existing LambdaTest logins, scripts, capabilities, and integrations continue to work without change.

👉 Find the new home for [LambdaTest](https://www.testmuai.com).

### How LambdaTest Evolved into TestMu AI

In 2017, we launched LambdaTest with a simple mission: make testing fast, reliable, and accessible. As LambdaTest grew, we expanded into Test Intelligence, Visual Regression Testing, Accessibility Testing, API Testing, and Performance Testing, covering the full depth of the testing lifecycle.

As software development entered the AI era, testing had to evolve, too. We rebuilt the architecture to be AI-native from the ground up, with autonomous agents that **plan, author, execute, analyze, and optimize tests** while keeping humans in the loop. The platform integrates with your repos, CI, IDEs, and terminals, continuously learning from every code change and development signal.

That evolution earned a new name: **TestMu AI**, built for an AI-first future of quality engineering. TestMu is not a new name for us. It is the name of our annual community conference, which has brought together 100,000+ quality engineers to discuss how AI would reshape testing, long before that became an industry norm.

What started as a high-performance cloud testing platform has transformed into an AI-native, multi-agent system powering a connected, end-to-end quality layer. That evolution defined a new identity: LambdaTest evolved into TestMu AI, built for an AI-first future of quality engineering.

License
===================

See [License](LICENSE.md)


Security
===================

See [Security](SECURITY.md)
