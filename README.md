# DadCast: When you're New Balances just aren't white enough.

Dadcast is a new project where I can better develop my full-stack clojure skills. I also think it's a dope name for a podcast, so you can look out for it in the apple podcast store within the next 5 to 10 business years.

### What the project does and why it is useful: 

Not quite sure at the moment. Twitter clones are always a good place to start, but this could also just be a silly website. It usefulness is not for the user currently, it's just for me.

### Getting Started

##### Prerequisites: 
1. Knowledge of clojure syntax
   - If you are not familiar, I suggest reading **_AND CODING_** through chapters 3-5 of 
     [Clojure for the Brave and True](https://www.braveclojure.com/do-things/).

##### Tools:
1. Shadow-cljs
   - [Shadow CLJS User's Guide](https://shadow-cljs.github.io/docs/UsersGuide.html#_deps_edn_tools_deps) 
   - [Condensed Guide](https://github.com/thheller/shadow-cljs)
2. Clojurescript/Reagent 
   - [Reagent Tut](https://reagent-project.github.io/)

   
##### Actually Getting Started:

1. Running `npx create-cljs-project <projectname-app>` in the terminal will set up a directory with the following files:
```
├── node_modules/
├── src/
|   ├── main
|   └── test
├── package.json
├── package-lock.json
└── shadow-cljs.edn
```

2. Delete the `:test` folder for now, then create a `:app` folder inside `:main`. Finally, create a core.cljs file with an namespace `(ns main.app.core)` insi`de of `:app`. I'll explain why we do this in a second.
   
3. Your shadow-cljs.edn will be pretty bare out of the box, but it actually has everything you need. It will give you a template with `:source-paths` and `:dependencies` vectors, as well as a `:builds` map. There are many ways to fill in this template. Below is an example of a simple browser-based build: 
```clojure
;; shadow-cljs configuration
{:source-paths
   ["src"]
   
 :dependencies
   [[reagent "1.1.1"]]
   
 :builds
   {:app 
      {:target :browser
       :output-dir "public/app/js"
       :asset-path "app/js"
       :modules {:main {:enteries [main.app.core]}}}}}
   ```

###### The Class Path
"`shadow-cljs` uses the Java Virtual Machine (JVM) and its "classpath" when working with files." [(1.3.1)](https://shadow-cljs.github.io/docs/UsersGuide.html#_the_classpath). When the JVM is compiling it's classpath, it will first take a look at your `:source-paths` to determine where the files are that it needs to compile, and if it can't find the file there, then it will search in `:dependencies`. For example, if your build entry is `[<projectname>.frontend.core]`, then the JVM is going to look at your `:source-path` for which folder to start looking in. Then it will filter through until it finally reaches `src/<projectname>/frontend/core.cljs`. If it does not find that in the offered `:source-path`, it will look elsewhere.
Machines don't know what you mean. The JVM does not understand what you meant to say, only what you said, so your namespaces are very important.
   
###### Builds
A build is a file of compiled code. We are using this section to nudge the JVM compiler in the right direction. 
Looking at the `:builds` section of the code above we first see the name of this build, `:app`. All the things underneath that are called [compiler options](https://clojurescript.org/reference/compiler-options). I recommend looking at [section 6.6](https://shadow-cljs.github.io/docs/UsersGuide.html#compiler-options). 

- The `:target` is where you want the compiled code to go. 
- `:output-dir` defaults to `"public/js"`, but you can specify otherwise. 
- Your `:asset-path` should match your `:target` directory minus the root. 
  - example: `:output-dir`  is `"public/app/js"`, then your `:asset-path` should be `"app/js"`.
- [`:modules`](https://shadow-cljs.github.io/docs/UsersGuide.html#_modules) is used when you are [targeting the browser](https://shadow-cljs.github.io/docs/UsersGuide.html#target-browser). 
  - inside of that is `:main` which will generate `main.js` in your `output-dir`. Can confirm that `:cheese` will create a `cheese.js` file. 
    - finally, `:entries` will be your root node, or entry file into this whole mess. 

This can get way more complicated depending on the build you need and what you need to optimize it for, but we can worry about that later. 

   4. Now that all of this is setup, run `npx shadow-cljs watch :app` and it will create a serverfor you and give you a port number to see your code in the browser. This will also create a `public/` folder, go into that foler and add and `index.html` file, kill the server, then restart it. Then you should be all set to go out and create. 
