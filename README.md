# pga2d

An experiment to implement 2D geometric algebra in ClosureScript.

## Overview

We (Mark Phillips and I) are just beginning.

## Setup

### Using IntelliJ/Cursive

This project is set up for use with Cursive, the IntelliJ plugin for
Clojure(Script) development.  To open the project with Cursive, from
within Cursive choose Open (NOT "Create New Project" or "Import
Project"), and navigate to the directory containing the project.

If this is the first time you have used Cursive with a ClojureScript
project on this computer, you will also need to create a clojure.main
Cursive REPL configuration.  The steps for doing this are:

* Click **Run->Edit** configurations.
* Click the + button at the top left and choose **Clojure REPL**
* Choose a **Local REPL**
* Enter a name in the **Name** field (e.g. "REPL")
* Choose the radio button **Use clojure.main in normal JVM process**
* In the **Parameters** field put `script/repl.clj`
* Click the **OK** button to save your REPL config.

More details are available at
https://github.com/bhauman/lein-figwheel/wiki/Running-figwheel-in-a-Cursive-Clojure-REPL
.


### From the Command Line

To get an interactive development environment run:

    lein figwheel

and open your browser at [localhost:3449](http://localhost:3449/).
This will auto compile and send all changes to the browser without the
need to reload. After the compilation process is complete, you will
get a Browser Connected REPL. An easy way to try it is:

    (js/alert "Am I connected?")

and you should see an alert in the browser window.

To clean all compiled files:

    lein clean
    
    
## Creating a Production Build
    
By a "production build" we mean a collection of files that you can
generate on your development machine which can then be put on a web
server, and/or viewed in a browser.  No ClojureScript compiler or
other tools are needed on either the server or in the browser -- a
production build consists of a collection of plain HTML, JS, and CSS
files; these files can be deployed to any web server and viewed in any
reasonably modern web browser.  A production build does NOT include a
REPL or hot code reloading.

The default "main" program is the file src/pga2d/test.cljs.  To create a 
To create a production build of this file, run the command:

    lein cljsbuild once min
    
Then open the file `resources/public/index.html` in your browser.  If
you want to deploy the results to a web server, deploy the entire
"resources/public" directory to the server.

### Creating an Alternate Production Build ("New Diagram")

You can also create an additional "main" program in the project and set
up an alternate build target and corresponding HTML file for it, so that
you can create, maintain, build, and deploy multiple separate programs from
this same project.  To create a new "main" program named "myprog", for example,
do the following

1. Edit the file `project.clj` to find the section that looks like:

   ```clj
   {:id "diagram1"
    :source-paths ["src"]
    :compiler {:output-to "resources/public/js/compiled/diagram1.js"
               :main pga2d.diagram1
               :optimizations :advanced
               :pretty-print false}}
   ```

   Copy/paste this section to create a duplicate of it, and change all
   occurences of "diagram1" to "myprog".
   
2. Copy the file `src/pga2d/diagram1.cljs` to `src/pga2d/myprog.cljs`, then
   edit it to create your new program.  Be sure to change the name in the
   `ns` call at the top from "pga2d.diagram1 to "pga2d.myprog'.
   
3. Copy the file `resources/public/diagram1.html` to `resources/public/myprog.html`,
   and edit it to change all occurences of "diagram1" to "myprog" (there should
   only be one, near the end of the file).
   
4. Run the build with the command   

   ```
   lein cljsbuild once myprog
   ```
    
5. Open the file `resources/public/myprog.html` in your browser.  If
   you want to deploy the results to a web server, deploy the entire
   "resources/public" directory to the server.
