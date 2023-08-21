# Dotbot rsync Plugin

To be used with [dotbot](https://github.com/anishathalye/dotbot),
this plugin allows to sync files from dotfiles repo.

You can now track files that should not be world viewable or require special permissions.

## Prerequisites

`rsync` (version 3.1 or newer) needs to be available on the system and runnuble by the user executing `dotbot`

## Usage

Add the plugin as a submodule to your dotfiles repo:

```
git submodule add https://github.com/j1r1k/dotbot-sync.git
```

Execute `dotbot` with plugin parameter

```
./install -p dotbot-sync/sync.py
```

## Configuration

All configuration parameters can be specified either globaly in `default` task or locally for each individual record

Example containing all options enumerated with their default values:

```yaml
- defaults:
    sync:
      rsync: 'rsync'                        # rsync executable to be used
      options: ['--delete', '--safe-links'] # list of options for rsync
      create: false                         # create missing directory hierarchy
      fmode: 644                            # file mode
      dmode: 755                            # directory mode
      owner: '<current user name>'          # owner (default value is looked up at runtime)
      group: '<current user group>'         # group (default value is looked up at runtime)
      stdout: false                         # ignore stdout of rsync process
      stderr: false                         # ignore stderr of rsync process

- sync:
    ~/.ssh/authorized_keys:
       path: 'ssh/authorized_keys'
       fmode: 400

    ~/.ssh/pubkeys/:
       path: 'ssh/pubkeys/*.pub' # support for glob expressions
```
