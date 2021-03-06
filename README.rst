=====
aptly
=====

.. image:: https://travis-ci.org/smira/aptly.png?branch=master
    :target: https://travis-ci.org/smira/aptly

.. image:: https://coveralls.io/repos/smira/aptly/badge.png?branch=HEAD
    :target: https://coveralls.io/r/smira/aptly?branch=HEAD

.. image:: https://badges.gitter.im/Join Chat.svg
    :target: https://gitter.im/smira/aptly?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge

.. image:: http://gobuild.io/badge/github.com/smira/aptly/download.png
    :target: http://gobuild.io/github.com/smira/aptly

Aptly is a swiss army knife for Debian repository management.

.. image:: http://www.aptly.info/img/aptly_logo.png
    :target: http://www.aptly.info/

Documentation is available at `http://www.aptly.info/ <http://www.aptly.info/>`_. For support use
mailing list `aptly-discuss <https://groups.google.com/forum/#!forum/aptly-discuss>`_.

Aptly features: ("+" means planned features)

* make mirrors of remote Debian/Ubuntu repositories, limiting by components/architectures
* take snapshots of mirrors at any point in time, fixing state of repository at some moment of time
* publish snapshot as Debian repository, ready to be consumed by apt
* controlled update of one or more packages in snapshot from upstream mirror, tracking dependencies
* merge two or more snapshots into one
* filter repository by search query, pulling dependencies when required
* publish self-made packages as Debian repositories
* mirror repositories "as-is" (without resigning with user's key) (+)
* support for yum repositories (+)

Current limitations:

* translations are not supported yet

Download
--------

To install aptly on Debian/Ubuntu, add new repository to /etc/apt/sources.list::

    deb http://repo.aptly.info/ squeeze main

And import key that is used to sign the release::

    $ gpg --keyserver keys.gnupg.net --recv-keys 2A194991
    $ gpg -a --export 2A194991 | sudo apt-key add -

After that you can install aptly as any other software package::

    $ apt-get update
    $ apt-get install aptly

Don't worry about squeeze part in repo name: aptly package should work on Debian squeeze+,
Ubuntu 10.0+. Package contains aptly binary, man page and bash completion.

If you would like to use nightly builds (unstable), please use following repository::

    deb http://repo.aptly.info/ nightly main

Binary executables (depends almost only on libc) are available for download from `Bintray <http://dl.bintray.com/smira/aptly/>`_.

If you have Go environment set up, you can build aptly from source by running (go 1.3+ required)::

    go get -u github.com/mattn/gom
    mkdir -p $GOPATH/src/github.com/smira/aptly
    git clone https://github.com/smira/aptly $GOPATH/src/github.com/smira/aptly
    cd $GOPATH/src/github.com/smira/aptly
    gom -production install
    gom build -o $GOPATH/bin/aptly

Aptly is using `gom <https://github.com/mattn/gom>`_ to fix external dependencies, so regular ``go get github.com/smira/aptly``
should work as well, but might fail or produce different result (if external libraries got updated).

If you don't have Go installed (or older version), you can easily install Go using `gvm <https://github.com/moovweb/gvm/>`_.


