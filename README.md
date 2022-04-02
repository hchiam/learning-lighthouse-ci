# Learning Lighthouse CI from scratch (quickstart)

[![version](https://img.shields.io/github/release/hchiam/learning-lighthouse-ci?style=flat-square)](https://github.com/hchiam/learning-lighthouse-ci/releases)

Just one of the things I'm learning. <https://github.com/hchiam/learning>

Have [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci) tool run with Travis for every commit or PR to a web app project hosted on GitHub.

## Results upon commit

[![Build Status](https://img.shields.io/travis/hchiam/learning-lighthouse-ci/master?style=flat-square)](https://travis-ci.org/hchiam/learning-lighthouse-ci/builds)

**Automated test run info here:** <https://travis-ci.org/hchiam/learning-lighthouse-ci/builds> (or click on the badge above). **Update:** Since June 15th, 2021, building on travis-ci.org "ceased", so you should use travis-ci.com from now on. Some of the old .org links have stopped working, so here's the .com builds page: <https://app.travis-ci.com/github/hchiam/learning-lighthouse-ci/builds> Also, you may want to use free GitHub Actions instead.

**Example PR here (click "View details"):** <https://github.com/hchiam/learning-lighthouse-ci/pull/1#issuecomment-555602268>

## Setup steps (if you `git clone` this repo)

1. To test the web app locally:

    ```bash
    npm install
    npm start
    ```

    and in a separate CLI tab:

    ```bash
    npm run build
    npm install -g @lhci/cli@0.3.x
    lhci autorun
    ```

1. To test the web app upon commit/PR:

    * You might want to edit [.travis.yml](https://github.com/hchiam/learning-lighthouse-ci/blob/master/.travis.yml)
    * You might want to edit [lighthouserc.json](https://github.com/hchiam/learning-lighthouse-ci/blob/master/lighthouserc.json)
    * ***Then*** make your commit.

## Setup steps (if you're starting from an empty folder)

1. For `lhci autorun` to work, you need a web app set up that has things like a dist or public folder, etc. To do that, you can run a one-liner command to set up a React app:

    ```bash
    # cd to desktop or containing folder
    create-react-app my-app
    ```

1. To make sure it's working locally:

    ```bash
    cd my-app
    npm start
    ```

    and in another CLI tab:

    ```bash
    cd my-app
    npm install -g @lhci/cli@0.3.x
    lhci autorun
    ```

1. The key is [setting up](https://github.com/GoogleChrome/lighthouse-ci#quick-start) the Travis file `.travis.yml`:

    ```yml
    language: node_js
    node_js:
      - 10
    before_install:
      - npm install -g @lhci/cli@0.3.x
    script:
      - npm run build
      - lhci autorun
    addons:
      chrome: stable
    ```

## Aside

If you want to see a report with more details (e.g. vulnerable libraries -> which *specific* ones), use a different CLI tool: run [`lighthouse`](https://github.com/GoogleChrome/lighthouse) locally:

```bash
npm install -g lighthouse
lighthouse https://airhorner.com/
# lighthouse <url>
```

Then open the generated html file.
