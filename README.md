
## Index:

- `SRCDIR`: local host directory where your Chef's kitchen is located
- `REMOTE_HOST`: remote host IP of FQDN

## Install

On your local computer (warning: this downloads half of the galaxy):
    gem install chef       --verbose   # Or install it from your package manager
    gem install knife-solo --verbose

    export PATH=$PATH:~/.gem/ruby/2.1.0/bin   # You might need to fix the path version

Ensure your remote host is available throught SSH and that you have a sudo enabled account on it.

## First init

(no need to run again, this is just here for the record)

On the local host, generate skeleton:

    knife solo init ${SRCDIR}

## Run Chef

On the local host:

     knife solo prepare ${REMOTE_HOST}

## Documentation

[knife-solo](http://matschaffer.github.io/knife-solo/)

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
