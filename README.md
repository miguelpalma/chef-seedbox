# chef-seedbox

Chef kitchen to setup a complete seedbox

In the rest of this doc, we will assume you have a sudo enabled SSH login on a host and a network
alias `sbdev` pointing at it.

## Index

- `SRCDIR`: local host directory where your Chef's kitchen is located

## Install

On your local computer, install `knife-solo` and `librarian-chef` using your package manager or:

    gem install knife-solo librarian-chef --no-ri --no-rdoc
    # You might need to fix the path version
    export PATH=$PATH:~/.gem/ruby/2.1.0/bin

## First init

(no need to run again, this is just here for the record)

On the local host, generate skeleton:

    knife solo init ${SRCDIR}
    cd ${SRCDIR}
    librarian-chef init

## Add a new recipe

Find the recipe to install on [Opscode community site](http://community.opscode.com/) and add its name to file `Cheffile`. The following will then download all its dependencies to directory `cookbook`:

    librarian-chef install

NB: directory `cookbook` is **not** tracked by git.

Also add it to the `nodes/sbdev.json` file along with attributes from recipes you wish to override.

## Run Chef

On the local host, to install chef on the remote host:

     knife solo prepare sbdev

On the local host, to deploy the requested applications on the remote host:

    knife solo cook sbdev

## Documentation

- [knife-solo official doc](http://matschaffer.github.io/knife-solo/)
- This page is largely based on [Deploy a basic lamp stack to Digital Ocean with Chef Solo](http://adamcod.es/2013/06/04/deploy-a-basic-lamp-stack-digital-ocean-chef-solo.html)

## TODO

- Re-use pre-made cookbooks
  - apache2
  - fail2ban
  - munin
  - openssh
  - vsftpd

  - htpasswd (Manage an htpasswd file)
  - ssh-keys (Creates "authorized_keys" in user "~/.ssh" directory from a data bag)

- Use Nagios rules as TDD tests
