.. _git:

Git and GitHub Pull Requests
============================

At Sourcefabric we use Git to manage source code and revision control
and GitHub to mananage the code committing cycle. You can find all 
official Git repositories at
`https://github.com/sourcefabric/ <https://github.com/sourcefabric/>`_.

This page is a guide to using Github at Sourcefabric. For more generic 
information on using Git and Github there is some great information on the 
`Github help page <http://help.github.com>`_

Using Github
-------------

Let's assume your GitHub account is `johndoe`, and that the Sourcefabric project
you want to contribute to is `Superdesk`.

The first thing to do is to fork the Superdesk repository in GitHub, so:

- Login in your GitHub account
- Go to the Superdesk project space in GitHub
- Look for the button labelled Fork and click on it

You now have in your GitHub account a copy of the Superdesk repository, that
is your fork and lives only in GitHub.

Now you need to download the source code so that you can work locally in your
own computer. Open a console and type in this:

    $ git clone git@github.com:johndoe/Superdesk.git

This will create a new directory Superdesk in your current working directory
containing a clone of your GitHub repository. This clone has by default a single
remote called origin, that points to your fork on GitHub.

Your local copy of the Superdesk project is tracking your GitHub fork, but what
about the original Sourcefabric repository? It is important to track the original
project, otherwise you won't get updates from all the other developers that get 
merged into `upstream`.

To add the the original repository as `upstream`:

    $ git remote add upstream https://github.com/sourcefabric/Superdesk.git
    $ git fetch upstream

Working on a ticket
--------------------

Create a new branch off `upstream/master` any time you start working on a ticket.

    $ git checkout -b ticket-xxxxx upstream/master

.. You can also create a branch based on a different branch than master, for example when working on a bug fix for a release branch, let's say 1.2 
    $ git checkout -b ticket-xxxxx-1.2 upstream/1.2

Do your work and commit to your local branch (remember to follow the
<conventions on commit messages>, that is a great help for core developers when
reviewing your code) and push your changes to your fork in GitHub.

    $ git push origin ticket-xxxxx

The first time you run this command you will notice in your GitHub fork that a
new branch has been created. From then on you can use the same command to
update your branch with new commits.

Git branching Model
--------------------

We use the following branching model:

* main development branch, `master`: the base for all development. Every 
  time you start working on something new, you should do it based on
  `master`. Major releases are based on `master`.
* *release* branches: officially supported versions of the product are kept in
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

* *feature* branches: when a new major feature or improvement is being done,
  likely work happens in a feature branch to not affect `master` directly.

  - Lifetime of feature branches goes from the moment where the implementation
    begins till the moment when the branch is merged back to `master`. Once that
    happens the feature branch may be removed from the repository.
  - A feature branch never triggers a release. Features are always merged back to
    `master` in order to be released.
  - Branch naming convention: <Jira Ticket Code>-<Short Descriptive Title>, where
    <Short Descriptive Title> must be in lowercases and must use the dash sign “-”
    as word separator (e.g. cs-2764-autosave).


.. admonition:: Usage in production

   If you want to deploy a product in a production environment we highly 
   recommend getting an official release package instead of using the 
   development version. 

Released Versions
^^^^^^^^^^^^^^^^^^

Officially released versions are available in the form of Git tags. Every time a
new version is released, a new Git tag is created, using the following naming
convention:

v<Version Number> (e.g. v4.0.0, v2.1.1-RC2)

You can see the list of released tags by checking:
https://github.com/sourcefabric/[product]/tags.


