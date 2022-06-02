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
├── node_modules (omitted ...)
├── package.json
├── package-lock.json
├── shadow-cljs.edn
└── src
    ├── main
    └── test
```

2. Delete test and rename main to the name of your project. Then create a frontend and backend folder inside src/<projectname> and inside your frontend, create a core.cljs file with an namespace `(ns projectname.frontend.core)`. This step will be very important later. 
   
3. Your shadow-cljs.edn will be pretty bare out of the box, like the code below:
   
