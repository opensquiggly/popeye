# Project Status
THIS PROJECT IS NEW AND NOT YET READY TO BE USED.

# About Popeye
Popeye is an open source code search engine written in C#, inspired by the open source
project Zoekt, which is written in Go. We wanted something with similar functionality
that was written in C# so that we could better incorporate the technology into our projects.

Popeye uses the code search indexing library Spinach, which in turn uses the Eugene data
persistence library. Most of the functionalty exposed by Popeye comes from the core Spinach 
library. The difference between Popeye and Spinach is that Spinach is a .NET library that 
you can embed into your projects, whereas Popeye is an actual end-user product that you can 
install, run, and use.

Popeye also serves as a good showcase project that demonstrates how Eugene and Spinach can
be used in .NET projects.

# Roadmap & Development Plan
As of this writiing, Popeye is a nascent product and we're just starting to get the skeleton
in place to begin fleshing out the functionality. This section outlines the goals and plans
for developers that plan on contributing to Popeye.

## Goals
The goals of Popeye are as follows:

* Act as a simple showcase project for the Eugene and Spinach libraries.
* Popeye should also act as a showcase project for building code search tools and
  Internal Developer Portals using pure .NET and C#. We hope to help further the 
  usage of C# in the cloud-native world of tools. For this reason, we've decide to
  implement the front end web server in Blazor.
* It should be a clean, simple project with well-abstracted and readable code that
  developers can use or improve in their own projects. Popeye should provide just enough
  functionality to be a basic, useful regular-expression based code search engine, and
  nothing more.
* For those who are looking for more functionality than the basic code search features
  than Popeye implements, they can either contribute to the Popeye project by submitting
  pull requests, or they can fork Popeye and add their own functionality as-needed.
* Popeye should look and act remarkably similar to the existing Zoekt server hosted at
  cs.bazel.build.

## Initial Feature Set
For Iteration 0 and subsequent development towards an MVP, Popeye needs the following
features:

* A normal, familar project directory structure with a source folder, documentation folder,
  build pipelines, etc.
* Popeye should not have any process dependencies such as databases (MongoDB, Postgres, etc.),
  external search engines (ElasticSearch, Azure Search, etc.), other cloud services
  (Redis, RabbitMQ, etc.). Dependencies are embeddable libraries, NPM packages, etc., are fine.
* Accessing git repositories should be done either using the git command line tool or the
  LibGit2Sharp library.  
  It should run in a single self-contained Docker container. It should not require Docker Compose,
  Kubernetes, or any other multi-container orchestrator.
* Popeye should be cloud agnostic and not depend on a specific cloud provider. It should run
  equally well on AWS, Azure, Google Cloud, Digital Ocean, Linode, or any other cloud provider,
  or even on-premise.  
* Iteration 0 should include a Blazor-based web server UI that displays "Hello World" or some
  other simple proof-of-concept welcome message.
* The Blazor web server implemented in Iteration 0 should be able to be built upon with a 
  standard development workflow, culminating in a simple code search web server that looks
  very similar to https://cs.bazel.build.
* Notice that there is no login screen, user identity management, or AAA processes. Any user
  that can reach the URL where Popeye is hosted can search and view any of the source files
  that the Popeye instance manager has configured to index.
* Because there is no user identity management, it will be the responsibility of the Popeye
  instance administrator to install it in their cloud environment with appropriately restrictive
  firewall settings so that only allowed users can access the URL. The administrator should be
  mindful that any user which can reach the Popeye hosting URL will lbe able to search and view
  all source repositories that Popeye has indexed. It is an all-or-nothing thing. There are no
  facilities to provide fine-grained access per user or per-repository. We may address this after
  the MVP is built, but we are trying to keep the MVP requirements very simple so that we can
  develop the MVP quickly.  
* Indexing is configured by editing a YAML (or JSON) file by the Popeye instance administrator.
  The configuration file is read by the Popeye server when it starts. To add new source repositories
  to Popeye, the Popeye instance administrator will stop Popeye, edit the configuration file,
  and restart it.
* Popeye should be installable from a Docker file, on the customer's own cloud infrastructure,
  using a familiar workflow.
* Popeye should optionally be installable using Kubernetes and/or Helm, but this is not a 
  requirement for Iteration 0 or the MVP.
* We expect most users will be install Popeye on a Linux-based system, and therefore any necessary
  scripts needed to install would preferentially be written in Bash, though PowerShell scripts
  would be acceptable, Bash is preferred.
* Popeye should be as fast as possible within the boundaries of what Eugene and Spinach offer.
  It would be nice if Popeye could stream long results to the web browser so that users can see
  partial search results immediately, but this is not required. It would be nice if we can
  eventually demonstrate how a streaming code search engine could work.
* Popeye need only be a single-node solution through the MVP. After the MVP is built we may
  consider adding clustering capabilities either built into Popeye itself, or in a separate
  project that uses Popeye. If we do add clusting capabilities later, we will probably do so
  using either Orleans or Akka.NET. Our current development roadmap should be done with this
  in mind and attempt to be structured in a way that would make clustering possible in the future.
* In addition to a web UI, Popeye should provide a REST API for clients to use. As with the user
  identity manage, the REST API calls will not be authenticated and will happily serve data to
  any caller than can reach the URL.
* Past the MVP, we may consider adding GraphQL support.    

In summary, Popeye should be a simple veneer around the Spinach code search library that provides
the user with a simple but fast regular-expression based code search engine for their projects.
It provides a lightweight Blazor-based web server which showcases the Spinach functionality.        
