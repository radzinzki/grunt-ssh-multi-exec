#grunt-ssh-multi-exec [![Build Status](https://travis-ci.org/ArnoldZokas/grunt-ssh-multi-exec.png?branch=master)](https://travis-ci.org/ArnoldZokas/grunt-ssh-multi-exec)
> Execute a set of SSH commands against multiple boxes

## Getting Started
This plugin requires Grunt `0.4.x`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-ssh-multi-exec --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-ssh-multi-exec');
```

##Overview
In your project's Gruntfile, add a section named `grunt-ssh-multi-exec` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  'ssh-multi-exec': {
    your_target: {
      mode: 'parallel | sequential'
      hosts: ['127.0.0.1:2222'],
      username: 'user',
      privateKey: '/path/to/private/key',
      commands: [
        {
          input: 'uptime',
          success: function(data, context) {
            // optional callback
            // 'data' contains stdout response from the target box
            // 'context' contains:
            // {
            //   host: '127.0.0.1'
            //   port: '2222'
            // }
          },
          error: function(err, context) {
            // optional callback
            // 'err' contains stderr response from the target box
            // 'context' contains:
            // {
            //   host: '127.0.0.1'
            //   port: '2222'
            // }
          }
        }
      ]
    },
  },
});
```
Commands execute sequentially, in the order specified.
By default, command sets are executed in against all specified hosts in parallel. To execute command sets against one host at a time, set `mode` option to `sequential`.

##Examples
###Single machine, single command
```js
config: {
  hosts: ['127.0.0.1:2222'],
  username: 'user',
  privateKey: '/path/to/private/key',
  commands: [
    {
      input: 'touch me'
    }
  ]
}
```

###Single machine, single command (with callbacks)
```js
config: {
  hosts: ['127.0.0.1:2222'],
  username: 'user',
  privateKey: '/path/to/private/key',
  commands: [
    {
      input: 'touch me',
      success: function(data) {
        console.log(data);
      },
      error: function(err) {
        console.log(err);
      }
    }
  ]
}
```

###Password authentication
```js
config: {
  hosts: ['127.0.0.1:2222'],
  username: 'user',
  password: 'password',
  commands: [
    {
      input: 'touch me'
    }
  ]
}
```

###Single machine, multiple commands
```js
config: {
  hosts: ['127.0.0.1:2222'],
  username: 'user',
  privateKey: '/path/to/private/key',
  commands: [
    {
      input: 'touch me'
    },
    {
      input: 'touch again'
    }
  ]
}
```

###Multiple machines, multiple commands
```js
config: {
  hosts: ['127.0.0.1:2222', '127.0.0.1:2223'],
  username: 'user',
  privateKey: '/path/to/private/key',
  commands: [
    {
      input: 'touch me'
    },
    {
      input: 'touch again'
    }
  ]
}
```

##Release History
* **v2.4.0** (2014-03-14)
 * added option to execute command sets sequentially
* **v2.3.0** (2014-03-13)
 * added context to success and error callbacks
* **v2.2.0** (2014-03-12)
 * fixed dependency versioning
* **v2.1.0** (2014-03-12)
 * fixed bug that was preventing execution of commands that do not return a response
* **v2.0.0** (2014-03-11)
 * **Breaking change!** - task renamed to `ssh-multi-exec`
* **v1.0.0** (2014-03-10)
 * **Breaking change!** - see port configration
 * added support for executing commands against multiple boxes
 * added log message batching (clean, coherent logs)
* **v0.1.2** (2014-03-10)
 * added password-based authentication
* **v0.1.0** (2014-03-07)
 * initial release

##Contributors
* [@matteofigus](https://github.com/matteofigus)
* [@jankowiakmaria](https://github.com/jankowiakmaria)
