# defra-hapi-handlers
Base class to define the GET and POST handlers for a given route

[![Build Status](https://travis-ci.com/DEFRA/defra-hapi-handlers.svg?branch=master)](https://travis-ci.com/DEFRA/defra-hapi-handlers)
[![Known Vulnerabilities](https://snyk.io/test/github/defra/defra-hapi-handlers/badge.svg)](https://snyk.io/test/github/defra/defra-hapi-handlers)
[![Code Climate](https://codeclimate.com/github/DEFRA/defra-hapi-handlers/badges/gpa.svg)](https://codeclimate.com/github/DEFRA/defra-hapi-handlers)
[![Test Coverage](https://codeclimate.com/github/DEFRA/defra-hapi-handlers/badges/coverage.svg)](https://codeclimate.com/github/DEFRA/defra-hapi-handlers/coverage)

## Installation

Via github:
```
npm install --save https://github.com/DEFRA/defra-hapi-handlers.git#master
```

It is recommended that tie to a specific commit/version as follows:
```
npm install --save https://github.com/DEFRA/defra-hapi-handlers.git#commit_or_version
```
## Usage
Please note:
 - this example is written using the standard linter (no semicolons)
 - example usage can be found within the unit tests 
```
// Registering handlers:

// First extend the Handlers class

class Handlers extends require('defra-hapi-handlers') {
  get schema () {
    return Joi.object({ config: 'schema config' })
  }

  get errorMessages () {
    return {
      'field-name': {
        'error.type': 'error message'
      }
    }
  }

  async getBreadcrumbs () {
    return [{
      text: 'Home',
      href: '/'
    }, {
      text: 'Current'
    }]
  }

  get payload () {
    return { data: 'stuff' }
  }
}

// Now get ready to register the routes using the instance of the new Handlers class

const Hapi = require('hapi')
const server = hapi.server()

const handlers = new Handlers()

// routes will include a 2 element array where the first is the hapi route configuration for a get method and the second is for a post method
const [ getRoute, postRoute ] = handlers.routes({
  path: '/my-page',
  app: {
    view: 'my-page'
  }
})

// Register each routes
server.route(getRoute)
server.route(postRoute)

```
## Contributing to this project

Please read the [contribution guidelines](/CONTRIBUTING.md) before submitting a pull request.

## License

THIS INFORMATION IS LICENSED UNDER THE CONDITIONS OF THE OPEN GOVERNMENT LICENCE found at:

<http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3>

The following attribution statement MUST be cited in your products and applications when using this information.

>Contains public sector information licensed under the Open Government license v3

### About the license

The Open Government Licence (OGL) was developed by the Controller of Her Majesty's Stationery Office (HMSO) to enable information providers in the public sector to license the use and re-use of their information under a common open licence.

It is designed to encourage use and re-use of information freely and flexibly, with only a few conditions.
