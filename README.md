Bob [![http://travis-ci.org/cliffano/bob](https://secure.travis-ci.org/cliffano/bob.png?branch=master)](http://travis-ci.org/cliffano/bob)
---

Convention-based build tool for Node.js projects.

Installation
------------

    npm install -g bob

Project Convention
------------------

Mandatory:

* package.json - project descriptor file
* lib/ - directory containing JavaScript library files
* test/ - directory containing JavaScript test files

Optional (only relevant when project is an app):

* {name}.js - main app file, must support `node {name}.js start|stop|restart|status`
* run/ - directory containing any runtime information like pid or log files

Reserved and generated by Bob:

* build/ - directory containing build reports and artifacts

Usage
-----

Bob can be run from the project root directory (same level as package.json file).

Install project dependencies (per Node.js project):

    bob dep
    
Run Bob from project directory:

    bob target1 target2 target3 ...

Run Bob with specific environment:
(if unspecified, NODE_ENV defaults to 'development')

    NODE_ENV=production bob start

Run Bob in robot mode and generate XML reports:
(if unspecified, BOB_MODE defaults to 'human')

    BOB_MODE=robot bob lint test
    
Targets
-------

<table>
  <tr>
    <td>dep</td>
    <td>Install all dependencies specified in package.json file by executing <code>npm install .</code> .</td>
  </tr>
  <tr>
    <td>tools</td>
    <td>Install all Bob dependencies having binary executablein the global scope.</td>
  </tr>
  <tr>
    <td>clean</td>
    <td>Delete build/ and run/ directories, along with any nohup.* and *.log files.</td>
  </tr>
  <tr>
    <td>lint</td>
    <td>Run <a href=http://github.com/jshint/node-jshint">jshint/node-jshint</a> or <a href=http://github.com/tav/nodelint">tav/nodelint</a> against all .js files in lib/ and test/ directories.</td>
  </tr>
  <tr>
    <td>style</td>
    <td>Run <a href=http://github.com/nomiddlename/jscheckstyle">nomiddlename/jscheckstyle</a> against all .js files in lib/ directory.</td>
  </tr>
  <tr>
    <td>test</td>
    <td>Run <a href=http://github.com/cloudhead/vows">cloudhead/vows</a> against all .js files in test/ directory.</td>
  </tr>
  <tr>
    <td>coverage <code>(experimental)</code></td>
    <td>Run <a href=http://github.com/visionmedia/node-jscoverage">visionmedia/node-jscoverage</a> via <a href=http://github.com/cloudhead/vows">cloudhead/vows</a> against all .js files in test/ and lib/ directories.</td>
  </tr>
  <tr>
    <td>doc</td>
    <td>Run <a href=http://github.com/nodeca/ndoc">nodeca/ndoc</a> against all .js files in lib/ directory.</td>
  </tr>
  <tr>
    <td>versionup</td>
    <td>Upgrade patch version number in package.json file.</td>
  </tr>
  <tr>
    <td>versionup-minor</td>
    <td>Upgrade minor version number in package.json file.</td>
  </tr>
  <tr>
    <td>versionup-major</td>
    <td>Upgrade major version number in package.json file.</td>
  </tr>
  <tr>
    <td>template <code>(experimental)</code></td>
    <td>Populate variables in template files with values from package.json file.</td>
  </tr>
  <tr>
    <td>stop</td>
    <td>Stop the app by executing <code>node {name}.js stop</code> .</td>
  </tr>
  <tr>
    <td>start</td>
    <td>Start the app by executing <code>node {name}.js start</code> .</td>
  </tr>
  <tr>
    <td>restart</td>
    <td>Restart the app by executing <code>node {name}.js restart</code> .</td>
  </tr>
  <tr>
    <td>status</td>
    <td>Display app status by executing <code>node {name}.js status</code> .</td>
  </tr>
  <tr>
    <td>nuke</td>
    <td>Kill all processes with command containing the word 'node' .</td>
  </tr>
  <tr>
    <td>package</td>
    <td>Create a .tar.gz package file at build/artifact/ directory, along with md5 and sha1 checksums of the package file.</td>
  </tr>
  <tr>
    <td>package-meta <code>(experimental)</code></td>
    <td>Create a meta file to build/artifact, along with md5 and sha1 checksums of the meta file.</td>
  </tr>
  <tr>
    <td>deploy <code>(experimental)</code></td>
    <td>Upload the .tar.gz package file to a remote location, either via SCP or FTP.</td>
  </tr>
  <tr>
    <td>deploy-unpack <code>(experimental)</code></td>
    <td>Deploy, then remotely unpack the .tar.gz package file via SSH.</td>
  </tr>
  <tr>
    <td>deploy-restart <code>(experimental)</code></td>
    <td>Deploy, unpack, then remotely execute <code>node {name.js} restart</code> .</td>
  </tr>
</table>

Continuous Integration
----------------------

###Travis CI

Add this scripts.test to project's package.json file:

    {
      "scripts": {
        "test": "npm install -g bob; bob clean lint test coverage;"
      }
    }

###Jenkins CI

Install Bob on the server, then configure a job with shell script build step 

    bob clean lint test coverage;

Config
------

TODO

Colophon
--------

Follow [@cliffano](http://twitter.com/cliffano) on Twitter.