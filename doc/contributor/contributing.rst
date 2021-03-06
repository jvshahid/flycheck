=====================
 Contributor’s Guide
=====================

Thank you very much for your interest in contributing to Flycheck! We’d like to
warmly welcome you in the Flycheck community, and hope that you enjoy your time
with us!

There are many ways to contribute to Flycheck, and we appreciate all of them. We
hope that this document helps you to contribute. If you have questions, please
ask on our `issue tracker`_ or in our `Gitter chatroom`_.

For a gentle start please take a look at all the things we `need your help
with`_ and look for `beginner-friendly tasks`_.

Please note that all contributors are expected to follow our :ref:`Code of
Conduct <flycheck-conduct>`.
>
.. _issue tracker: https://github.com/flycheck/flycheck/issues
.. _Gitter chatroom: https://gitter.im/flycheck/flycheck
.. _need your help with: https://github.com/flycheck/flycheck/issues?q=is%3Aopen+is%3Aissue+no%3Aassignee
.. _beginner-friendly tasks: https://github.com/flycheck/flycheck/labels/beginner%20friendly

.. _flycheck-bug-reports:

Bug reports
===========

Bugs are a sad reality in software, but we strive to have as few as possible in
Flycheck. Please liberally report any bugs you find. If you are not sure whether
something is a bug or not, please report anyway.

If you have the chance and time please `search existing issues`_, as it’s
possible that someone else already reported your issue. Of course, this doesn’t
always work, and sometimes it’s very hard to know what to search for, so this is
absolutely optional. We definitely don’t mind duplicates, please report
liberally.

To open an issue simply fill out the `issue form`_. To help us fix the issue,
include as much information as possible. When in doubt, better include too much
than too little. Here’s a list of facts that are important:

* What you did, and what you expected to happen instead
* Whether and how you were able to `reproduce the issue in emacs -Q`_
* Your Flycheck setup from ``M-x flycheck-verify-setup``
* Your operating system
* Your Emacs version from ``M-x emacs-version``
* Your Flycheck version from ``M-x flycheck-version``

.. _search existing issues: https://github.com/flycheck/flycheck/issues?q=is%3Aissue
.. _issue form: https://github.com/flycheck/flycheck/issues/new
.. _reproduce the issue in emacs -Q: http://www.lunaryorn.com/2015/11/29/reproduce-bugs-in-emacs-Q.html

.. _flycheck-windows-issues:

Windows-only issues
-------------------

As Flycheck does not support Windows officially we generally do *not* attempt to
fix issues that only occur on Windows. We will move all Windows-only issues to
the `list of open Windows issues`_, and leave them to Windows users and
developers.

We welcome anyone who wants to fix open Windows issues, and we will merge pull
requests for improved Windows compatibility. If you know Windows and Emacs,
please take a look at the list of open Windows issues and try to fix any of
these.

.. _list of open Windows issues: https://github.com/flycheck/flycheck/labels/windows%20only

Feature requests
================

To request a new feature please open a new issue through our `issue form`_.
A feature request needs to find a core developer or maintainer who adopts and
implements it.

The Build system
================

Flycheck provides a :file:`Makefile` with some convenient targets to compile and
test Flycheck.  The Makefile requires Cask_, the Emacs Lisp dependency manager.
Run ``make help`` to see a list of all available targets.  Some common ones are:

- ``make init`` initialises the project by installing local Emacs Lisp
  dependencies.
- ``make compile`` compiles Flycheck and its libraries to byte code.
- ``make specs`` runs all Buttercup_ specs for Flycheck.  Set :makevar:`PATTERN`
  to run only specs matching a specific regular expression, e.g. ``make
  PATTERN='^Mode Line' specs`` to run only tests for the mode line.
- ``make test`` runs all ERT unit tests for Flycheck.  We are phasing ERT out in
  favour of Buttercup; no new ERT unit tests will be added and this target will
  eventually be removed.
- ``make integ`` runs all integration tests for Flycheck syntax checkers.  These
  tests are very dependent on the checker programs and their versions; expect
  failures when running this target.  Set :makevar:`SELECTOR` to run only tests
  matching a specific ERT selector, e.g. ``make SELECTOR='(language haskell)'
  integ`` to run only integration tests for Haskell.  ``make LANGUAGE=haskell
  integ`` is a shortcut for this.

.. _Cask: http://cask.readthedocs.io/
.. _Buttercup: https://github.com/jorgenschaefer/emacs-buttercup

Pull requests
=============

Pull Requests are the primary mechanism to submit your own changes to
Flycheck. Github provides great documentation about `Pull Requests`_.

