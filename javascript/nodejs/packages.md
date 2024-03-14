# Packages

It is not productive to create everything from scratch. To increase productivity, **NodeJS** provides a mechanism to re-use previously written code. Such code is called a **package**. **Packages** can be installed via a commandline utility called **NPM**.

**Packages** can be installed either _Global_ or _local_. _Global_ **packages** are installed on the machine and can be used from the command line or by all _Node apps_ from that single installation. _Local_ **packages** are installed with each _Node app_ and cannot be used by other _Node apps_.

When a _Node app_ uses a **package**, it is called a _dependency_. This means that the _Node app_ _depends_ on the **package** in order to function properly. **Packages** can also use other **packages** as _dependencies_. **Packages** have _version numbers_. A _version number_ indicates a specific iteration of code or features that the **package** supports. When a _Node app_ _depends_ on a specific _version_ of a **package**, it avoids protentional problems and _conflicts_ that might arise if there was no _versioning_ in place. A _conflict_ is when the _Node app_ expects a certain feature or behavior that does not exist, or behaves differently than expected.

#### To install a package:

**NodeJS** provides a utility called `npm` that manages **packages**. With it you can install and remove **packages** easily.

Each application should have a `package.json` file in its root directory. This file does not exist by default and must be created. To create it, simply type:

`npm init` at the application root directory and follow the prompts. To add a **NodeJS** package, simply type:

`npm install <name> --save` at the application root directory.

You can also remove a package via:

`npm remove <name>` at the application root directory.

When you get a _project_ from GitHub the first time, it will usually contain the `package.json` file already. But the **packages** will usually not be included with the git repository. The **packages** will be listed in the `package.json` file. To install all the **package** dependencies, simply type:

`npm intall` at the application root directory.

Some **packages** will behave more like applications and others more like functionality for YOUR _Node app_. Those that behave more like applications (or utilities) must be installed _globally_ and those that provide functionality as a part of YOUR _Node app_ must be installed _locally_. To install a _global_ **package**, simply type:

`npm install -g <name>` anywhere.

#### Exercises:

* Create a new _Node app_. Add a `package.json` file
* What is the purpose of the `main` key/value in the `package.json` file?
* Install at least one **package** to the _project_
* What happens if you omit `--save` when installing a **package**?
* Install at least one **package** that is specific to the dev dependencies (HINT: testing usually will be dev specific (as in development, vs deployed to the end users and ready to use))
* Remove at least one **package** from the _project_
  * Validate that `package.json` reflects the change. If not, figure out why and try again
* Install a specific _version_ of a package to the _project_
* What directory does NPM install _local_ **packages** to?
* What happens if you install a **package** at a different directory level than the application root directory?
* How can you avoid uploading **package** files to github? (HINT: git.ignore... but how, specifically?)
* Install a _global_ package (`Nodemon`??)
* Can a _global_ **package** be a _dependency_ to your _Node app_? Explain why or why not?
* Launch your **NodeJS** app using the dev configuration.
