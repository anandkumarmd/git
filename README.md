git
===

http header::
http://code.tutsplus.com/tutorials/http-headers-for-dummies--net-8039

node:
----
PATH:C:\Program Files\nodejs;C:\Users\Kumar\AppData\Roaming\npm;
C:\Users\Kumar\AppData\Roaming\npm
  bower (config file)
  bower.cmd (?)
  karma
  karma.cmd
  
  [node_modules] folder contains all plugins
    bower (install javascrip framework)
    karma (install and execute tesing framework)
    karma-jasmine
    karma-chrome-launcher



npm
===
C:\Users[username]\AppData\Roaming\npm

Do you have a file named grunt.cmd in this folder? If not i'd maybe try again

npm install -g grunt-cli 

If this exists and you have 

C:\Users[username]\AppData\Roaming\npm in your PATH environment variable then typing grunt from a command prompt should work.


npm ( get's location of .npmrc => config file)
npm config
npm config ls -l  (list long)


npm -g  (global vs local)
In general, the rule of thumb is:
LOCAL::If you’re installing something that you want to use in your program, using require('whatever'), then install it locally, at the root of your project.
GLOBAL::If you’re installing something that you want to use in your shell, on the command line or something, install it globally, so that its binaries end up in your PATH environment variable.


bower
====

Try reinstalling it. npm cache clean && npm uninstall -g bower && npm install -g bower

module.js:340
    throw err;
          ^
Error: Cannot find module 'H:\AppData\Roaming\npm\Roaming\npm\node_modules\bower'
    at Function.Module._resolveFilename (module.js:338:15)
    at Function.Module._load (module.js:280:25)
    at Function.Module.runMain (module.js:497:10)
    at startup (node.js:119:16)
    at node.js:901:3


change in bower.cmd
- - - - - - - - - - 
@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\Roaming\npm\node_modules\bower" %*
) ELSE (
  node  "%~dp0\Roaming\npm\node_modules\bower" %*
)


TO

@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\Roaming\npm\node_modules\bower" %*
) ELSE (
  node  "%~dp0\node_modules\bower" %*
)


grunt
====
http://chariotsolutions.com/blog/post/grunt-javascript-centric-build-tool/

pwd>set PATH=X:\AppData\Roaming\npm;%PATH%

http://attebury.me/blog/2014/01/nodejs-gruntjs-and-path-errors-in-windows-7

[[edit in X:/AppData/Roaming/npm]]

@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\Roaming\npm\node_modules\grunt-cli" %*
) ELSE (
  node  "%~dp0\node_modules\grunt-cli\bin\grunt" %*
)
----------------------------------------------------------------------------------------
Nodejs Gruntjs And Path Errors In Windows 7

@attebury
GitHub
Flickr
31 January 2014

nodejs, gruntjs, and windows7

Whew. I had a lot of trouble getting GruntJS to work on Windows 7 at the office and so leave this google fruit for the next intrepid enterprise front-end developer who faces similar errors.

I emphasize the enterprise developer because it took about 15 minutes to get NodeJS, GruntJS, Bower and Yeoman working on my personal Windows 7 VM. Something in the enterprise domain environment confused NodeJS.

The PATH environment error occurred when trying to run grunt after installing grunt-cli.

> npm install grunt-cli
… everything downloads - no errors

Then

> grunt

grunt module.js:340
     throw err;
              

Error: Cannot find module '\\%USERPROFILE%\AppData\Roaming\npm\Roaming\npm\node_modules\grunt-cli'
     at Function.Module._resolveFilename (module.js:338:15)
     at Function.Module._load (module.js:280:25)
     at Function.Mdoule.runMain (module.js:497:10)
     at startup (node.js:119:16)
     at node.js:902:3
My Windows PATH: \\%USERPROFILE%\AppData\Roaming\npm

So it looks like Node is duplicating part of my PATH inside the cmdlet.

Opening \\%USERPROFILE%\AppData\Roaming\npm\node_modules\grunt.cmd in a text editor yields:

@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\Roaming\npm\node_modules\grunt-cli" %*
) ELSE (
  node  "%~dp0\Roaming\npm\node_modules\grunt-cli" %*
)
After removing the duplicated Roaming\npm from the else statement:

@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\Roaming\npm\node_modules\grunt-cli" %*
) ELSE (
  node  "%~dp0\node_modules\grunt-cli" %*
)
Running grunt again yields a new error:

> grunt
Yields another error:

The term 'grunt' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling o the name, or if a path was included, verify that the path is correct and try again.

At least we’re getting somewhere.

Here’s the structure of the grunt-cli folder. (At least for the parts we care about.)

**\\\\%USERPROFILE%\AppData\Roaming\npm\node_modules\grunt-cli\bin\grunt

Editing \\%USERPROFILE%\AppData\Roaming\npm\node_modules\grunt.cmd file once more to specify the grunt text file in that bin directory:

@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\Roaming\npm\node_modules\grunt-cli" %*
) ELSE (
  node  "%~dp0\node_modules\grunt-cli\bin\grunt" %*
)
And grunt works!

I had to make similar edits for Bower and for grunt-init. I expect to make more edits for any future globally installed node module.

For the record, the setup was:

node
v0.10.25

npm -v
1.3.24

git --version
git version 1.8.5.2.msysgit.0

systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
OS Name:      Microsoft Windows 7 Enterprise
OS Version:    6.1.7601 Service Pack 1 Build 7601

Hosted on GitHub. Generated by Jekyll.
--------------------------------------------------------------------------------------
