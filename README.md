# kwapi-g5k_vagrant
Vagrant to make debian package of kwapi-g5k

# How to generate a new package ?
* Edit version in the *setup.py* file
* *vagrant up*
* *ls *.deb*
* *rsync -av python-kwapi_X.deb apt.g5k:*
* Do generic stuff to publish the .deb file (see Grid'5000 documentation)

# FAQ
## Why is there a different setup.py for package creation ?
The links to the etc directory are different. I haven't find a way to fix this.
The name of the rrdtool python package is different too.
The author name is different because of a problem when you parse it's name.

## Why is there a different init.d/kwapi file ?
Because python files runs under /usr/local/bin but init.d debian files runs under /usr/bin.

## How can I install this package in Grid'5000
Use the kwapi-g5k puppet classes. They are here for that.

# TODO
* add the other package generation
