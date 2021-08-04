# Chomp

Quick clone Launchpad Git branches for reviewing merge proposals.

The Launchpad Merge Proposal interface is extremely limited, so it is often
helpful to open the changes in your local editor. However, it can be a little
tedious to get the correct clone command, clone it into your repository
directory with a different name (so you don't get it confused with the
main version), open it up in your editor, and then delete it when your'e done.

Chomp automates that.

This was originally intended to go hand-in-hand with the Review Gator workflow
on the Canonical Public Cloud team (ergo the name) but it works perfectly
without it.

## Installation

For Chomp to work, your Git *must* have the `lp:` shortcut configured globally
([learn how here](https://help.launchpad.net/Code/Git#Configuring_Git)).

Place the `chomp` file in your environment path, e.g. in `~/.local/bin`.

By default, Chomp will check out repositories in the directory `~/.chomp`, but
you can override this by setting the environment variable `CHOMP_PATH`.

Chomp uses VSCode to "open in editor" by default, namely with the '`code -n %P`'
command, where the path to the repository is subtituted for `%P`.
You can override this command by setting the environment variable
`CHOMP_EDITOR`.

## Usage

To use Chomp, you only need the Launchpad repository and branch as it
appears on the top of the Merge Request. It will always take the form
`~user/group/+git/repo` or `~user/group/+git/repo:branch`.

For example: `~codemouse92/cloudware/+git/cpc_docs:fixtypos`

That line must *always* start with a tilde for Chomp to recognize it.
To clone that repository and branch, simply run:

```
chomp ~codemouse92/cloudware/+git/cpc_docs:fixtypos
```

It will clone the repository in Chomp's working directory with the name
`user.group.repo` (e.g. `codemouse92.cloudware.cpc_docs`), and check out the
appropriate branch (if one was specified). Then it will ask if you want to
open the repository directory in your editor (and you only need to
hit enter!)

Not sure if you've cloned this before? Not to worry. If Chomp finds the same
repository again (from the same user), it'll let you decide if you want to
reclone, switch branch, or just abort.

If you just want to edit a repository you've already checked out, run
`chomp edit`, like this:

```
chomp edit ~codemouse92/cloudware/+git/cpc_docs:fixtypos
```

That will also handle switching to the correct local branch. (Edit never pulls
from remote.)

Finally, when you're done with the repository and want it off your system,
just run `chomp remove`:

```
chomp remove ~codemouse92/cloudware/+git/cpc_docs:fixtypos
```

Easy as pie.
