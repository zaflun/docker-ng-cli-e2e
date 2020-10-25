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