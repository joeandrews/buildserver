Buildserver
===========

A set of tools that deliver an automated build server using node.js for a custom build process.

This library is designed to act as either a standalone buildserver with a dedicated UI to request builds or attatch to github webhooks to deliver automated continious intergration builds or both!


***Install***

Clone the git repository using :

```
git clone git@github.com:joeandrews/buildserver.git

```
The repository is made up of 3 seperate code bases each with there own dependancies.

  • The toolchain, found in /toolchain.
  • The server for the UI found in /server
  • The joblist found in /jobs
  
Both the toolchain and the server require dependancies listed in the respective package.json files. 
These can be installed via:
```
cd /toolchain
npm install

cd ../server
npm install

```
***Instructions***  

**ToolChain**

This a utility belt of tools that are usefull in compiling and building a code base to deploy to production. It includes :
  
  1: A jobhub for managing the job work flow. This is responsible for adding, checking, completing, archiving and listing any jobs.
  
  2: The jobhub includes a tools.js file which provides some standard utility functions for spawning command line proccess, requiring files from the file system and a suite of git functions, for cloning, listing tags and checking out specific versions of a repository.
  
  
**Server**

The server is responsible for deliving the web-ui as well as dealing with the github webhooks. Data is transfered between the client and server via socket.io and dust.js is utilised for clientside templates.
The server can be started in two modes, production(minified) or development.

The server is accesible via port 8100 and provides the following routes by default. The basic auth credentials are:

User: build
Password : build

```
/   This servers the single page UI.
/webhooks    Responsible for handling the post data from the webhooks.
```

```
node server.js --build=norm

node server.js --build=min

```

**Jobs**

The job source code is simply a object keyed by the job types of all the possible jobs that the server can do. e.g("tag_build"). The key must match the value of a job.type key in a job object.
