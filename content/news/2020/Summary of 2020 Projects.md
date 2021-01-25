---
title: "Summary of 2020 Projects"
date: 2021-01-24T08:30:00+08:00
author: Alyssa Parado
summary: Read more about all the projects we funded in 2020
draft: true
---

# 2020 Summary of Projects


## Calva

* Version 2.0.75 released
  - [Support cljs-suitable JavaScript completion](https://github.com/BetterThanTomorrow/calva/issues/552)
  - [Fix Printing to Calva REPL prints <repl#7> before each print out](https://github.com/BetterThanTomorrow/calva/issues/548)


* Version 2.0.76 released
  - [Fix Calva locking up when opening files with very long lines](https://github.com/BetterThanTomorrow/calva/issues/556)


#### Configuration of Formatting

Calva's formatter can now be configured to support different formatting policies - a big thanks to [nbardiuk](https://github.com/nbardiuk). This is something users have been asking for, and we're excited to offer it now! See [this post](https://clojureverse.org/t/calva-gets-configurable-formatting/5596) for more information.


#### Docs

The [Calva docs](https://calva.io/) have a new look and a new home! We switched to using mkdocs for building our docs and are using the material theme.

#### Debugger

The debugger has been released! [Documentation for the debugger](https://calva.io/debugger/) was written and published that covers the existing functionality and lists current and upcoming features.

I've added a command to instrument functions for debugging as an alternative and more convenient method than adding `#dbg` reader tags to the code file. I've also added editor decorations to visually indicate which functions are instrumented. The instrumented function definitions as well as the usages gain a top and bottom border and a background. clj-kondo is used [as a JVM library](https://github.com/borkdude/clj-kondo/blob/master/doc/jvm.md#api) to get the var definitions and usages, and [this data](https://github.com/borkdude/clj-kondo/tree/master/analysis) is matched up with cider-nrepl's [`debug-instrumented-defs`](https://docs.cider.mx/cider-nrepl/nrepl-api/ops.html#_debug_instrumented_defs) response data to create the decorations on document change.

The instrument command and decorations features were released and I've started working on displaying structured values, for locals, in the VS Code debugger side pane (currently non-primitives are shown as strings). This should allow a user to "drill down" into a structured value like a map or collection.





## Fireplace

* Retool `:Eval` to support streaming response.
* Implemented sending text to stdin.
* Implemented eval backgrounding.  Press CTRL-D during any interactive eval to
  detach from it and continue using Vim.  The results will open in a preview
  window when finished.
* Implemented a variation of jump to definition that works with Vim's tag stack.
  <https://github.com/tpope/vim-fireplace/issues/304>
* Fixed evaluation with babashka.
  <https://github.com/tpope/vim-fireplace/issues/375>
* Documented asynchonous evaluation.
* Provided simple stacktrace filtering.
  <https://github.com/tpope/vim-fireplace/issues/362>
* Automatically update :Last buffer.
  <https://github.com/tpope/vim-fireplace/issues/297>
* Fixed Neovim nested callback issue.
  <https://github.com/tpope/vim-fireplace/issues/378>
* Supported shadow-cljs in salve.vim.
  <https://github.com/tpope/vim-fireplace/issues/322#issuecomment-696945856>
* Phased out internal use of old APIs.





## Reagent

Some of the fixed tests were related to how Reagent added component stack
information into the error essages, which was retrieved from React class component internal properties.

React now provides a proper way to get the component stack information for errors
using Error Boundaries.


I created Reagent 0.10.0 release. This version marks the functions deprecated,
so library authors have some time to fix calls before functions are removed.



Related to the functional render feature, I implemented first version
of providing options to Reagent. This way existing applications can keep
using the old implementation and Class components, and allow users to choose
if they want to try functional components. Additionally a custom component
can be added, which can be used to control per form if Class or functional
component is created. 

Improved the documentation and examples, and added code coverage reporting to CI and Github.


Reagent 1.0.0-alpha1 is out and contains implementation of both
creating React function components from Reagent components
and options.

I added some new documentation pages
and a new example showing making Function components default
and using Hooks with Reagent, and created the first release for testing.

Based on the comments from users, I've already added
two more "shortcuts" to Reagent: `:f>` to create
Function Reagent component (using the default
options), and `:r>` to use React
components without properties conversion done by
`:>` and `adapt-react-class`.

added new test environment for Reagent, using the
new `:bundle` compilation target. This target generates
JS tooling compatible output. This output can be passed to
Webpack, or for testing, Karma.


#### General bug fixes

During implementation of functional components, I've also merged some
previously implemented changes to master, and refactored test checks
to provide better failure messages.





## Ring


The [ADR](https://github.com/ring-clojure/ring/blob/2.0/doc/adr-spec-2.md) for Ring 2.0 has been completed


The servlet interop functions and Jetty adapter have been updated to
support the Ring 2.0 request and response formats. 

Fixed various smaller issues with Ring 1.8.0
 
Ring 2.0.0-alpha1 has been released, with the adapter and servlet
utility functions supporting both Ring 1 and Ring 2 keys by default,
though there is also an option for forcing a particular version.





## Cider

#### nREPL:

* Implemented an initial version of the built-in code completion middleware
* Reviewed and merged dynamic middleware loading functionality
* Provided default print functions via `nrepl.util.print`.
* Implemented an initial version of the build-in lookup middleware and fixed handling of aliased symbols in lookup middleware
* added var type to completion candidates
* cut nREPL 0.8.0-alpha1 
* Issued several alphas including small fixes to the new lookup and completion logic.
* Released nREPL 0.8 (https://metaredux.com/posts/2020/06/15/nrepl-0-8-evolving-the-protocol.html)
* Extended the nREPL docs on building new middleware (https://nrepl.org/nrepl/building_middleware.html)


#### cider-nrepl:

* Normalized the interface of several ops by making the params they accept consistent
* Cut a new release (0.25)
* Issued to a bug-fix release that workarounds an incompatibility between clj-suitable and shadow-cljs 2.10.
* Released cider-nrepl 0.25.3 (mostly to address the complaints about downloading the ClojureDocs export automatically)


#### Piggieback:

* Cut Piggieback 0.5 with pprint support


####  CIDER:

* Added support for the new nREPL completions op
* Fixed a couple of long-standing bugs related to streamed printing in the REPL (https://github.com/clojure-emacs/cider/issues/2628 and https://github.com/clojure-emacs/cider/issues/1971)
* Make it possible to configure the print buffer size that nREPL uses via CIDER
* Reviewed and merged some inspector improvements
* Added a couple of small command (e.g. `cider-repl-toggle-clojure-font-lock`) and made many documentation improvements including some new page navigation
* Improved the behavior of commands based on `cider-jump` (https://github.com/clojure-emacs/cider/issues/2850)
* Fixed eldoc on Emacs 28.1. 
* Improved support for Babashka.
* Fixed a couple of small bugs with REPL warning messages.
* Did some work towards making CIDER a bit Clojure-agnostic, so it's easier to use it with flavours of Clojure and other programming languages.
* Fixed eldoc for `.` and `..`.
* Merged and polished REPL auto-trimming functionality (https://github.com/clojure-emacs/cider/pull/2857).
* Implemented initial support for sideloading.
* Released CIDER 0.25 and 0.26 ("Nesebar") (https://github.com/clojure-emacs/cider/releases/tag/v0.26.0)
* Polished the sideloading functionality (have user and system sideloading, add better docs)


#### inf-clojure:

* Released inf-clojure 3.0 (no new functionality, but massive improvements to the internals)



Orchard:

* Merged a fix for #86 that fixes the resolution order in the info function
* Cut new releases (0.5.9), (0.5.10), and (0.5.11)


Misc:

* Fixed a deployment issue with the clojuredocs-edn-export tool (it generates data that orchard uses)
* Helped with adding print middleware support to shadow-cljs
* Helped with adding eldoc support to babashka.nrepl
* Specified docs license (https://github.com/clojure-emacs/cider/issues/2740)
* Fixed a dependency bug in Orchard and cider-nrepl (https://github.com/clojure-emacs/orchard/issues/91)
* Bundle clojuredocs export with Orchard and cut version 0.6 (this eliminates the need to delete the data on demand when starting CIDER)
* Fixed cider-mode not being auto-activated for babashka (https://github.com/clojure-emacs/cider/issues/2882)
* Merged Krell REPL support (https://github.com/clojure-emacs/cider/pull/2861)
* Fixed an init bug when using babashka (https://github.com/clojure-emacs/cider/issues/2882)
* Made connection-info babashka/generic nREPL server aware (https://github.com/clojure-emacs/cider/pull/2883)
* Added cider-eval-list-at-point for evaluating code between paired delimiters (lists, vectors, etc)





## Figwheel

* Created some integration [testing](https://github.com/bhauman/figwheel-main-testing) for figwheel-main to track if new releases of ClojureScript break any of the main features.

	These tests launch figwheel and then touch various files to ensure
correct loading in terms of load order and files included in the
reload.

	These tests append various errors to files to ensure the correct error
messages show up as well.

* Got both lein-figwheel and figwheel-main working with the latest CLJS :bundle target

	The new :bundle target is an important improvement in the CLJS
compiler that provides better support for NPM dependencies in web
projects.

	* Updated the Leiningen template for lein-figwheel.

 		- The template now generates a project that supports the new `:bundle` target. One can generate the standard figwheel project by adding a `+no-bundle` option on the command line.
		- Improved the templates CLI option parsing and removed `om` as a generated framework.
* Added the new Figwheel logo and updated the website style of the [Figwheel website](https://figwheel.org)
* Improved the `:bundle` target support in [figwheel-main](https://figwheel.org).
	- This was reflected in the `com.bhaumsn/figwheel-main 0.2.7` release and the newly updated [documentation for working with NPM](https://figwheel.org/docs/npm.html).
* Refactored RNFB and added support for `expo`
* Removed [Devcards](https://github.com/bhauman/devcards) dependence on `js/React` global
* Implemented a `--clean` command which makes it easier to clean your compiled artifacts out of your project.
* Created the [`certifiable`](https://github.com/bhauman/certifiable) library to ease the creation of a local dev certificate and Java Keystore. This should enable `figwheel-main` to have turn-key HTTPS support.
* Added cleaning to `figwheel-main`.  You can either add the `--clean` to your CLI options or or `:clean-ouputs true` to your Figwheel options. 
	- This will clean all of your builds compilation output including generated bundles AND all of the compiled output from and extra-mains that you have configured as well.
* Added a new [`:ssl-valid-hosts`](https://figwheel.org/config-options#ssl-valid-hosts) option will let you configure which hostnames and ips the generated certificate considers valid.
* Completed React Native support. This supports React Native Expo CLI as well.
	- The minimal configuration for a React Native project in `figwheel.main` is now:


      ^{:react-native :cli}
      {:main example.main}

* Released `figwheel.main 0.2.10`
* Fixed bug introduced by a refactor that broke `:connect-url` this
  has been deployed to 0.2.11
* Added a tutorial/doc on how to use Nodejs with Figwheel





## Practicalli

#### Practicalli Study Group

* Provided the weekly live broadcasts, data science series and a new series on `clojure.spec`
* Developed content for Practicalli Clojure and Practicalli Clojure Webapps books.


#### Visualising data science

Concluded the [series of 7 live broadcasts on Visualising data science](https://www.youtube.com/playlist?list=PLpr9V-R8ZxiDUXIR2z8Y8wvhpoPyl0t_D).


#### Introduction to clojure.spec.alpha

* Started a new video series covering how to use spec in the REPL and with Clojure projects

* [Practicalli/leveraging-spec](https://github.com/practicalli/leveraging-spec) project was created, covering Clojure predicates, spec/conform, spec/valid?, literal values (Clojure sets), the spec registry, fully qualified namespaces, map literal syntax, spec/def and spec/explain.


#### Practicalli Clojure

Migrated the book to Clojure CLI tools and deps.edn projects.

Updated install guide to use Java 11 and added more editor options to the install guides, including NeoVim Conjure and Atom.io Chlorine.

Updated the [practicalli/clojure-deps-edn](https://github.com/practicalli/clojure-deps-edn) repository with also contains a collection of commonly used aliases.  This repository greatly simplifies the installation of Clojure CLI tooling.

Added content and videos to the [Introducing Spec section](http://practicalli.github.io/clojure/clojure-spec/) of the book

Added details on configuring tools.deps and how to define and use multiple aliases. Provided a collection of aliases for community tools, jcenter clojars mirror and how to use a local Artifactory instance.

[Configuring a REPL on starutup for deps.edn projects](https://practicalli.github.io/clojure/repl-driven-development/configure-repl-startup.html), examples of using `dev/user.clj` to require namespaces, call functions and manage component lifecycle services (mount, component, integrant, etc.).

Extended the Unit Testing section to cover useful practices with clojure.test library, refactor is assertions with are to work over data sets.

Configured git template to use live branch as the default branch name.

Created [an introduction to CircleCI as a continuous integration service](http://practicalli.github.io/clojure/testing/integration-testing/circle-ci/random-clojure-function.html) and identified and documented recommended docker images to use for Clojure deps.edn and Leinigen projects. 

Configure REPL startup using `dev/user.clj` file and `:dev` alias in practicalli/clojure-deps-edn configuration.

Add section on [data browser tools](https://practicalli.github.io/clojure/clojure-tools/data-browsers/), extending REBL and Clojure Inspector with new projects Reveal and Portal.



**Random Clojure Function project**.
Created a guide to develop a project that [generates a random function](http://practicalli.github.io/clojure/simple-projects/random-clojure-function.html) from the namepaces available in the REPL or the functions from specified namespaces.

Using the [random Clojure function project](http://practicalli.github.io/clojure/simple-projects/random-clojure-function.html), created a [guide to develop a project with the help of CircleCI](http://practicalli.github.io/clojure/testing/integration-testing/circle-ci/random-clojure-function.html) as the continuous integration service.


**Banking on Clojure**
Updated the [banking-on-clojure project](http://practicalli.github.io/clojure/clojure-spec/projects/bank-account/) using a TDD approach with Clojure spec.



#### Practicalli ClojureScript

Clarified the introduction to the ClojureScript book status and surfaced the work that remains current and functional. This content includes and several reagent based projects, building and deploying a ClojureScript website for ClojureBridge and creating a TicTacToe game with Scalable Vector Graphics.


#### Practicalli Spacemacs

Supported the community with issues on Spacemacs gitter and #spacemacs channel of Clojurians Slack.

Several updates on using the Magit client including guide on using Magit Forge, updated and tested the Magit Forge configuration page and more. 

[Practicalli Spacemacs playlist](https://www.youtube.com/playlist?list=PLpr9V-R8ZxiCHMl2_dn1Fovcd34Oz45su) updated with related Spacemacs videos from jr0cket channel.

Created a reference sheet for CIDER configuration variables, as there is no overall reference.

Add Emacs profiler use to the [Spacemacs troubleshooting guide](https://practicalli.github.io/spacemacs/install-spacemacs/troubleshooting.html)



#### Hacking on Spacemacs

Added key bindings to refactor namespace forms in clojure-mode

Updated [practicalli/.spacemacs.d](https://github.com/practicalli/spacemacs.d/) repository with doom modeline configuration.


#### Spacemacs Pull Requests

Refactor applications menu key bindings to create more room for key bindings and improve mnemonic keybinding use.  


#### Practicalli Clojure WebApps

Refactored overall book content design for Practicalli Clojure WebApps

Created [a guide to deploy a Clojure application via CirceCI onto Heroku](https://practicalli.github.io/clojure-webapps/projects/status-monitor-deps/). 

Updated the status monitor project to deps.edn to use as the basis for a guide to deploy Clojure applications via CircleCI to Heroku (a cloud platform as a service).

Updated details of using postgresql with Clojure (documentation will be extended soon) and recommended next.java as a library to use for SQL.

Started a section on [Application servers](https://practicalli.github.io/clojure-webapps/app-servers/), covering approaches to server configuration and server start/stop/reload.

Started a section on Databases that will initially cover H2 and Postgresql relational databases, using Sql with next.jdbc



#### Practicalli Website

Added [Shields](https://github.com/badges/shields) for each book with links to content ideas and pull requests on the respective repositories. 

Added Practicalli website and YouTube channel to the [Clojure.org community resources](https://clojure.org/community/resources).

Updated the Creative commons license notice on the front pages of all books and GitHub README files, ensuring compliance with the [Software Freedom Conservancy](https://sfconservancy.org/).

Add favicon to each book website


#### Clojure deps.edn updates

* Using REBL from Emacs CIDER using nREBL middleware, alias and configuration
* Update of dependency versions in the `deps.edn` file with depot
* Update unit testing aliases, add separate expectation aliases.
* Added more tools to practicalli/clojure-deps-edn
Any experimental or alpha state tools are clearly marked as 'experimental - used at own risk' to set clear expectations.

Added Google Storage mirrors for Maven Central for Americas, Asia and Europe to library repository configuration.  Also added a community mirror in Asia (China) for Clojars.





## Re-frame

* Reviewed and triaged all existing open issues and Prs.
* Released a stable v1.0.0 version of re-frame
* Many improvements to the docs have been made. Too many to mention but some are notable:

  - added a new FAQ on [laggy input](https://day8.github.io/re-frame/FAQs/laggy-input/)
  - added a new FAQ on [field focus](https://day8.github.io/re-frame/FAQs/FocusOnElement/)
  - added to existing FAQ on [global interceptors](https://day8.github.io/re-frame/FAQs/GlobalInterceptors/#answer-v100-onwards)
  - Additions made to [External-Resources](https://day8.github.io/re-frame/External-Resources/)
  - completely reworked [Infographics for Dominoes 1,2 3](https://day8.github.io/re-frame/event-handling-infographic/)
  - completely reworked [Infographics for Interceptors](https://day8.github.io/re-frame/Interceptors/#infographics). See also other explanations added to that tutorial. 



