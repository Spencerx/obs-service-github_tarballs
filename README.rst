========================================================================
 OBS service for downloading tarballs and commit information from github
========================================================================

.. image:: https://travis-ci.org/mapleoin/obs-service-github_tarballs.png
   :target: https://travis-ci.org/mapleoin/obs-service-github_tarballs

This is an `Open Build Service`_ source service. It downloads a tarball
from a remote URL and updates the ``.spec`` and ``.changes`` files with
git commit information from the `github API`_.

How It Works
------------

The ``Version`` field will be set to ``%(git_latest_release)s``.
Where ``git_latest_release`` is the ``tag_name`` as read from the GitHub
API call.
You need to have valid ``Release`` added to your repository. Without,
this service will not work. See `github API LatestRelease`_.

On the first run, ``github_tarballs`` will just set the spec file's
``Version`` field to the latest git release. The .changes file will only
be updated with commit message information when newer commits (compared
to the one now set in ``Version``) are found. Comparison is made between
tags.

The ``github_tarballs`` service will also change the specfile's
``Source:`` to the ``filename`` argument of the service and the ``%setup
-q`` line to match the parent folder name in the tarball.

Rate Limiting
-------------

The github API rate limits requests. The limit can be extended by using
github credentials to access the API. ``obs-service-github_tarballs``
will read and use these credentials from the
``.github_tarballs_credentials`` file in the current user's home
directory if it can. The file should contain one line with the standard
in standard HTTP BasicAuth format ``username:password``.

Dependencies
------------

Requires argparse which is part of python2.7, but available as a
third-party dependency in python2.6.

The tests require `python-mock`_. To run them, just use ``nosetests`` or
``python -m unittest discover`` (on python2.7).

Contributing
------------
This is the git repository for `openSUSE\:Tools/obs-service-github_tarballs`_.
The authoritative source is https://github.com/openSUSE/obs-service-github_tarballs.

You can submit or ask for improvements using github's Pull Requests or
Issues. If you're sending a patch, please make sure the testsuite is
still running and also run flake8 on the files you've modified. It would
be great if you could also modify this README file to describe new
 functionality and add tests.

You can take a look at the .travis.yml file to see how the testsuite and
flake8 are being run.


.. _Open Build Service: http://openbuildservice.org/
.. _github API: http://api.github.com/
.. _github API LatestRelease: https://developer.github.com/v3/repos/releases/#get-the-latest-release
.. _python-mock: http://www.voidspace.org.uk/python/mock/mock.html
.. _openSUSE\:Tools/obs-service-github_tarballs: https://build.opensuse.org/package/show/openSUSE:Tools/obs-service-github_tarballs

