git
===


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
