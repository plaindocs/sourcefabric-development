.. _git:

Git repositories
================

At Sourcefabric we use Git to manage source code. You can find all official 
Git repositories hosted in GitHub at
`https://github.com/sourcefabric/ <https://github.com/sourcefabric/>`_.


.. admonition:: Usage in production

   If you want to deploy a product in a production environment we highly 
   recommend getting an official release package instead of using the 
   development version. 

The branching model we follow in Sourcefabric is simple. There are three 
different types of branches:

* main development branch, `master`: the base for all development. Every 
  time you start working on something new, you should do it based on
  `master`. Major releases are based on `master`.
* release branches: officially supported versions of the product are kept in
  release branches for maintenance. 
  
  - If you want to contribute a fix to a bug that affects any of the supported 
    released versions, you should add it to the corresponding release branch. 
  - When a release is no longer supported, the release branch is removed from 
    the repository.
  - NO new features are ever added to a release branch.
  - A release branch triggers always and in all cases the next minor release only.
  - Whenever a release needs to happen, a new release branch is created branching
    off `master`, and when doing so ALL new features added since the last release
    will be part of the new release, this means you cannot cherry pick which
    features will make the new release.


* feature branches: when a new major feature or improvement is being done,
  likely work happens in a feature branch to not affect `master` directly.

  - Lifetime of feature branches goes from the moment where the implementation
    begins till the moment when the branch is merged back to `master`. Once that
    happens the feature branch may be removed from the repository.
  - A feature branch never triggers a release. Features are always merged back to
    `master` in order to be released.
  - Branch naming convention: <Jira Ticket Code>-<Short Descriptive Title>, where
    <Short Descriptive Title> must be in lowercases and must use the dash sign “-”
    as word separator (e.g. cs-2764-autosave).

Released Versions
-----------------

Officially released versions are available in the form of Git tags. Every time a
new version is released, a new Git tag is created, using the following naming
convention:

v<Version Number> (e.g. v4.0.0, v2.1.1-RC2)

You can see the list of released tags by checking:
https://github.com/sourcefabric/[product]/tags.

