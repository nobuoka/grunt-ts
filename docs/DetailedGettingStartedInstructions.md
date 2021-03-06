# Detailed Getting Started Instructions

###Installing the prerequisites

Perform these steps once per computer:

 * Download and install Node.js from http://nodejs.org/
 * You will need a git client.  If you don't already have one, consider the clients for Mac or Windows from GitHub: https://mac.github.com/ or https://windows.github.com/
 * Once those are installed, you will need to download the Grunt command-line interface to allow access to the `grunt` command anywhere on your system.  Run this command: `npm install -g grunt-cli`
 
There are frequent updates to Node.js for functionality, performance, and security, so you should try to keep it up-to-date.  The GitHub for Mac and Windows clients will automatically patch themselves.  The `grunt-cli` package is just a stub that will launch whatever version of GruntJS is installed in your project folder, so it doesn't typically need updates.

###Configuring a project for grunt-ts

Perform these steps once per project:

 * Ensure that your project is completely checked-in to source control or backed-up.  Consider starting a new branch in your source control system for this work.
 * Open a command-line and navigate to your project folder.  Run `npm install grunt-ts` .  This will download grunt-ts, Grunt, and TypeScript from npm.
 * Look for a file called `gruntfile.js` in your project.  If it's not there, create it and add the code below.  If it is there, follow the instructions in the note:

````javascript
module.exports = function(grunt) {
  grunt.initConfig({
    ts: {
      default : {
        src: ["**/*.ts", "!node_modules/**/*.ts"]
      }
    }
  });
  grunt.loadNpmTasks("grunt-ts");
  grunt.registerTask("default", ["ts"]);
};
````
 * **Note:** If you already had a `gruntfile.js`, you'll still need to make at least three edits to it.  First, add the `ts` property to the existing initConfig() call (separate from existing properties with commas).  Next, add the line to load the grunt-ts task (`grunt.loadNpmTasks("grunt-ts");`).  Finally, ensure `ts` is listed in your default task or whichever tasks you wish to use.  All calls to `grunt` need to be within the braces `{ }` of the function where grunt is getting passed-in.
 * This basic gruntfile uses the `default` task (which is selected if you run `grunt` from the command-line with no arguments).  We've set the `src` property of the `ts:default` task to a "glob" array.  Grunt globs allow the developer to select files that the task should act on.  In this case, we are selecting all files with a `.ts` extension in the project root folder and any subfolders, excluding (`!` means exclude) any `.ts` files in the `node_modules` folder.
 * If you run `grunt` from the command line, all `.ts` files in your project folder and all subdirectories will be compiled.  If you wish to further customize what happens, you'll have to edit the gruntfile appropriately.  See the rest of the documentation for instructions.