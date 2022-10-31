# mes-logs-service

A serverless microservice responsible reporting error logs from the mes-mobile-app

## Dependencies
DVSA dependencies have been moved from npm to github so in order to install/update any private @DVSA packages
you are required to have an entry in your global `~/.npmrc` file as follows:
```shell
//npm.pkg.github.com/:_authToken=<your auth token here>
```


## Structure

All serverless functions live in dedicated directories in `src/functions`.
Code that is common between multiple functions should reside in `src/common`.

As per the principles of Hexagonal Architecture, each function has the following directories to help us separate concerns:

* `framework` - contains all Inbound and Outbound Adapters, and all use of external/proprietary APIs - depends upon...
* `application` - contains all Inbound and Outbound Ports, doesn't use any external/proprietary APIs - depends upon...
* `domain` - contains all domain objects (Aggregates, Objects, Value classes etc) with all "business logic" (not just anaemic data holders), doesn't use any external/proprietary APIs.

## Build

To build a zip file for every function to `build/artifacts`, run:

```shell
npm run package
```

To build a subset of the functions, pass a comma separated list of function names, like so:

```shell
npm run package -- get,set
```

N.b. The build requires [jq](https://github.com/stedolan/jq).

## Test

To run the unit tests, run:

```shell
npm run test
```

## Integration tests

To run the integration tests, run:

```shell
npm run test:integration
```
