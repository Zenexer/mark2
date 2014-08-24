# installation

## requirements

* UNIX-like operating system (Linux, Mac OS X, BSD)
* python 2.6/2.7 (+ dev package for psutil installation)
* psutil
* urwid 1.x
* twisted
* twisted-web
* twisted-words (for IRC support)
* feedparser (for RSS support)
* pyopenssl (for push notifications and IRC over SSL)

### debian/ubuntu

This should suffice:

    $ sudo apt-get install python-dev python-pip
    $ sudo pip install -r requirements.txt

### centos

CentOS and some other distros ship an older version of python. First check you have python 2.6 or 2.7:

    $ python2.6 -V
    $ python2.7 -V

If at least one of them works, you should be able to do:

    $ sudo yum install python-devel
    $ sudo easy_install pip
    $ sudo pip install -r requirements.txt

Otherwise, you need to install python 2.7. A decent guide for centos is
[located here](http://toomuchdata.com/2012/06/25/how-to-install-python-2-7-3-on-centos-6-2/). Be sure to follow the
instructions for installing distribute also.

Next, install twisted from the package on [their website](http://twistedmatrix.com/). Don't use easy_install - you
won't get the binaries that ship with twisted.

easy_install for python 2.7 is probably in `/usr/local/bin/easy_install-2.7`. You should use it to install the remaining
mark2 dependencies:

    sudo /usr/local/bin/easy_install-2.7 psutil urwid feedparser

## installation

mark2 doesn't need to be installed to a particular directory, but if you have no reasonable ideas `/usr/mark2` will be
okay. First, download mark2:

    git clone https://github.com/Zenexer/mark2.git

If you don't have git, an alternative is to download a tarball:

    wget https://github.com/mcdevs/Zenexer/archive/master.tar.gz
    tar xf master.tar.gz
    rm master.tar.gz
    mv mark2-master mark2

After downloading with git or wget, symlink the `mark2` script into your executable path:

    # Open the mark2 directory that you just extracted:
    cd mark2
    
    # Check $PATH:
    echo $PATH
    
    # If $PATH contains /usr/local/bin:
    sudo ln -s "$PWD/mark2" /usr/local/bin
    # Otherwise:
    sudo ln -s "$PWD/mark2" /usr/bin

You *need* to create a dedicated user to run servers.  **Do not run servers as root--things will break!**

    sudo adduser --disabled-password mcservers

To start a server, run `mark2 start` as `sudo -u mcservers mark2 start ...`

### tips

If your server has a strange name, you have a couple of options:

1. add it to `mark2.jar-path` in your mark2.properties
2. specify the full path to the jar in `mark2 start`

If your servers all reside in one directory, you may want to add a start
helper to your path:

    #!/bin/bash
    mark2 start /path/to/servers/$1

And run it like

    mcstart pvp

Likewise if `mark2 attach -n blah` becomes a little too much, you could always
`alias at='mark2 attach -n'`
