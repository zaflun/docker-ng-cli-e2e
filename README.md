# CI Configuration

1. [Get current Angular CLI e2e version](https://hub.docker.com/r/zaflun/ng-cli-e2e/tags)
2. [Create protractor-ci.conf.js in e2e](#create-protractor-ciconfjs-in-e2e)

***

## Add Support for Angular e2e tests

### Create protractor-ci.conf.js in e2e

```
const config = require('./protractor.conf').config;
 
config.capabilities = {
    browserName: 'chrome',
    chromeOptions: {
        args: ['--headless', '--no-sandbox']
    }
};
 
exports.config = config;
```

### Add protractor-ci config to ng e2e
```
--protractor-config=e2e/protractor-ci.conf.js
```

## Locking the ChromeDriver version
Angular CLI uses webdriver for protractor tests. The npm package to install/update webdriver checks every hour if a new version is available and updates to the latest version. This might break your build if webdriver requires a later version of the Chrome browser. (See https://github.com/angular/webdriver-manager/blob/HEAD/docs/versions.md )
The solution is to run an update to a fixed version just before the actual build happens. This will prevent installation of a later version.

For example:

```
docker ... zaflun/ng-cli-e2e:11.1.0 \
    ./node_modules/protractor/bin/webdriver-manager update --versions.chrome 88.0.4324.96 && \
    ng e2e --webdriver-update=false
```