.. _Pull Requests: https://help.github.com/articles/using-pull-requests/

Please make your pull requests against the ``master`` branch.

Use ``make specs test`` to test your pull request locally. When making changes
to syntax checkers of a specific language, it’s also a good idea to run
:samp:`make LANGUAGE={language} integ` and check whether the tests for the
particular language still work.  A successful ``make integ`` is by no means
mandatory for pull requests, though, we will test your changes, too.

All pull requests are reviewed by a :ref:`maintainer <flycheck-maintainers>`.
Feel free to mention individual developers (e.g. ``@lunaryorn``) to request a
review from a specific person, or ``@flycheck/maintainers`` if you have general
questions or if your pull request was waiting for review too long.

Additionally all pull requests go through automated tests on `Travis CI`_ which
check code style, run unit tests, etc.

After the pull request was reviewed and if all tests passed maintainers will
leave a ``LGTM`` comment at which point the pull request is ready for being
merged.

.. _Travis CI: https://travis-ci.org/flycheck/flycheck/pull_requests

Commit guidelines
-----------------

The art of writing good commit messages is a wide subject. This model commit
message illustrates our style::

   Fix a foo bug

   The first line is the summary, 50 characters or less.  Write in the
   imperative and in present tense: “Fix bug”, not “fixed bug” or “fixes
   bug”.

   After the summary more paragraphs with detailed explanations may follow,
   wrapped at 72 characters.  Separate multiple paragraphs by blank lines.

   You may use simple formatting like *emphasis* or _underline_, but keep
   it to a minimum.  Commit messages are not in Markdown :)

   Commit messages may reference issues by number, like this: See GH-42.
   Please use `GH-` to prefix issue numbers.  You may also close issues
   like this: Fixes GH-42 and closes GH-42.

`Git Commit`_ and Magit_ provide Emacs mode for Git commit messages, which helps
you to comply to these guidelines.

.. _Git Commit: https://github.com/magit/magit/
.. _Magit: https://github.com/magit/magit/

Writing documentation
=====================

Documentation improvements are very welcome.  Flycheck’s manual is written in
reStructuredText_ and built with Sphinx_.  The source of the manual resides in
the ``doc/`` directory.

You need Python 3.4 or newer to install Sphinx_ for Flycheck’s documentation.
On OS X it is recommended that you use Homebrew_ to install the latest Python
version with ``brew install python3``.  On Linux you should be able to obtain
Python 3.4 from the package manager of your distribution.

With Python 3 installed change into the ``doc/`` directory and run ``make init``
to install Sphinx and related tools required for Flycheck’s documentation.  We
recommend that you use virtualenv_ to avoid a global installation of Python
modules.  ``make init`` will warn you if you do not.

When editing documentation run ``make html-auto`` to view the results of your
edits.  This target runs a local webserver at http://localhost:8000 which serves
the HTML documentation and watches the documentation sources for changes to
rebuild automatically.  When you finished your edits it is a good idea to run
``make linkcheck`` to verify all links in the documentation.  Note that this
target can take a while especially when run on a clean build.

Run ``make help`` to see a list of all available Make targets for the
documentation.

Documentation pull requests work in the same way as other pull requests.  To
find documentation issues sort by the `documentation`_ label.

.. _ReStructuredText: http://docutils.sourceforge.net/rst.html
.. _Sphinx: http://www.sphinx-doc.org
.. _Homebrew: http://brew.sh
.. _virtualenv: https://virtualenv.pypa.io/en/latest/
.. _A-documentation: https://github.com/flycheck/flycheck/labels/documentation

Issue management
================

We use Github labels for basic issue management:

- **The red “bug” label denotes critical bugs in Flycheck that must be fixed
  urgently.**
- Violet labels describe the area of Flycheck the issue belongs to.
- The green “beginner friendly” label denotes easy tasks for newcomers to the
  project.
- Orange labels denote blockers.
- Grey labels indicate resolutions to issues.

Out of tree contributions
=========================

There are many ways that you can contribute to Flycheck that go beyond
this repository.

Answer questions in our `Gitter channel`_ or on StackExchange_.

Participate in Flycheck discussions in other Emacs communities and help
users with troubles.

Write :ref:`extensions for Flycheck <flycheck-extensions>`.

.. _Gitter channel: https://gitter.im/flycheck/flycheck
.. _StackExchange: https://emacs.stackexchange.com/questions/tagged/flycheck

--------------

This contributing guide is heavily inspired by `Rust’s excellent
contributing
information <https://github.com/rust-lang/rust/blob/master/CONTRIBUTING.md>`__.
