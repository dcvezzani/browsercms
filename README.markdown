# BrowserCMS: Humane Content Management for Rails

BrowserCMS is a general purpose, open source Web Content Management System (CMS) that supports Ruby on Rails v3.2. It can be used as a standalone CMS, added to existing Rails projects or extended using Rails Engines. It is designed to support three distinct groups of users:

1. Non-technical web editors who want a humane system to manage their site, without needing to understand what HTML or even Rails is.
2. Designers who want to create large and elegantly designed websites with no artificial constraints by the CMS.
3. Developers who want to drop a CMS into their Rails projects, or create CMS driven websites for their clients.

## Features
BrowserCMS is intended to offer features comparable to commercial CMS products, which can support larger teams of editors. This means having a robust set of features as part of its core, as well as the capability to customize it via modules.

Here's a quick overview of some of the more notable features:

* Stanealone CMS: BrowserCMS is designed to provide a robust CMS capabilities out of the box for content heavy web sites.
* Mobile Friendly: Sites can be built to use mobile optimized designs that are optimized for small screens, with low bandwidth, with responsive design.
* In Context Editing: Users can browse their site to locate content and make changes from the page itself.
* Design friendly Templates: Pages aren't just a template and giant single chunk of HTML. Templates can be built to have multiple editable areas, to allow for rich designs that are still easy to manage by non-technical users.
* Highly Extensible: Developer have access to the full Rails development stack, and can customize their project by adding their own controllers, views as well as CMS content types.
* Sitemap: An explorer/finder style view of sections and pages in a site allowing users to add and organize pages.
* Content Library: Provides a standardized 'CRUD' interface to allow users to manage both core and custom content types.
* Content API: A set of behaviors added to ActiveRecord which allow for versioning, auditing, tagging and other content services provided by the CMS.
* Section Based Security: Admins can control which users can access specific sections (public users), as well as who can edit which pages (cms users).
* Workflow: Supports larger website teams where some users can contribute, but not publish. Users can assign work to other publishers to review.
* Page Caching: Full page caching allows the web server (Apache) to serve HTML statically when they don't change.
* CMSify your Rails App: BrowserCMS can be added to existing Rails applications to add content management capabilities.

## Getting Started
See the [Getting Started](https://github.com/browsermedia/browsercms/wiki/Getting-Started) guide for instructions on how to install and start a project with BrowserCMS.  If you have a Rails project already, you may consider simply [adding BrowserCms to your project](https://github.com/browsermedia/browsercms/wiki/Adding-BrowserCMS-to-an-existing-Rails-project) instead.

## Cloning the Branch
At this time, do not use master to develop enhancements for BrowserCms.  Please use the '3.5.x' branch.

    git clone -b 3.5.x git@github.com:dcvezzani/browsercms.git

## Configuring the Test Environment
To get the tests to pass (for this fork, at least), you will need to configure your RVM to include two gemsets.  Assume you have already installed BrowserCms, you want to add some enhancements to the BrowserCms project and you are currently in the browsercms fork (the directory being labeled 'browsercms').

    # install if it's not already there
    rvm use ruby-1.9.3-p327

    rvm gemset create rails309
    rvm gemset create rails310

    rvm gemset use rails309
    gem install --version "3.0.9" rails

    rvm gemset use rails310
    gem install --version "3.1.0" rails

    # this should restore the configured gemset for the browsercms project
    cd ../browsercms

If development efforts are taking place, it's more convenient if we can work with an unpacked browsercms gem that we don't have to 'gem install' over and over again.  This, however, has the drawback that we can't take advantage of rvm gemsets to ensure that we are using the correct ./bin executable, no matter where we are on our development system.  One way this can be handled is by generating Bundler binstubs and telling our tests where to find them.

    bundle install --binstubs

The Cucumber tests use Aruba to test command line calls (CLI).  They are the only tests that will be making calls to bcms.  The Cucumber configuration (features/support/env.rb) takes care of this for us.  If binstubs are there, they will be used (e.g., ./bin/bcms); if not, calls to bcms will be handled by RVM which will not adequately test BrowserCms and the enhancements being worked on in the fork.

### Running the Tests
Once the configuration is in place, the tests can be run.  Assuming testing will be done using sqlite3 (which is how the Gemfile is currently configured),...

    # run tests on browsercms proper (for the first time)
    ./bin/rake ci:test

    # run tests on browsercms proper for subsequent times
    ./bin/rake test

    # run all cucumber tests
    ./bin/cucumber

    # run a single cucumber test
    ./bin/cucumber -r features features/commands/generate_module.feature

    # checkout other testing options
    ./bin/rake --tasks

## License
BrowserCMS is released under a LGPL license, and is copyright 1998-2013 BrowserMedia. The complete copyright can be found in COPYRIGHT.txt, and copy of the license can be found in LICENSE.txt.

## Documentation / Support
The user documentation and guides for this version of the application can be found at:

1. [Guides and Wiki](http://wiki.github.com/browsermedia/browsercms)
2. [API Docs](http://rubydoc.info/gems/browsercms/)
3. [Report a Bug!](https://github.com/browsermedia/browsercms/issues)
4. [Discuss the Project](http://groups.google.com/group/browsercms)
5. [BrowserCMS Site](http://browsercms.org)
